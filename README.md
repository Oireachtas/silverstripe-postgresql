# PostgreSQL Module Module

[![CI](https://github.com/silverstripe/silverstripe-postgresql/actions/workflows/ci.yml/badge.svg)](https://github.com/silverstripe/silverstripe-postgresql/actions/workflows/ci.yml)

## Installation

```sh
composer require silverstripe/postgresql
```

## Configuration

### Environment file

Add the following settings to your `.env` file:

```
SS_DATABASE_CLASS=PostgreSQLDatabase
SS_DATABASE_USERNAME=
SS_DATABASE_PASSWORD=
```

See [environment variables](https://docs.silverstripe.org/en/getting_started/environment_management) for more details. Note that a database will automatically be created via `dev/build`.

### Through the installer

Open the installer by browsing to install.php, e.g. http://localhost/install.php
Select PostgreSQL in the database list and enter your database details

## Usage Overview

See [docs/en](docs/en/README.md) for more information about configuring the module.
	
## Known issues

All column and table names must be double-quoted.  PostgreSQL automatically 
lower-cases columns, and your queries will fail if you don't.

Collations have known issues when installed on Alpine, MacOS X and BSD derivatives
(see [PostgreSQL FAQ](https://wiki.postgresql.org/wiki/FAQ#Why_do_my_strings_sort_incorrectly.3F)).
We do not support such installations, although they still may work correctly for you.
As a workaround for PostgreSQL 10+ you could manually switch to ICU collations (e.g. und-x-icu).
There are no known workarounds for PostgreSQL <10.

Ts_vector columns are not automatically detected by the built-in search 
filters.  That means if you're doing a search through the CMS on a ModelAdmin
object, it will use LIKE queries which are very slow.  If you're writing your 
own front-end search system, you can specify the columns to use for search 
purposes, and you get the full benefits of T-Search.

If you are using unsupported modules, there may be instances of MySQL-specific 
SQL queries which will need to be made database-agnostic where possible.
