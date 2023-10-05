

### Setting Up DBMS in Docker for Testing

When developing and testing applications, especially ones like ETL frameworks, it's essential to have a consistent and easily reproducible environment. Docker offers an ideal solution by enabling developers to set up database management systems (DBMS) swiftly and without the hassles of manual configurations or system-specific issues.

Using Docker containers, developers can spin up instances of various DBMS with just a few commands. This ensures that the testing of the ETL framework is conducted in a controlled environment, closely mimicking a real-world scenario but tailored for development and testing rather than deployment.

This guide will walk you through setting up popular DBMS in Docker containers. The primary aim is to assist developers in quickly establishing their testing environments, allowing them to focus on the core ETL logic and ensuring the reliability and efficiency of data transformations.

Certainly! Here's a consolidated guide for setting up and populating a PostgreSQL instance using Docker, based on your provided configuration and requirements:



### Setting Up PostgreSQL in Docker for ETL Framework Testing

For testing our ETL framework, we'll set up a PostgreSQL instance with the following configuration:

- **Host**: localhost
- **Port**: 5432
- **User**: postgres
- **Password**: mysecretpassword
- **Database Name**: postgres

#### 1. Pull the PostgreSQL Docker Image:

Retrieve the PostgreSQL image from Docker Hub:

```bash
docker pull postgres
```

#### 2. Create and Start a PostgreSQL Container:

Initiate a Docker container with our specific configuration:

```bash
docker run --name postgres-etl-test -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
```

- `--name postgres-etl-test` gives the container a name.
- `-e POSTGRES_PASSWORD=mysecretpassword` sets the PostgreSQL instance password.
- `-p 5432:5432` exposes port 5432 on both host and container.

#### 3. Attach to the Container's Bash Shell:

Get direct interaction with the PostgreSQL instance:

```bash
docker exec -it postgres-etl-test bash
```

You'll now be inside a bash shell for the `postgres-etl-test` container.

#### 4. Setup `pgbench` and Populate the Database:

Switch to the PostgreSQL user:

```bash
su - postgres
```

Create a database:

```bash
createdb postgres
```

Initialize the database with `pgbench` (creating necessary tables):

```bash
pgbench -i postgres
```

To populate the primary table with 1 crore (10 million) rows:

```bash
pgbench -i -s 100 postgres
```

This command might take a while as it's generating and inserting a large amount of data.


### Setting Up MySQL in Docker for ETL Framework Testing

For our ETL testing environment, we will configure a MySQL instance with the following parameters:

- **Host**: localhost
- **Port**: 3306
- **User**: root
- **Password**: my-secret-pw
- **Database Name**: your_db_name

Here are the steps to achieve this:

#### 1. Pull the MySQL Docker Image:

If you haven't already, fetch the MySQL image from Docker Hub:

```bash
docker pull mysql
```

#### 2. Create and Start a MySQL Container:

Using the pulled image, launch a Docker container with the specified configuration:

```bash
docker run --name mysql-etl-test -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql
```

Here:
- `--name mysql-etl-test` gives a specific name to your container.
- `-e MYSQL_ROOT_PASSWORD=my-secret-pw` sets the password for the MySQL root account.
- `-p 3306:3306` exposes port 3306 on both the container and the host machine.

#### 3. Connect to the MySQL Instance:

To access the MySQL instance within the container:

```bash
docker exec -it mysql-etl-test mysql -uroot -p
```

You'll be prompted for the password. Enter `my-secret-pw` (or whatever password you've set).

#### 4. Create the Database:

Once you're inside the MySQL prompt, create your desired database:

```sql
CREATE DATABASE your_db_name;
```

To switch to the database you've just created:

```sql
USE your_db_name;
```

Now, you're working within the `your_db_name` database and can start creating tables, inserting data, and running queries as required.

With these instructions, you'll have a MySQL instance within a Docker container, set up according to the specified configuration, ready for ETL testing. This environment allows developers to work in a consistent database setting regardless of their local machine configurations.