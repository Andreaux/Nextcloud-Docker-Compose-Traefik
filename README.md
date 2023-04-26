# Nextcloud docker-compose template with MariaDB and Cron jobs with traefik labels

This is my Nextcloud docker-compose (almost) "all-in-one" template.

The stack features separate containers for:
- mariadb
- nextcloud
- nextcloud cron jobs

The stack also includes minimal healthcheck for mariadb to make sure the DB is available before the other containers are started.

Configuration for Nextcloud and the DB are mapped from local folders in /mnt (mounted remotely from my TrueNAS box using NFS). You can easily change the mount path through environment variables to suit your installation.

The stack is flavoured to be used along with traefik acting as proxy and issuing SSL certificates.

This docker-compose file doesn't contain traefik. The traefik labels might need adjusting to fit your environment.

## Note about deploying the stack with no pre-existing Nextcloud DB

This template was created along an existing Nextcloud DB. For the first run, you might need to comment out the healthcheck part for the mariadb container as it checks for a database called 'nextcloud' which at that stage obviously doesn't exist yet. I'm unsure how the stack would start absent that DB. Let me know if you have success deploying this stack without a pre-existing Nextcloud DB while not removing the healthcheck.

## Disclaimer

This template is provided as-is with no pretention as for its usefulness or accuracy. I provide no support, but am open to suggestions or corrections. Bear in mind that I'm still learning docker and docker-compose so there's no guarantee I haven't made errors in there although this installation works fine since a few weeks now.
