## General
Docker Compose project for Grafana Cloud integration for sch.gr RADIUS and LDAP services. Includes the following components:
- FreeRADIUS Prometheus Exporter (leveraging FreeRADIUS status server)
- OpenLDAP Prometheus Exporter (leveraging OpenLDAP monitor bacjend)
- FreeRADIUS promtail to send logs to Loki/Grafana Cloud (reads a special JSON file)
- Grafana Agent to forward FreeeRADIUS metrics to Grafana Cloud
- Grafana Agent to forward OpenLDAP metrics to Grafana Cloud

## Commands
* There are separate directories and docker-compose.yaml files for RADIUS and LDAP services
* Installation: `docker-compose up -d`
* Restart after changes in files:
  - `docker-compose stop`
  - `docker-compose rm`
  - `docker-compose up -d`
* Logs:
  - For all: `docker-compose logs`
  - For specific instance: `docker-compose logs <instance>`
* ps: `docker-compose ps`

## Environment
Relevant environment variables:
* LOKI_URI: The Loki URI to push logs
* GRAFANA_URI: The Grafana Cloud URI to push logs
* LOKI_USER/GRAFANA_USER: Usernames for authentication to Loki/Grafana Cloud
* LOKI_PASS/GRAFANA_Pass: Passwords

## Labels
Main Labels:
* Loki RADIUS:
   - agent: sch-radius
   - job: schradiuslogs
   - radhost: ${RADIUS}
   - status: accept|reject
   - username
   - nas
   - cid (Caller-Id)
 * Grafana RADIUS:
    - agent: sch-radius
    - job: schradiusmetrics
    - radhost: ${RADIUS}
 * Grafana LDAP:
     - agent: sch-ldap
     - job: schldapmetrics
     - ldaphost: ${LDAP}
