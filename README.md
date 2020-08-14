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

After all containers are ready DR ONE should be available at
https://localhost:10101/dr/web.

## Run DR ONE with Keycloak authentication

Note that this configuration uses predefined administrative user.

To enable Keycloak driven authentication in DR ONE, the `DR_AUTH` variable
should be set to the string `keycloak`.

In bash/sh you can run the following command:

```
DR_AUTH=keycloak docker-compose up
```

In `cmd` you need to have a separate command to set environment:

```
set DR_AUTH=keycloak
docker-compose up
```

Keycloak service will be configured with administrative user `admin` having
password `admin`. Keycloak administrative console can be accessed at
`https://auth.localhost.localdomain:8443/admin`. When it is up and running at
least one user should be created in the `Drone` realm so it would be possible to
use it to access DR ONE.

DR ONE should be accessible at `https://dr-one.localhost.localdomain:10101/dr/web`.
