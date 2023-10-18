---
last_modified_date: 2023-09-29 21:48:59 +0200
layout: default
title: Running GatewayD
description: How to run GatewayD and test it with psql
nav_order: 4
parent: Getting Started
---

# Running GatewayD

These are the steps to make GatewayD work for you:

1. Start the PostgreSQL database.
2. Start the Redis database for caching query results.
3. Install GatewayD and the cache plugin.
4. Configure and start GatewayD.
5. Test your setup with [`psql`](https://www.postgresql.org/docs/current/app-psql.html) or any other PostgreSQL client or driver.
6. Clean up.

{: .note }
> For demo purposes, we'll use Docker to start the databases. Also, you can skip step one if you already have a database up and running.

## 1. Start your PostgreSQL database

Use the following command to start a PostgreSQL database server inside a container:

```bash
docker run --rm --name postgres-test -p 5432:5432 -e POSTGRES_PASSWORD=postgres -d postgres
```

Test you database by running the following command:

```bash
docker exec -it postgres-test psql postgresql://postgres:postgres@localhost:5432/postgres -c "\d"
```

Since the database is just created, no relations exist.

## 2. Start your Redis database

Use the following command to start a Redis server inside a container:

```bash
docker run --rm --name redis-test -p 6379:6379 -d redis
```

You can verify if both of the above worked correctly by running `docker ps`.

## 3. Install GatewayD and the cache plugin

Download and extract GatewayD and the [gatewayd-cache-plugin](/plugins/gatewayd-plugin-cache) using the following commands:

```bash
mkdir gatewayd && cd gatewayd
wget https://github.com/gatewayd-io/gatewayd/releases/download/{% github_latest_release gatewayd-io/gatewayd %}/gatewayd-linux-amd64-{% github_latest_release gatewayd-io/gatewayd %}.tar.gz
tar xf gatewayd-linux-amd64-{% github_latest_release gatewayd-io/gatewayd %}.tar.gz
./gatewayd plugin install https://github.com/gatewayd-io/gatewayd-plugin-cache@{% github_latest_release gatewayd-io/gatewayd-plugin-cache %}
```

## 4. Configure and start GatewayD

Open the `gatewayd_plugins.yaml` file with your favorite editor and change the `localPath` to `./gatewayd-plugin-cache`. Also, replace the checksum to the one provided in the `checksum.txt` file. You can verify the checksum by running the following command:

```bash
sha256sum gatewayd-plugin-cache -c checksum.txt
```

{: .note }
> If you want to see the details of what is happening behind the scenes, open the `gatewayd.yaml` in your favorite editor and set the log level of the default logger to `debug` or `trace`. Alternatively, you can set the `GATEWAYD_LOGGERS_DEFAULT_LEVEL=debug` environment variable.

Run the following command to start GatewayD:

```bash
./gatewayd run
```

Running GatewayD will produce this log output, which means that GatewayD is started and is:

1. listening on port `15432` with 10 connections to postgres in the pool.
2. running the `gatewayd-plugin-cache`.
3. having the pid `41568`.
4. exposing aggregated Prometheus metrics on `http://localhost:9090/`.
5. exposing an HTTP and a gRPC API on ports `18080` and `19090`.

```bash
2023-04-08T02:01:04+02:00 INF configuring client automatic mTLS plugin=gatewayd-plugin-cache
2023-04-08T02:01:04+02:00 INF Starting metrics server via HTTP over Unix domain socket endpoint=/metrics plugin=gatewayd-plugin-cache timestamp=2023-04-08T02:01:04.242+0200 unixDomainSocket=/tmp/gatewayd-plugin-cache.sock
2023-04-08T02:01:04+02:00 INF configuring server automatic mTLS plugin=gatewayd-plugin-cache timestamp=2023-04-08T02:01:04.243+0200
2023-04-08T02:01:04+02:00 INF Registering plugin hooks name=gatewayd-plugin-cache
2023-04-08T02:01:04+02:00 INF Plugin is ready name=gatewayd-plugin-cache
2023-04-08T02:01:04+02:00 INF Started the metrics merger scheduler metricsMergerPeriod=5s startDelay=1680912069
2023-04-08T02:01:04+02:00 INF Starting plugin health check scheduler healthCheckPeriod=5s
2023-04-08T02:01:04+02:00 INF Metrics are exposed address=http://localhost:9090/metrics
2023-04-08T02:01:04+02:00 INF There are clients available in the pool count=10 name=default
2023-04-08T02:01:04+02:00 INF Started the client health check scheduler healthCheckPeriod=1m0s startDelay=2023-04-08T02:02:04+02:00
2023-04-08T02:01:04+02:00 INF GatewayD is listening address=0.0.0.0:15432
2023-04-08T02:01:04+02:00 INF Started the HTTP API address=localhost:18080
2023-04-08T02:01:04+02:00 INF Started the gRPC API address=localhost:19090 network=tcp
2023-04-08T02:01:04+02:00 INF GatewayD is running pid=41568
```

{: .note }
> The `run` command automatically lints the configuration files and exits if there is an error. You can skip the linting by using the `--lint=false` flag.

## 5. Test your setup with `psql`

GatewayD is running on the host, while PostgreSQL is running inside a container. You can run the following command to test it. Notice that `172.17.0.1` is the IP address of the host machine.

```bash
docker exec -it postgres-test psql postgresql://postgres:postgres@172.17.0.1:15432/postgres
```

Now you can create a table and insert data into it. Querying the data will trigger the cache plugin to store the results in Redis and subsequent SELECT queries will be served from the cache. The moment you insert a new value into the table or update a row, all the cached values from that table will be invalidated.

```sql
postgres=# create table test (id int);
CREATE TABLE
postgres=# insert into test values (1);
INSERT 0 1
postgres=# insert into test values (1);
INSERT 0 1
postgres=# insert into test values (1);
INSERT 0 1
postgres=# select * from test; -- This is read from the database.
 id
----
  1
  1
  1
(3 rows)

postgres=# select * from test; -- This is read from the cache.
 id
----
  1
  1
  1
(3 rows)
```

You can check the cached keys using the following command and it should contain three keys.

```bash
docker exec -it redis-test redis-cli dbsize
```

Now, insert a new row into the `test` table:

```sql
postgres=# insert into test values (1); -- The cache is invalidated.
INSERT 0 1
```

Now, check the total number of keys again, and you'll see that there is only a single key, which means that the cached values are gone.

## 6. Clean up

You can clean up all of the above by following these steps:

1. Exit `psql` by typing `Ctrl+D` or `\q` and hitting `Enter`.
2. Stop `gatewayd` gracefully by typing `Ctrl+C`.
3. Stop the container by running `docker stop postgres-test redis-test`. The containers will be removed automatically.
