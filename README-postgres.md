# PostgreSQL Installation and Setup

### PostgreSQL Installation

1. Install dependencies:
```bash
# Install PostgreSQL
brew install postgresql@15

# Start PostgreSQL service
brew services start postgresql@15

# Install pgAdmin (GUI)
brew install --cask pgadmin4

# Install project dependencies
npm install
```

2. Configure PostgreSQL:
```bash
# Verify PostgreSQL is running
psql postgres

# Create database
createdb prompt_resp_db

# Create user (optional)
createuser --interactive --pwprompt

# Connect to database
psql prompt_resp_db
```

3. Configure environment variables in `.env` file:
```
DATABASE_URL=postgres://username:password@localhost:5432/prompt_resp_db
PORT=3000
JWT_SECRET=your_jwt_secret
```

4. Seed the database with initial data:
```bash
node movie_api/postgres/utils/seedDatabase.js
```
or
```bash
npm run seed:postgres
```

5. Start the server:
```bash
node movie_api/postgres/server.js
```

6. Open pgAdmin and connect to the database:
- Add New Server
- Name: Local PostgreSQL
- Host: localhost
- Port: 5432
- Username: your_username
- Password: your_password

### PostgreSQL Cloud Setup (AWS RDS)

1. Create AWS RDS PostgreSQL instance:
- Visit [AWS RDS Console](https://console.aws.amazon.com/rds)
- Create database
- Select PostgreSQL
- Choose free tier if available
- Configure security settings

2. Configure RDS Connection:
- Create a database user
- Configure security groups to allow your IP
- Get your connection string
- Replace `DATABASE_URL` in `.env` with RDS connection string

3. Connect with pgAdmin:
- Add New Server
- Enter RDS endpoint, port, username, and password
- Connect

### Common PostgreSQL Shell Commands

```bash
# Connect to PostgreSQL
psql postgres

# List all databases
\l

# Connect to database
\c prompt_resp_db

# List all tables
\dt

# Describe table
\d table_name

# Execute SQL query
SELECT * FROM movies;
SELECT * FROM users;

# Count records
SELECT COUNT(*) FROM movies;

# Find specific record
SELECT * FROM movies WHERE title = 'Movie Title';

# Exit PostgreSQL shell
\q
```

### Essential PostgreSQL CLI Commands

# Database Operations
```bash
# Start PostgreSQL shell
psql postgres

# Show PostgreSQL version
psql --version

# Create database
createdb database_name

# Drop database
dropdb database_name

# List all databases
\l

# Connect to database
\c database_name

# Show database stats
\l+ database_name
```

# Table Operations
```bash
# List tables
\dt

# Describe table
\d table_name

# Create table
CREATE TABLE table_name (
  id SERIAL PRIMARY KEY,
  field VARCHAR(255) NOT NULL
);

# Drop table
DROP TABLE table_name;

# Rename table
ALTER TABLE table_name RENAME TO new_name;
```

# CRUD Operations
```bash
# Insert record
INSERT INTO table_name (field) VALUES ('value');

# Insert multiple records
INSERT INTO table_name (field) VALUES 
  ('value1'),
  ('value2');

# Select all records
SELECT * FROM table_name;

# Select with specific criteria
SELECT * FROM table_name WHERE field = 'value';

# Select one record
SELECT * FROM table_name WHERE field = 'value' LIMIT 1;

# Update record
UPDATE table_name
SET new_field = 'new_value'
WHERE field = 'value';

# Delete record
DELETE FROM table_name WHERE field = 'value';
```

# Query Operations
```bash
# Count records
SELECT COUNT(*) FROM table_name;

# Limit results
SELECT * FROM table_name LIMIT 5;

# Offset results
SELECT * FROM table_name OFFSET 5;

# Sort results
SELECT * FROM table_name ORDER BY field ASC;

# Find distinct values
SELECT DISTINCT field FROM table_name;

# Complex query with multiple conditions
SELECT * FROM table_name
WHERE field1 = 'value1'
AND field2 > 100
AND field3 IN ('a', 'b', 'c');
```

# Index Operations
```bash
# Create index
CREATE INDEX idx_name ON table_name(field);

# List indexes
\di

# Drop index
DROP INDEX idx_name;
```

# User Management
```bash
# Create user
CREATE USER username WITH PASSWORD 'password';

# Grant privileges
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;

# List users
\du

# Drop user
DROP USER username;
```

# Backup and Restore
```bash
# Backup database (from terminal)
pg_dump database_name > backup_file.sql

# Restore database (from terminal)
psql database_name < backup_file.sql
```

### Project Dependencies

- pg: PostgreSQL client
- sequelize: ORM for PostgreSQL
- dotenv: Environment variable management

---
