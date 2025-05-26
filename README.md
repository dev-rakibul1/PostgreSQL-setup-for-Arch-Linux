# PostgreSQL setup for Arch Linux

## Install PostgreSQL

`sudo pacman -S postgresql`

- Check Status and enable
- Enable and start PostgreSQL service:

`sudo systemctl enable postgresql`
`sudo systemctl start postgresql`
`sudo systemctl status postgresql`

## Create database user and password

<pre><code>
CREATE DATABASE <Database name>;
CREATE USER <your user name> WITH PASSWORD '<your password>';
GRANT ALL PRIVILEGES ON DATABASE <Database name> TO <your user name>;
</code></pre>

## After installation:

<p> // for postgresql login command</p>

`sudo -u postgres psql`

## Create a new URI on terminal:

<pre>
<code>

CREATE USER myuser WITH PASSWORD 'mypassword';
CREATE DATABASE mydb OWNER myuser;
GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;

<p>PostgreSQL Connection URI:</p> 
postgresql://myuser:mypassword@localhost:5432/mydb

</code>
</pre>

**\*\*\*\***\*\*\***\*\*\*\***MOST IMPORTANT FOR CREATE\***\*\*\*\*\***\*\*\***\*\*\*\*\***

<pre>
<code>

CREATE USER gql WITH PASSWORD 'gqlpass';
CREATE DATABASE gqldb OWNER gql;
GRANT ALL PRIVILEGES ON DATABASE gqldb TO gql;

ALTER USER gql CREATEDB;

</code>
</pre>

`postgresql://gql:gqlpass@localhost:5432/gqldb`

## After must have need to permissions

- sudo -u postgres psql // for postgresql login command
- ALTER USER projects CREATEDB; // here is "projects" is project name
- You should see: ALTER ROLE

## Some command for access database

- logout: \q
- check list: \l
- switch database: \c <database name>
- check database relations: \dt
- Query All Users: SELECT \* FROM "users";
- Get all user: \du
- Single user check: \du user_2
- Access privileges: \z

## After migration prisma

`npx prisma migrate dev --name init`

## If you are logged in as a superuser (for example, postgres or rakibul), you can reset the password for the gql user like this:

`ALTER USER gql WITH PASSWORD 'new_password_here';`

<p>Replace 'new_password_here' with the new password you want to set.</p>

## Important:

    - You cannot view the existing password because PostgreSQL stores passwords in a secure hashed form.
    - You can only reset the password by setting a new one.
    - To check which users are superusers, use the \du command in psql.
    - Superusers have attributes like:
        - Superuser, Create role, Create DB etc.

## To replace to user name and must have supperuser permissions

`ALTER ROLE db_2 RENAME TO user_2;`

## Database user permission role

`ALTER USER user_2 WITH SUPERUSER;`

<p>For all permissions commands:</p>

`ALTER USER user_2 WITH SUPERUSER CREATEROLE CREATEDB REPLICATION BYPASSRLS;`

## For remove permissions: only wrie 'NO' like:

`ALTER USER user_2 WITH NOSUPERUSER NOCREATEROLE NOCREATEDB NOREPLICATION NOBYPASSRLS;`

## Delete user, database and password

<pre>
| Work                       | Command                                           |
| -------------------------- | --------------------------------------------      | 
| User delete                | `DROP USER user_2;`                               |
| Database delete            | `DROP DATABASE db_2;`                             |
| Password replace/remove    | `ALTER USER user_2 WITH PASSWORD 'newpass/null';` |
</pre>
