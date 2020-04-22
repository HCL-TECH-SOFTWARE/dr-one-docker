# DR ONE in Docker

Docker compose file that allows to run DR ONE optionally with Keycloak
authentication. Includes a script for automated Keycloak configuration.

The `docker-compose.yaml` defines 3 services:
- `dr-one` for DR ONE
- `db` for MongoDB
- `auth` for Keycloak

## Run DR ONE without authentication

Just start `dr-one` service with `docker-compose`:

    docker-compose up dr-one

## Run DR ONE with Keycloak authentication

Please note that this configuration uses predefined names, passwords and
secrets.

Also currently DR ONE uses Keycloak's cli-admin client to perform access control
for designs, which is potential risk.

And finally for now the Keycloak service should be accessible via `auth`
name.

Before DR ONE can be started, Keycloak service should be started and configured
first:

    docker-compose up auth

As soon as Keycloak is up and running (look for `Keycloak started` in the log)
execute the configuration script in its container:

    docker-compose exec auth config-kc-for-dr-one

When it is finished, bring up the DR ONE container specifying authentication
mode for it:

    DR_AUTH=keycloak docker-compose up dr-one

