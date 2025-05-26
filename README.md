# PostgreSQL setup for Arch Linux

## Install postgreSQL

`sudo pacman -S postgresql`

- Check Status and enable
- Enable and start PostgreSQL service:

`sudo systemctl enable postgresql
sudo systemctl start postgresql
sudo systemctl status postgresql
`

Create database user and password

CREATE DATABASE <Database name>;
CREATE USER <your user name> WITH PASSWORD '<your password>';
GRANT ALL PRIVILEGES ON DATABASE <Database name> TO <your user name>;

After installation:

sudo -u postgres psql // for postgresql login command

Create a new URI on terminal:

# CREATE USER myuser WITH PASSWORD 'mypassword';

# CREATE DATABASE mydb OWNER myuser;

# GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;

# postgresql://<username>:<password>@<host>:<port>/<database>

**\*\*\*\***\*\*\***\*\*\*\***MOST IMPORTANT FOR CREATE\***\*\*\*\*\***\*\*\***\*\*\*\*\***
CREATE USER gql WITH PASSWORD 'gqlpass';
CREATE DATABASE gqldb OWNER gql;
GRANT ALL PRIVILEGES ON DATABASE gqldb TO gql;

ALTER USER gql CREATEDB;

# postgresql://gql:gqlpass@localhost:5432/gqldb

After must have need to permissions

# sudo -u postgres psql // for postgresql login command

# ALTER USER projects CREATEDB; // here is "projects" is project name

# You should see: ALTER ROLE

Some command for access database

# logout: \q

# check list: \l

# switch database: \c <database name>

# check database relations: \dt

# Query All Users: SELECT \* FROM "users";

# Get all user: \du

After migration prisma

# npx prisma migrate dev --name init
