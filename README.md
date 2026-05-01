# kanidm_rootless

This is an example kanidm deployment for a rootless Docker setup, where the user running the Docker daemon is 1000:1000. "example.com" and "idm.example.com" should be replaced with your own domain and subdomain in the Caddyfile and .env file.

The vol_init container will run as root inside the container, setting 1000:1000 as the owner of relevant directories inside the named Docker volumes kanidm will use and adjusting the permissions according to the Security Hardening section (5.4) of the kanidm book. Permissions adjustments for server.toml are ommitted, instead I've used environment variables for configuration to keep as much in the compose file as possible.

I intend to extend this with a zerobyte container to back up kanidm's own backups to a remote host. kanidm's guidelines recommend not hosting other services on the domain used for identity, but ideally the zerobyte container will be accessed only locally, or even better, configured with backup target and destintation declaratively and not accessed at all.