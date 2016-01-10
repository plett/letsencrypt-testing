#Experimenting with letsencrypt

letsencrypt is an awesome project, but I don't like the concept of automated
tools making changes to my web server config, so I threw together a
docker-compose setup to allow the letsencrpt client run independently of any
other services.

I'm also taking this opportunity to play with the new 
[Docker 1.9 networking](https://blog.docker.com/2015/11/docker-multi-host-networking-ga/)
which I hadn't used before.

It is a haproxy front end container which terminates the ssl (using the
letsencrypt cert, of course) and passes plain http traffic on to an nginx
container. Any authentication requests for getting/renewing a letsencrypt cert
is split off by haproxy and sent to a different container. The --webroot option
to the letsencrypt client has made this a lot simpler.

This is hardcoded for my plett.uk domain which I was using for testing during
the letsencrypt closed beta.
