# SQL2022-Docker
Simple docker compose to have a container based sql server for various purposes

We are passing two environment variables through the environment option:

```yaml
    environment:
      - "ACCEPT_EULA=Y"
      - "MSSQL_PID=EXPRESS"   
```

- `ACCEPT_EULA=Y` - This is required to run sql server in a container.
- `MSSQL_PID=EXPRESS` - We are selecting the Express version of SQL Server which is `free` to use.

Also we need to specify the `sa` password. For that we are mapping the environment variables from the `secret.env` file. You should add this file to your `.gitignore` if sharing the docker-compose with your team using a git repository.

the instruction for the docker-compose to use the `secret.env` file is the following:

```yaml
    env_file:
      - secret.env
```

To make sure we have data persistence we are mapping the following `volumes` to our container:

```yaml
    volumes:
      - ./sql/data:/var/opt/mssql/data
      - ./sql/secrets:/var/opt/mssql/secrets
```

Most probably these files should not be committed to your repository and you should add the `sql/` folder to your `.gitignore` also.

Also the two ports used by SQL Server have been mapped:

```yaml
    ports:
      - 1433:1433/tcp
      - 1434:1434/udp
```