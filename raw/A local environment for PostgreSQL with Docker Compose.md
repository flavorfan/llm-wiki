---
title: "A local environment for PostgreSQL with Docker Compose"
source: "https://medium.com/norsys-octogone/a-local-environment-for-postgresql-with-docker-compose-7ae68c998068"
author:
  - "[[Christophe Vaudry]]"
published: 2025-06-11
created: 2026-04-30
description: "I have created a small project on GitHub that provides a docker compose file and a basic directory structure to have a local development env"
tags:
  - "clippings"
---
![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*oFtufjSXiK4Udjl7NFEsrw.png)

## Introduction

I have created a [small project on GitHub](https://github.com/TGITS/docker-compose-examples/tree/main/postgresql-docker-compose-examples) that provides a *docker compose file* and a basic directory structure to have a local development environment with a [PostgreSQL](https://www.postgresql.org/) database.

All you need is to have a container engine compatible with *docker* and *docker compose* available in the command line. This project has been developed and tested under Windows 11 Professional with [Docker](https://www.docker.com/) and [Rancher Desktop](https://rancherdesktop.io/). However it should work on Windows, MacOs and Linux, with directly [Docker](https://www.docker.com/) or [Docker Desktop](https://www.docker.com/products/docker-desktop/).

## TL;DR

If you want to skip the details and just use a docker compose file to run a postgreSQL instance, here you go:

- Get the [project on GitHub](https://github.com/TGITS/docker-compose-examples) (you can get the zip file, clone or fork the GitHub repository)
- Go to the `docker-compose-examples/postgresql-docker-compose-examples/postgresql-complete` directory and run the following command: `docker compose -f dc-postgresql-complete.yml up -d`.
- Access the instance with the `psql` cli by opening an interactive shell on the running container of the postgres instance with `docker exec -it postgres /bin/sh` and then in the open shell run the cli with `psql -W -Umydb -dmydb`; you will be prompted to enter a password which is defined in the `.env` file, under the variable `POSTGRES_PASSWORD`.
- You also have an instance of [pgAdmin](https://www.pgadmin.org/) available on `localhost:5433` and an instance of [Metabase](https://www.metabase.com/) available on `localhost:5434`. The user name and password used are the ones defined in the `.env` file.
- To stop the containers: `docker compose -f dc-postgresql-complete.yml down`.

## The docker compose file

First, you have to fetch the [project on GitHub](https://github.com/TGITS/docker-compose-examples). You should find in the project a ***postgresql-docker-compose-examples*** directory that contains the following sub-directories and files:

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*42LiTAb30KhZsWR9ApHNig.png)

The various directories and files available

The following picture show the docker compose file `dc-postgresql-complete.yml` and its relations to the other files.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*HdKXZ2E1pXxkrmnNxptqBA.png)

Content of the docker compose file dc-postgresql-complete.yml

The `.env` file defines some system variables used in the docker compose file for [PostgreSQL](https://www.postgresql.org/) and [pgAdmin](https://www.pgadmin.org/). You can of course change the values to your needs if necessary.

The docker compose file by itself is quite straightforward.

One service is defined for the `postgres` instance. The retrieved container image is the `latest`. You can (and in some case you should) change to point to a specific version of `postgres`.

You have two other services respectively for [pgAdmin](https://www.pgadmin.org/) and [Metabase](https://www.metabase.com/). The retrieved images are also the `latest` but that can be adapted easily to get a specific version. The examples on the [project on GitHub](https://github.com/TGITS/docker-compose-examples) are a little bit more detailled on this point.

A network and several volumes are defined. It is not strictly necessary but it is a good practice. Furthermore if you create a larger docker compose file based on this one, it can be relevant to be aware of volumes and network.

In this example, the database is initialized with a table and some data. The code for the initialization is under the directory `initdb.d`.

![](https://miro.medium.com/v2/resize:fit:1150/format:webp/1*XP6rZUgjrsA0TPRFu_IJkw.png)

Content of the initdb.d directory

The astute reader will have remarked that the directory `initdb.d` is mapped to the directory `docker-entrypoint-initdb.d` inside the container. As the name suggests, the code in this directory is executed when the container is started. Here, this is the file `init.sql` which contains the SQL code that is executed when the container is run.

```c
CREATE TABLE pokemon (
    num INT,
    name TEXT,
    type1 TEXT,
    type2 TEXT,
    total INT,
    hp INT,
    attack INT,
    defense INT,
    special_attack INT,
    special_defense INT,
    speed INT,
    generation INT,
    legendary BOOLEAN
);

COPY pokemon
FROM '/docker-entrypoint-initdb.d/pokemon.csv'
DELIMITER ','
CSV HEADER;
```

There is only the creation of a table and the loading of the data from a csv file (`pokemon.csv`). Of course it is only an example, you can have a more complex initialization if needs be.

## Running and stopping the containers with the PostgreSQL instance

To run the containers with the associated [PostgreSQL](https://www.postgresql.org/), [pgAdmin](https://www.pgadmin.org/) and [Metabase](https://www.metabase.com/) instances using `docker-compose`, open a shell on your computer go to the `docker-compose-examples/postgresql-docker-compose-examples/postgresql-complete` directory and run the following

```c
docker compose -f dc-postgresql-complete.yml up -d
```

If your are on Windows, you can use WSL or if you have the docker engine installed (via Docker Desktop or Rancher Desktop) you can use Windows Powershell as in the following screenshots.

![](https://miro.medium.com/v2/resize:fit:1376/format:webp/1*5mZXYuIId87qR95bfWwFeg.png)

First pull of the default latest images version from Windows Powershell

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*m25JdCxsWeiiPN6p8cY46w.png)

Running containers of the default latest image of PostgreSQLs, pgAdmin and Metabase on Rancher Desktop on Windows

To stop the container, type the following in your shell, from the directory which contains the docker compose file `dc-postgresql-complete.yml`: `docker compose -f dc-postgresql-complete.yml down`

![](https://miro.medium.com/v2/resize:fit:1380/format:webp/1*-b7Eq4Q4Du9ZydYodMRFXw.png)

Stopping the containers with docker compose

## Accessing the PostgreSQL instance with the CLI in the container

To access your database instance with the dedicated CLI from a shell in the container itself, you have to open an interactive shell on the running container of the [PostgreSQL](https://www.postgresql.org/) instance:

```c
docker exec -it postgres /bin/sh
```

The container name defined in `dc-postgresql-single.yml` is `postgres`.

You then have to run the Postgres CLI from this shell:

```c
psql -W -Umydb -dmydb
```

With the option `-W`, you will be prompted for a password. The expected password is defined in the `.env` file, under the variable `POSTGRES_PASSWORD`.

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*AMgYZxI4YIof9cWf2xnpeQ.png)

Accessing the PostgreSQL instance from the PSQL CLI

You can now try and execute a query. For example you can try:

```c
SELECT * FROM public.pokemon 
LIMIT 10;
```

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*4KuYetwURxd9pv4HCtavEw.png)

Accessing the PostgreSQL instance from the PSQL CLI and executing a query

To quit `psql` you can type `exit` and to quit the shell you can also type `exit`.

The `.env` file defines the 3 environment variables used in the docker compose file `dc-postgresql-single.yml`: `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD`, which respectively corresponds to the name of a [PostgreSQL](https://www.postgresql.org/) Database, the name of a user of this database and the password of this user.

The Postgres instance will be created with this database and the associated user.

## Accessing the PostgreSQL instance with pgAdmin

When the containers are up, [pgAdmin](https://www.pgadmin.org/) will be available on `localhost:5433`.

To configure [pgAdmin](https://www.pgadmin.org/), when the application is started, on your first run, you should have something similar to the next screenshot. You have to provide the values of the environment variables `PGADMIN_DEFAULT_EMAIL ` and `PGADMIN_DEFAULT_EMAIL`.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*X8b0rEPs3moyw7JdO79IPQ.png)

First connection to pgAdmin (Web)

You first need to register a new server by a right click on `Servers` in the `Object explorer`.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*hzwPZk2urxUmKFUkmtv_vw.png)

Initiating the registration of a new server

A popup window with several tabs should appear. In the `General` tab you have to fill the `Name` field (this is the name you want to give to your [PostgreSQL](https://www.postgresql.org/) instance, it can be whatever you want). You should also toggle on the `Connect now?` button.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*mvwN_Zanjdb05iW5PEvETA.png)

Configuring the connection to the new server (1/2)

In the `Connection` tab, you have to fill the `Host name/address` field with the value `postgres` (the host name of the [PostgreSQL](https://www.postgresql.org/) instance in the container), the `Port` field with the value `5432`, and the fields `Maintenance database`, `Username` and `Password` with respectively the values of the environment variables `POSTGRES_DB`, `POSTGRES_USER`, and `POSTGRES_PASSWORD`.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*pyvxHvU0NBKXPe3sxSCIvA.png)

Configuring the connection to the new server (2/2)

When you click on the `Save` button, [pgAdmin](https://www.pgadmin.org/) should connect to the database server and it should appear in the `Object Explorer` panel.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*USEVk8--EknfrZ_ZCyJyrg.png)

Accessing the new database server

You can navigate to the table `Pokemon` which should have been initialized.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*n80WjK1coLQua_1ZWy-blQ.png)

Accessing the table with which the database has been initialized

## Accessing the PostgreSQL instance with Metabase

[Metabase](https://www.metabase.com/) is not a database tool like [pgAdmin](https://www.pgadmin.org/) or [DBeaver](https://dbeaver.io/). It is a *\_business intelligence\_* / *\_analytics\_* platform: you will not directly do low level SQL requests or working directly on the Database. It’s a tool to manipulate your data to extract information from them.

As such it does not have the same use as [pgAdmin](https://www.pgadmin.org/) but can be useful in its own right depending on your needs.

When the containers are up, [Metabase](https://www.metabase.com/) will be available on `localhost:5434`.

On the first connection, you will have to configure [Metabase](https://www.metabase.com/).

As you can see in the first screenshot, the first screen is not necessarily in English (in French in my case, which corresponds to my locale). However you can choose the appropriate language for your configuration in the next screen. On this first screen, you just have to click on the button.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*BUnCk0J7Le-M3Pce2YacpQ.png)

First connection to Metabase — Configuration (1/7)

You choose the language for the user interface and then enter some *personal* information (name, email, etc.)

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ptuKPNQ1m4YHgEHLmG2H5g.png)

First connection to Metabase — Configuration (2/7)

You will next indicate what is your intended use of [Metabase](https://www.metabase.com/) if you know it.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*kKOgx_m1zt_ftPrTu_cAFA.png)

First connection to Metabase — Configuration (3/7)

You will next indicate to which kind of database you want to connect, in our case [PostgreSQL](https://www.postgresql.org/).

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*8f1hZRO-1WmHK9mqK2_Z8w.png)

First connection to Metabase — Configuration (4/7)

After selecting [PostgreSQL](https://www.postgresql.org/), you will have to configure your connection:

- The host is `postgres` (as defined in the docker compose file)
- The port is `5432` (as defined in the docker compose file)
- The fields `Database name`, `Username` and `Password` should be filled respectively with the values of the environment variables `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD` defined in the `.env` file.

You can now connect to the database!

![](https://miro.medium.com/v2/resize:fit:1208/format:webp/1*Ue0jQCFWm4sGVEToWYCcjg.png)

First connection to Metabase — Configuration (5/7)

You can finally give your usage data preferences.

![](https://miro.medium.com/v2/resize:fit:1154/format:webp/1*BEsA0cTYoSpos_gkLLHt6A.png)

First connection to Metabase — Configuration (6/7)

At last, the configuration is done!

![](https://miro.medium.com/v2/resize:fit:1366/format:webp/1*G5WH0qYqTunrTYBKtfyiUQ.png)

First connection to Metabase — Configuration (7/7)

You can now explore your data. [Metabase](https://www.metabase.com/) invites you to have a look at the table created at initialization (Here \`Pokemon\`).

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*3qULMeJN5dKbxG_je3rtZQ.png)

Accessing the data

You can start exploring the data:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Bfdhotm5Cha1nrwnY78Wqw.png)

Exploring the data with Metabase

## Accessing the PostgreSQL instance with DBeaver

[DBeaver Community](https://dbeaver.io/) is an open source tool that offers a graphical user interface to access various relational databases including [PostgreSQL](https://www.postgresql.org/).

After starting [DBeaver](https://dbeaver.io/):

- Go in the menu `File` and select the `New` option (`File > New`) or use the shortcut `Ctrl+N`.
- Select `DBeaver > Database Connection` and click on the `Next` button.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*QCfZ3jEV3MZsaOIuaQxFkA.png)

Selecting the creation of a new Database Connection

- Select `PostgreSQL` and click on the `Next` button

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*jHUbre2DuYSFTQf_g6QcPw.png)

Selecting PostgreSQL as the database for which you want to create a connection

- A window with the connection settings to fill should open. You should change the value for `Database` (should be the value associated with `POSTGRES_DB` in the `.env` file), for `Username` (should be the value associated with `POSTGRES_USER` in the `.env` file) and `Password` (should be the value associated with `POSTGRES_PASSWORD` in the `.env` file). The default value for the other fields should be the values you need.
![](https://miro.medium.com/v2/resize:fit:1282/format:webp/1*vBp9srg5a569W46aOLUi6w.png)

Database connection settings

- If it is the first time you try to connect to a [PostgreSQL](https://www.postgresql.org/) Database, you will need to download the database driver. To this end, you have to select the tab `Driver properties` [DBeaver](https://dbeaver.io/) should propose to download a [PostgreSQL](https://www.postgresql.org/) driver, you just have to click on the `Download` button.
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*87naVDEbovI5f9yPi93OHQ.png)

Downloading the database driver

- When the driver has been downloaded, you will now see the driver properties and you just have to click on the `Finish` button.
![](https://miro.medium.com/v2/resize:fit:1282/format:webp/1*DHQlkPnm-QYni-Fjd6hXMg.png)

Driver properties

- You should now see the connection to your [PostgreSQL](https://www.postgresql.org/) Database in the `Database Navigator` view.
![](https://miro.medium.com/v2/resize:fit:1308/format:webp/1*I4KGNoBj2F7ZpQiGbGhPWw.png)

The new connection in the Database Navigator view

- You can now access your new database, with its for now unique table and you can found the created user under `Roles`.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*GngVVyu5vU-osi32ed9_qg.png)

Accessing the new database from the Database Navigator view

## Accessing the PostgreSQL instance with the pgAdmin Desktop client

When you [download pgAdmin 4](https://www.pgadmin.org/download/), it comes with a desktop graphical user interface written in Electron.

Once [pgAdmin](https://www.pgadmin.org/) is installed on your computer, it is under the subdirectory `runtime` with the name `pgAdmin4` or `pgAdmin4.exe` on Windows. Executing this file will start the [pgAdmin](https://www.pgadmin.org/) web application and the Electron application.

The whole application require a lot of ressources of your system and [DBeaver](https://dbeaver.io/) is probably a more lightweight solution. However, pgAdmin is a very complete and powerful solution to work with a [PostgreSQL](https://www.postgresql.org/) instance. As such it is a matter of needs and preferences.

To configure [pgAdmin](https://www.pgadmin.org/):

- Run the desktop application (`pgAdmin4` or `pgAdmin4.exe` on Windows). When the application is started, on your first run, you should have something similar to the next screenshot
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*0cESdVQu9xfY0d5eMfv-3A.png)

First connection to pgAdmin

- You first need to register a new server by a right click on `Servers` in the `Object Explorer` panel.
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*QdFCpkrgDdajNp5RpB2dnw.png)

Initiating the registration of a new server

- A popup window with several tabs should appear. In the `General` tab you have to fill the `Name` field (this is the name you want to give to your [PostgreSQL](https://www.postgresql.org/) Instance, it can be whatever you want). You should also toggle on the `Connect now ?`button.
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*gTTUTOv2mkcNH1xF4Xoa3w.png)

Configuring the connection to the new server

- In the `Connection` tab, you have to fill the `Host name/address` field with the value `localhost`, the `Port` field with the value `5432`, and the fields `Maintenance database`, `Username` and `Password` with respectively the values of the environment variables `POSTGRES_DB`, `POSTGRES_USER`, and `POSTGRES_PASSWORD`.
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*6NkeFHjo3ApF-64SYLqlBw.png)

Configuring the connection to the new server

- When you click on the `Save` button, [pgAdmin](https://www.pgadmin.org/) should connect to the database server and it should appear in the `Object Explorer` panel.
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*7pbMv2jSjIKDFopd2XA2fQ.png)

Accessing the new server

## Dedicated docker compose files

**Dedicated docker compose file with only PostgreSQL**

If you only need a [PostgreSQL](https://www.postgresql.org/) instance you can use the docker compose file under `docker-compose-examples/postgresql-docker-compose-examples/postgresql-only`.

- To fire up the container: `docker compose -f dc-postgresql-only.yml up -d`
- To stop it: `docker compose -f dc-postgresql-only.yml down`

The configuration of the different tools is similar to what have been presented previously if need be.

In this example the [PostgreSQL](https://www.postgresql.org/) instance database is not initialized with a table.

![](https://miro.medium.com/v2/resize:fit:1370/format:webp/1*74LQ1sdJIuu7OJqOiNNCQg.png)

First pull of an image postgres:17.4-alpine from Windows Powershell

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*f3WNhV4MnJSQOKIaTdKW_Q.png)

Running container of an image postgres:17.4-alpine on Rancher Desktop on Windows

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*ZmX_ESaRGZzEhqhhpPERIA.png)

Running container of the default latest image of postgres on Rancher Desktop on Windows

**PostgreSQL and pgAdmin**

If you only need a [PostgreSQL](https://www.postgresql.org/) instance with [pgAdmin](https://www.pgadmin.org/) you can use the docker compose file under `docker-compose-examples/postgresql-docker-compose-examples/postgresql-pgadmin`.

- To fire up the container: `docker compose -f dc-postgresql-pgadmin.yml up -d`
- To stop it: `docker compose -f dc-postgresql-pgadmin.yml down`

The configuration of [pgAdmin](https://www.pgadmin.org/) is identical to the one explained previously.

**PostgreSQL and Metabase**

If you only need a [PostgreSQL](https://www.postgresql.org/) instance with [Metabase](https://www.metabase.com/) you can use the docker compose file under `docker-compose-examples/postgresql-docker-compose-examples/postgresql-metabase`.

- To fire up the container: `docker compose -f dc-postgresql-metabase.yml up -d`
- To stop it: `docker compose -f dc-postgresql-metabase.yml down`

The configuration of [Metabase](https://www.metabase.com/) is identical to the one explained previously.

## Conclusion

With all this, you should have the basis for a local development environment for [PostgreSQL](https://www.postgresql.org/), that you can use “as is” or customize if needed. Some tools to exploit [PostgreSQL](https://www.postgresql.org/) and explore your data have also been presented. You should have all that is necessary to start with [PostgreSQL](https://www.postgresql.org/).

## Complementary ressources

- [Official PostgreSQL Site](https://www.postgresql.org/)
- [Official PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Postgresql Logo](https://wiki.postgresql.org/wiki/Logo)
- [PostgreSQL Docker Official Image on Docker Hub](https://hub.docker.com/_/postgres)
- [pgAdmin](https://www.pgadmin.org/)
- [pgAdmin Documentation](https://www.pgadmin.org/docs/pgadmin4/latest/index.html)
- [pgAdmin Official Image on Docker Hub](https://hub.docker.com/r/dpage/pgadmin4/)
- [Metabase](https://www.metabase.com/)
- [Running Metabase on Docker](https://www.metabase.com/docs/latest/installation-and-operation/running-metabase-on-docker)
- [Metabase Official Image on Docker Hub](https://hub.docker.com/r/metabase/metabase)
- [DBeaver Community](https://dbeaver.io/)
- [PostgreSQL Clients](https://wiki.postgresql.org/wiki/PostgreSQL_Clients)
- [Pre-seeding database with schema and data at startup for development environment](https://docs.docker.com/guides/pre-seeding/)
- Baeldung tutorial if you just want to use Docker and not Docker Compose: [PostgreSQL with Docker Setup](https://www.baeldung.com/ops/postgresql-docker-setup)
- Medium Post which explains how to initialize a PostgreSQL Database: [Initializing a PostgreSQL Database with a Dataset using Docker Compose: A Step-by-step Guide](https://medium.com/@asuarezaceves/initializing-a-postgresql-database-with-a-dataset-using-docker-compose-a-step-by-step-guide-3feebd5b1545)
- [The CSV File with the Pokemon data is from here](https://gist.github.com/armgilles/194bcff35001e7eb53a2a8b441e8b2c6)

I have also written similar articles on [Valkey](https://medium.com/norsys-octogone/a-local-environment-for-valkey-with-docker-compose-8be59c6b91e4), [Redis](https://medium.com/norsys-octogone/a-local-environment-for-redis-with-docker-compose-f553cf64ca58), [MongoDB](https://medium.com/norsys-octogone/a-local-environment-for-mongodb-with-docker-compose-ba52445b93ed) and [Dependency Track](https://medium.com/norsys-octogone/a-local-environment-for-dependencytrack-with-docker-compose-f59181ca1ce7) if you’re interested.

I thank my colleague [Thomas Verhoken](https://medium.com/@tverhoken) for his proofreading.