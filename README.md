# Docker Compose for Wildfly (running CABLES Service) + Postgres

## Running instructions

Insert your LDAP CREDENTIALS in the following file: env-vars/rbac-wildfly-vars.env

    LDAP_CREDENTIALS=<INSERT_YOUR_LDAP_CREDENTIALS_HERE>

Start service

	docker-compose up -d

The REST interface should be available at:

	http://localhost:8086

## Systemd Integration

To integrate this as a systemd service, do:

    make install

To remove the systemd service and its additional files:

    make uninstall

## Host IP mapping

The RBAC/Cable images have the following names:

  - RBAC management studio: sirius-rbac.lnls.br
  - RBAC auth services: sirius-rbac-auth.lnls.br
  - Naming service: sirius-ns.lnls.br

If running on the same host, with the same
docker network, the mapping must be the internal
docker IP, such as 172.18.0.3. This is necessary
as the port mapping between the container/host
might change and the docker DNS services knows
how to deal with this. If running on the same,
but the actual IP is used, the docker DNS service
will not be used and the services will try to
use the actual specified port, which could be
incorrect due to container/host port mapping.

So, in summary, if running services on the same
host, use

  extra_hosts:
    - "sirius-rbac.lnls.br:172.18.0.3"
    - "sirius-rbac-auth.lnls.br:172.18.0.4"
    - "sirius-ns.lnls.br:172.18.0.6"

where 172.18.0.3/172.18.0.4/172.18.0.6 are the internal
docker IPs

If running the services on different host, just use
the destination IPs.
