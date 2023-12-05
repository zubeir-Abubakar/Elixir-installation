# ![https://elixir-lang.org/](/elixir-lang-ar21.svg)

## Installation

* Install Elixir and Erlang
* Install Postgres
* Install dependencies
* Set up DB
* Set environment variables
* Run the server

### Install Elixir and Erlang

> It is recommended to use asdf for managing elixir and erlang version for the development

Install asdf http://asdf-vm.com/guide/getting-started.html

* `asdf plugin-add erlang && asdf plugin-add elixir`

* `asdf install`

> Version is defined in `.tool-versions`

### Install Postgres

> Use postgres 12 or higher

* **Ubuntu**: `sudo apt-get install postgresql`
* **MacOS**: `brew install postgresql`

### Install dependencies and Configure DB

* run `bin/setup`, which:
    - creates `dev.secret.exs` (if not exists)
    - creates `.env` (if not exists)
    - clears directories with auto-generated files: 
        - `./_build` (compiled elixir source code)
        - `./deps` (elixir dependencies)
        - `./bin/temp` (staging database dumps)
    - Fetches dependencies
    - Drops existing database
    - Creates new database, runs migrations and seeds data

Default setting will assume that you have postgres running on the default port with `postgres`/`postgres` user/password pair. If you don't you can change it by editing `dev.secret.exs`:

## Usage

* Start Phoenix endpoint with `bin/server`

This server is a GraphQL API which is available at: [`localhost:4000/graphql`](http://localhost:4000/graphql)

## Cloning the staging database
a good use case for tool would be cloning the staging database and running migrations against it; ensuring they're working (as expected) before merging one's pull request.

* Ensure your `.env` file has the correct credentials.  
* Your technical lead should provide you with correct values especially for `REMOTE_DB_PASSWORD=cloudsql_proxy_hosted_db_password`  

* run `bin/db/clone`, which:
    - connects to cloud sql proxy
    - dumps the staging database
    - imports the dump to your local database, thereby cloning the staging environment data for your development and alpha testing convenience.   

### Open to improvements / feedback
* feel free to peruse the helper scripts under `bin/*` and submit a PR with improvements... 
* Or if you're just curious :)