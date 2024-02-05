Stack version 2.0

# WARNING!
Previous versions of this stack use MariaDB. For this version, I transitioned to Postgres. If you are using a previous version of this stack, be aware that you will loose DB contents if you deploy this new stack.

# Nextcloud docker-compose template with Postgres, Redis, Collabora CODE and Cron jobs with Traefik labels

This is my Nextcloud Docker-Compose "all-in-one" template.

The stack features separate containers for:
- postgres (postgres:latest)
- redis (redis:alpine)
- nextcloud (nextcloud:latest)
- collabora (collabora/code:latest)
- nextcloud cron jobs (rcdailey/nextcloud-cronjob:latest)

The stack also includes dependencies to make sure the DB and Memcache (Redis) are available before the other containers are started.

Configuration for Nextcloud and the DB are mapped from within the docker-compose file (mounted remotely from my TrueNAS box using NFS). You can of course change the mount method and path to suit your installation.

My Home Lab runs an Ubuntu Virtual Machine to host my Docker Projects that runs Traefik as a reverse proxy and Portainer to manage Stacks and Containers so this stack is flavoured to be used along with traefik acting as proxy and issuing SSL certificates through Cloudflare (a free account totally works which will enable a free wildcard certificate for all your local hosts as well).

NOTE:
This docker-compose file doesn't contain Traefik and Portainer, you will need to get it up and running separately (I am hosting docker-compose files for those too).
The traefik labels might need adjusting to fit your environment.

## Environment variables

Docker Compose will need environment variables set. I have included an example .env file to make what is expected there easier to understand.

If you use Portainer, you will have to set these within Portainer (Advanced mode is easier as you just need to copy-paste the contents of the .env file) when creating the Nextcloud stack after you've pasted the docker-compose.yml file into Portainer. If you use "docker-compose" to bring up the stack, the .env file should be picked up automatically so fill in your information in there.

## Traefik

My Home Lab runs an Ubuntu Virtual Machine to host my Docker Projects which runs Traefik as a reverse proxy. The reverse proxy is needed to be able to provide all internal services with an SSL certificate and be able to use all services without needing to write port numbers in URLs. I found the easiest for me was to use Cloudflare and get SSL certificates through Cloudflare. A free Cloudflare account is more than enough to achieve this. While you can deploy this Stack without Traefik, you would have to set up SSL certificates for each service individually. Traefik makes this otherwise tedious process effortless.

If you need to set up Traefik and/or Portainer, check out my Traefik-Docker-Compose package here: https://github.com/Andreaux/Traefik-Docker-Compose or my Portainer-Docker-Compose package (*coming soon*).

## Support this project

If you find this useful, a coffee through Ko-Fi is all it takes to make me happy <3 (I love coffee :D) Click the Sponsor button on the top of this page or visit https://ko-fi.com/andreaux to buy me a coffee.

## Disclaimer

This template is provided as-is with no pretention as for its usefulness or accuracy. I provide no support, but am open to comments, suggestions or corrections (please do!). Bear in mind that I'm still learning docker and docker-compose so there's no guarantee I haven't made errors in there although this installation works fine since a few months now.
