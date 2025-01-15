# Data Modelling with dbt

This repository provides a step-by-step guide for handling a dataset with over 1 million records using dbt, Docker, and PostgreSQL. 

## Table of Contents
- [Introduction](#introduction)
- [Requirements](#requirements)
- [Setup](#setup)
  - [Docker and PostgreSQL](#docker-and-postgresql)
  - [Python Data Loader](#python-data-loader)
  - [dbt Installation and Configuration](#dbt-installation-and-configuration)
- [Data Modelling with dbt](#data-modelling-with-dbt)
- [Validation](#validation)
- [Resources](#resources)
- [License](#license)

## Introduction
This guide demonstrates how to set up a local environment using Docker, load a large dataset into PostgreSQL, and use dbt (data build tool) for data transformation and modelling.

## Requirements
- Docker
- Python 3.x
- dbt Core
- PostgreSQL

## Setup

### Docker and PostgreSQL

1. **Start Docker**:
   Ensure Docker is running on your system.

 **Pull PostgreSQL Image**:
   docker pull postgres:latest	
   Verify Docker Image: docker image ls

2. Run PostgreSQL Instance: docker run -dp 5431:5432 -e "POSTGRES_PASSWORD=pass" -e "POSTGRES_USER=postgres" -v /home/postgres-target/:/var/lib/postgresql/data --name dbtmodeldb postgres:latest 
The /home/postgres-target directory ensures that the configuration on the local system is retained even if the image is removed.

3. Connect to PostgreSQL: docker exec -it dbtmodeldb psql -U postgres -h localhost

4. Create Database: 
CREATE DATABASE test;
 \l -- List databases
 \q -- Exit PostgreSQL

Python Data Loader
1. Transform and Load Data:
    * Use the provided Python script (postgres_dataloader.py) to transform and load the dataset into PostgreSQL.
    * Run the script:shpython postgres_dataloader.py
2. Verify Data Load:
    * Connect to the test database: 
    \c test
    \d -- Show schema and tables
    * Validate that the dataset is loaded:
    SELECT COUNT(*) FROM your_table;

dbt Installation and Configuration
1. Install dbt Core and dbt-Postgres:
   python -m pip install dbt-core dbt-postgres

2. Verify Installation:
   dbt --version

3. Configure dbt:
    * Create a profiles.yml file in the .dbt directory with the necessary configuration.
    * Ensure the PostgreSQL port is set to 5432.

4. Debug Configuration:
   dbt debug

Data Modelling with dbt

1. Run dbt: dbt run
This executes the ETL flow based on the configuration in the models folder. The schema.yml and hacker.sql files provide the layout for the modelling.

2. Check New Tables:
    * Verify the new tables in the database:
    \d
3. Alternative Initialization:
    * You can also initialize a new dbt project:
    dbt init test_dbtool
    * Follow the prompts to set up the project.

Validation:
   Verify Data:
    * Use SQL queries to validate the transformed data in the new tables created by dbt.

Resources:
* dbt Documentation
* Docker Documentation
* PostgreSQL Documentation

License:  This project is licensed under the MIT License - see the LICENSE file for details.

Feel free to open an issue or contact the maintainers if you have any questions or need assistance.

Happy coding!!


