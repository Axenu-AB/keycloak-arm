# Keycloak Docker image

This is a fork of mihaibob/keycloak

## Available Keycloak versions

*Starting with version 15.0.1 of Keycloak, only ARM 64 is supported by this repo*

## Tags
15.1.0 => keycloak 15.1.0
16.1.1 => keycloak 16.1.1

## How the image is build

For ARM 64 the default image as shipped by Keycloak are used, no modifications are made.

For ARM version, this image uses the official Keycloak [repository](https://github.com/keycloak/keycloak-containers) that is used to build the official Keycloak image. The only difference is that the Dockerfile used to build the official version of Keycloak is changed with the one from [this](https://github.com/Mihai-B/keycloak-arm) repository and the image is build on a Raspberry Pi 3 (32 bit)

The docker image has to be changed when building the ARM version of Keycloak because the base image that is used by Keycloak does not support ARM processors thus it is swapped with Ubuntu as base image


## How to use

### Quick start Keycloak using MySql/MariaDb

#### First run
```
docker run -p 9877:8080 --name keycloak -e KEYCLOAK_USER=<ADMIN_USERNAME> -e KEYCLOAK_PASSWORD=<ADMIN_PASS>  -e DB_VENDOR=<DB_VENDOR> -e DB_ADDR=<DB_ADDRESS> -e DB_DATABASE=<DATABASE_NAME> -e DB_USER=<DATABASE_USER> -e DB_PASSWORD=<DATABASE_PASS> -e JDBC_PARAMS: "serverTimezone=UTC" mihaibob/keycloak:<KEYCLOAK_VERSION>
```

In this example Keycloak will be available on port 9877. <br>
The variables need to be changed acordingly: <br>
`ADMIN_USERNAME` - the username you want to use for Keycloak's admin user <br>
`ADMIN_PASS` - the password for Keycloak's admin user <br>
`DB_VENDOR` - the database vendor, can be any of: h2, mysql, mariadb, postgres, oracle, mssql <br>
`DB_ADDRESS` - where the database can be accessed, example: 192.168.1.10. Do not use 'localhost' even if the database is on the same board <br>
`DATABASE_NAME` - the database keycloak should create the tables in(make sure the database is allready created) <br>
`DATABASE_USER` - the user that keycloak should use to access the database <br>
`DATABASE_PASS` - the password keycloak should use to access the database <br>
`KEYCLOAK_VERSION` - the Keycloak version to run

#### Upgrading Keycloak container to a later version

After Keycloak was run using the 'First run' command, and an upgrade is in order then the command to start Keycloak should look like this:
```
docker run -p 9877:8080 -d --name keycloak -e DB_VENDOR=mysql -e DB_ADDR=<DB_ADDRESS> -e DB_DATABASE=<DATABASE_NAME> -e DB_USER=<DATABASE_USER> -e DB_PASSWORD=<DATABASE_PASS> -e JDBC_PARAMS: "serverTimezone=UTC" mihaibob/keycloak:<KEYCLOAK_VERSION>
```

Notice we did not specify the 'KEYCLOAK_USER' and 'KEYCLOAK_PASSWORD' since they are saved in the database now

## Full documentation 
For a complete documentation refer to Keycloak's official documentation on how to configure the docker container because the process is exactly the same. The documentation can be found [here](https://hub.docker.com/r/jboss/keycloak).
