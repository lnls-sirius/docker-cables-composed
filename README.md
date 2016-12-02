# Docker Compose for Wildfly (running CABLES Service) + Postgres

## Running instructions

	docker-compose up -d

The REST interface should be available at:

	http://localhost:8086

## Systemd Integration

To integrate this as a systemd service, do:

    make install

To remove the systemd service and its additional files:

    make uninstall
