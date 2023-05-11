# Nextcloud docker-compose template with MariaDB, Collabora CODE and Cron jobs with traefik labels

This is my Nextcloud Docker-Compose "all-in-one" template.

The stack features separate containers for:
- mariadb (mariadb:latest)
- nextcloud (nextcloud:latest)
- collabora (collabora/code:latest)
- nextcloud cron jobs (rcdailey/nextcloud-cronjob:latest)

The stack also includes minimal healthcheck to make sure the DB is available before the other containers are started.

Configuration for Nextcloud and the DB are mapped from local folders in /mnt (mounted remotely from my TrueNAS box using NFS). You can easily change the mount path through environment variables to suit your installation.

My Home Lab runs an Ubuntu Virtual Machine to host my Docker Projects that runs Traefik as a reverse proxy and Portainer to manage Stacks and Containers so this stack is flavoured to be used along with traefik acting as proxy and issuing SSL certificates through Cloudflare (a free account totally works which will enable a free wildcard certificate for all your local hosts as well).

This docker-compose file doesn't contain traefik, you will need to get it up and running separately. The traefik labels might need adjusting to fit your environment.

## Environment variables

Docker Compose will need environment variables set. I have included examples as in-line comments to make what is expected there easier to understand.

There is a .env file included with examples for the environment variables. If you use Portainer like I do, you will have to set these within Portainer when creating the Nextcloud stack after you've pasted the docker-compose.yml file into Portainer. If you use "docker compose" to bring up the stack, the .env file should be picked up automatically so fill in your information in there.

## Deploying the stack with no pre-existing Nextcloud DB

This template was created along an existing Nextcloud DB. For the first run, you most probably need to comment out the healthcheck part for the mariadb container as it checks for a database called 'nextcloud' which at that stage obviously doesn't exist yet. I'm unsure how the stack would start absent that DB. Let me know if you have success deploying this stack without a pre-existing Nextcloud DB while not removing the healthcheck.

## Support this project

If you find this useful, a coffee through Ko-Fi is all it takes to make me happy <3 (I love coffee :D) Click the Sponsor button on the top of this page or visit https://ko-fi.com/andreaux to buy me a coffee.

## Disclaimer

This template is provided as-is with no pretention as for its usefulness or accuracy. I provide no support, but am open to suggestions or corrections. Bear in mind that I'm still learning docker and docker-compose so there's no guarantee I haven't made errors in there although this installation works fine since a few weeks now.
