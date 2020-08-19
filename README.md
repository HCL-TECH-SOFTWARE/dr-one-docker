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

This configuration assumes that the localhost is available as
`auth.localhost.localdomain` and `dr-one.localhost.localdomain`. If it is not,
you can add these entries to your `hosts` file.

To enable Keycloak driven authentication in DR ONE, the `DR_AUTH` variable
should be set to the string `keycloak`.

In bash/sh you can run the following command:

```
DR_AUTH=keycloak docker-compose up
```

On Windows you would also need to allow file sharing. 
- Right-click on the Docker Desktop icon in the taskbar -> Settings -> Resources -> File Sharing
- Add a folder where you checked out files from this repository to the list.
Then run the following commands in `cmd`

```
set DR_AUTH=keycloak
docker-compose up
```

Keycloak service will be configured with administrative user `admin` having
password `admin`. Keycloak administrative console can be accessed at
`https://auth.localhost.localdomain:8443/auth`. When it is up and running you would need to create users in `Drone` realm and assign them roles to manage design access. See chapter Creating Users in [Authentication Setup](https://www.devops-community.com/uploads/1/0/2/7/102707030/authentication_setup.2020.26.pdf) document.
DR ONE should be accessible at `https://dr-one.localhost.localdomain:10101/dr/web`.
