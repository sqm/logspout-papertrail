# logspout-papertrail

Logspout is a log router for Docker containers that run inside Docker. This repo creates a papertrail specific images when using the TLS logspout adapter.
This image could still be used with the UDP and TCP adapters to any syslog server.  Any secure (TLS) transport protocol will only be available to talk to papertrail.

## Getting logspout-papertrail

```
docker pull squaremouth/logspout-papertrail
```

## Using logspout-papertrail

#### Route all container output to remote syslog
The simplest way to use logspout-papertrail is to just take all logs and
ship to a remote syslog.  Just pass a syslog URI (or several comma
separated URIs) as the command.  Also, we always mount the Docker Unix
socket with `-v` to `/tmp/docker.sock`:

```
docker run --name="logspout" \
  --volume=/var/run/docker.sock:/tmp/docker.sock \
  -e 'SYSLOG_HOSTNAME=node.example.com' \
  squaremouth/logspout-papertrail \
  syslog+tls://logs.papertrailapp.com:55555
```
