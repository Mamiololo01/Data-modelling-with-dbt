# Data-modelling-with-dbt
Step-by-Step for handling 1M+ dataset using dbt with Docker and Postgres as database

Procedures:

Start up Docker

Pull the postgres image from docker hub and connect with it

Running the docker instance and sends 1M+ records into dockerized db using python script.

Installing and configuring dbt core.

Begin to build models


Docker pull Postgres:latest

Docker image ls. To verify

The command to run the Postgres instance is:

'docker run -dp 5431:5432 -e "POSTGRES_PASSWORD=pass" -e "POSTGRES_USER=postgres" -v /home/postgres-target/:/var/lib/postgresql/data  -- name dbtmodeldb   postgres:latest'

Connect to the database server "Docker exec -it dbtmodeldb psql -U postgres -h localhost".  

Create database
\l to show the database
CREATE DATABASE test;
\q text to exit the database
\dn to list schema


Python file (postgres_dataloader.py) does the transformation and loading of the excel file into the postgres
run "Python postgres_dataloader.py"

Connect to database.  \c test

\d shows the schema and database

Validate that dataset is loaded to the databas, select * from  table and use count functions

Installing and configuring dbt  https://docs.getdbt.com/guides

Install with pip

python -m pip install dbt-core dbt-postgres

Then run "dbt version"  to show the version and plugins core and postgres

Now configure dbt

.dbt/profiles.yml and data added

Ensure port is 5432

Execute dbt debug shows all check/test passed

Execute " dbt run" ETL flow wrt configuration on the model folder. Schema.yml and hacker.sql under the model folder provides the layout for the modelling by dbt

Once completed, there will be more tables in the database using the "\d" command.

Alternatively on a diff folder, you can use dbt init test_dbtool and follow the prompt



