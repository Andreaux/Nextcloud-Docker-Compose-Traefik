# nextcloud-docker-compose

This is my Nextcloud docker-compose (almost) "all-in-one" template.

The stack features separate containers for:
- mariadb
- nextcloud
- nextcloud cron jobs

The stack also includes minimal healthcheck for mariadb to make sure the DB is available before the other containers are started.

Configuration for Nextcloud and the DB are mapped from local folders in /mnt (mounted remotely from my TrueNAS box using NFS). You can easily change the mount path through environment variables to suit your installation.

The stack is flavoured to be used along with traefik acting as proxy and issuing SSL certificates.

This docker-compose file doesn't contain traefik. The traefik labels might need adjusting to fit your environment.

This template is provided as-is with no pretention as for its usefulness or accuracy. I provide no support, but am open to suggestions or corrections. Bear in mind that I'm still learning docker and docker-compose so there's no guarantee I haven't made errors in there although this installation works fine since a few weeks now.
