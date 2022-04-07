# Kubernetes ConfigMap Reload - Zitified

Forked from the excellent repository over at https://github.com/jimmidyson/configmap-reload. This is a "zitified" 
version of that program. The main difference is that this program will require the container to have a ziti identity 
located at /run/secrets/ziti.identity.json which will be used to provoke the target to reload. The target is 
specified by supplying the "webhook-url" using a format that follows this convention:

    https://serivceNameHere:portDoesNotMatter

## About
**configmap-reload** is a simple binary to trigger a reload when Kubernetes ConfigMaps are updated.
It watches mounted volume dirs and notifies the target process that the config map has been changed.
It currently only supports sending an HTTP request, but in future it is expected to support sending OS
(e.g. SIGHUP) once Kubernetes supports pod PID namespaces.

It is available as a Docker image at https://hub.docker.com/r/openziti/configmap-reloadz

### Rebuilding the Docker Image

First build the project by running `make docker`

Once built, push the container to docker hub: `docker push openziti/configmap-reloadz:latest-amd64`

### Usage

```
Usage of ./out/configmap-reload:
  -volume-dir value
        the config map volume directory to watch for updates; may be used multiple times
  -web.listen-address string
    	  address to listen on for web interface and telemetry. (default ":9533")
  -web.telemetry-path string
    	  path under which to expose metrics. (default "/metrics")
  -webhook-method string
        the HTTP method url to use to send the webhook (default "POST")
  -webhook-status-code int
        the HTTP status code indicating successful triggering of reload (default 200)
  -webhook-url string
        the url to send a request to when the specified config map volume directory has been updated
  -webhook-retries integer
        the amount of times to retry the webhook reload request
```

### License

This project is [Apache Licensed](LICENSE.txt)

