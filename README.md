# cas-overlay

This repository is an Apereo CAS overlay project built with Maven and packaged as a WAR for a Tomcat-based CAS server.

## Project overview

The project provides a customized CAS deployment layer on top of the Apereo CAS server stack. Configuration, service definitions, and web resources are kept under the overlay structure so the deployment can be adapted without changing the upstream server artifacts directly.

## Development principles

- Keep customization inside the overlay layout under src/main/resources, src/main/resources/services, and src/main/webapp.
- Do not commit secrets, keystore paths, LDAP credentials, or other environment-specific values.
- Validate authentication, LDAP, TLS, ticketing, and service-registry changes against the current CAS configuration before shipping.
- Use Maven verification as the standard completion check for repository changes.

## Prerequisites

- Java 25
- Maven 3.9+

## Build

Build the WAR artifact with:

```bash
mvn -DskipTests package
```

The build output is generated under the target directory, including the packaged WAR artifact for deployment.

## Run locally

The default runtime configuration is defined in [src/main/resources/application.properties](src/main/resources/application.properties). The application is configured to run under the CAS context path and uses HTTPS on port 9443 by default.

For local development, deploy the generated WAR to a servlet container such as Tomcat, or use the CAS web application entry point with the project configuration applied.

## Project structure

- [pom.xml](pom.xml) — Maven build definition and dependency management
- [src/main/resources](src/main/resources) — CAS configuration and runtime resources
- [src/main/resources/services](src/main/resources/services) — sample JSON service definitions
- [src/main/webapp](src/main/webapp) — web assets and overlay resources

## Important notes

- Keep environment-specific values such as keystore paths, LDAP credentials, and secrets out of committed files.
- Authentication, LDAP, TLS, and service registry changes should be validated against the existing CAS configuration before shipping.
- The sample service definitions in [src/main/resources/services](src/main/resources/services) are useful references when changing service registration behavior.
