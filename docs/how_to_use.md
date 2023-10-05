
**How to Use:**

**Configuration:**

To get started, prepare a single JSON configuration file. This file should encompass both the source and destination configurations, as well as specify the type and version of the operation you wish to carry out.

Your configuration file should resemble the following:

```
{
    "operation": {
        "type": "migration",
        "version": "1"
    },
    "source": {
        "plugin_name": "PostgresPlugin",
        "host": "localhost",
        "port": 5432,
        "user": "postgres",
        "password": "mysecretpassword",
        "dbname": "postgres",
        "table_name": "pgbench_accounts"
    },
    "destination": {
        "plugin_name": "MySQLPlugin",
        "host": "localhost",
        "port": 3306,
        "user": "root",
        "password": "my-secret-pw",
        "dbname": "your_db_name",
        "table_name": "destination_table_name"
    }
}
```

In the "operation" section:

- **type**: This defines the kind of operation to be executed. The values can be "migration", "etl", or any other custom types you may introduce later on.
- **version**: This represents the version number of the operation.

**Running the ETL Process:**

1. Before you start, ensure that all plugins mentioned in the configuration are present and are compatible versions.
2. With your configuration ready, initiate the ETL process via the main entry point, `main.py`:

```
$ python main.py path_to_your_configuration_file.json
```

Make sure to replace `path_to_your_configuration_file.json` with the precise path to your JSON configuration file.

Executing this command initializes the ETL process. It uses the stated plugins to extract data from the designated source, possibly undergoes a transformation, and eventually loads it to the target destination.