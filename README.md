## Overview

HTTPS local certificate with:
Keycloak 18 + custom theme approach + Mysql + Traefik
(KC-X / Quarkus implementation)

Everything under a docker-compose with traefik reverse proxy
The recipe includes custom domain with https certificate

## Explanation

While doing a docker-compose it just compiles the theme, generating the jar file and integrating it


## How to execute:

- Install mkcert.
- Edit your host to use the provided certificates, with the following:

```
$ sudo nano /etc/hosts
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
127.0.0.1       dev.test
127.0.0.1       dev.kc
$ cd docker/certs
$ mkcert -install
#or as an example, execute:
$ mkcert -cert-file dev.test.crt -key-file dev.test.key dev.test localhost 127.0.0.1 ::1
```

When you can reach your localhost with the provided domains, start the container with Traefik holding the certificates

- Execute:
> docker-compose up -d --build

Wait 30 seconds to initialize and check:

Check traefik domain status at:
- http://localhost:8079/dashboard/#/http/routers

Check custom containers at:
- https://dev.test > shows basic https
- https://dev.kc   > main admin panel for KC18

Theme modifications:

- After accessing KC admin panel with admin/admin, go to settings and chose the my-custom-theme option
- Log out
- Log in to see changes