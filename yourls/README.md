<!--

********************************************************************************

WARNING:

    DO NOT EDIT "yourls/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "yourls/" combined with a set of templates)

********************************************************************************

-->

# Supported tags and respective `Dockerfile` links

**No supported tags found!**

It is very likely that `yourls` does not support the currently selected architecture (`windows-amd64`).

# Quick reference

-	**Where to get help**:  
	[the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://blog.docker.com/2016/11/introducing-docker-community-directory-docker-community-slack/), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)

-	**Where to file issues**:  
	[https://github.com/YOURLS/docker-yourls/issues](https://github.com/YOURLS/docker-yourls/issues)

-	**Maintained by**:  
	[YOURLS](https://github.com/YOURLS/docker-yourls)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	[`amd64`](https://hub.docker.com/r/amd64/yourls/)

-	**Published image artifact details**:  
	[repo-info repo's `repos/yourls/` directory](https://github.com/docker-library/repo-info/blob/master/repos/yourls) ([history](https://github.com/docker-library/repo-info/commits/master/repos/yourls))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images PRs with label `library/yourls`](https://github.com/docker-library/official-images/pulls?q=label%3Alibrary%2Fyourls)  
	[official-images repo's `library/yourls` file](https://github.com/docker-library/official-images/blob/master/library/yourls) ([history](https://github.com/docker-library/official-images/commits/master/library/yourls))

-	**Source of this description**:  
	[docs repo's `yourls/` directory](https://github.com/docker-library/docs/tree/master/yourls) ([history](https://github.com/docker-library/docs/commits/master/yourls))

-	**Supported Docker versions**:  
	[the latest release](https://github.com/docker/docker-ce/releases/latest) (down to 1.6 on a best-effort basis)

# What is YOURLS?

YOURLS is a set of PHP scripts that will allow you to run Your Own URL Shortener. You'll have full control over your data, detailed stats, analytics, plugins, and more. It's free.

> [github.com/YOURLS/YOURLS](https://github.com/YOURLS/YOURLS)

![logo](https://raw.githubusercontent.com/docker-library/docs/56798ba4051d863557e7e6256c452a9265745675/yourls/logo.png)

# How to use this image

```console
$ docker run --name some-yourls --link some-mysql:mysql \
    -e YOURLS_SITE="https://example.com" \
    -d winamd64/yourls
```

The following environment variables are also honored for configuring your YOURLS instance:

-	`-e YOURLS_DB_HOST=...` (defaults to the IP and port of the linked `mysql` container)
-	`-e YOURLS_DB_USER=...` (defaults to "root")
-	`-e YOURLS_DB_PASS=...` (defaults to the value of the `MYSQL_ROOT_PASSWORD` environment variable from the linked `mysql` container)
-	`-e YOURLS_DB_NAME=...` (defaults to "yourls")
-	`-e YOURLS_TABLE_PREFIX=...` (defaults to "", only set this when you need to override the default table prefix in wp-config.php)
-	`-e YOURLS_COOKIEKEY=...` (default to unique random SHA1s)
-	`-e YOURLS_SITE=...` (yourls instance url)

If the `YOURLS_DB_NAME` specified does not already exist on the given MySQL server, it will be created automatically upon startup of the `yourls` container, provided that the `YOURLS_DB_USER` specified has the necessary permissions to create it.

If you'd like to be able to access the instance from the host without the container's IP, standard port mappings can be used:

```console
$ docker run --name some-yourls --link some-mysql:mysql -p 8080:80 -d winamd64/yourls
```

Then, access it via `http://localhost:8080` or `http://host-ip:8080` in a browser.

If you'd like to use an external database instead of a linked `mysql` container, specify the hostname and port with `YOURLS_DB_HOST` along with the password in `YOURLS_DB_PASS` and the username in `YOURLS_DB_USER` (if it is something other than `root`):

```console
$ docker run --name some-yourlss -e YOURLS_DB_HOST=10.1.2.3:3306 \
    -e YOURLS_DB_USER=... -e YOURLS_DB_PASS=... -d winamd64/yourls
```

## ... via [`docker stack deploy`](https://docs.docker.com/engine/reference/commandline/stack_deploy/) or [`docker-compose`](https://github.com/docker/compose)

Example `stack.yml` for `yourls`:

```yaml
version: '3.1'

services:

  yourls:
    image: yourls
    restart: always
    ports:
      - 8080:80
    environment:
      YOURLS_DB_PASS: example
      YOURLS_SITE: https://example.com

  mysql:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
```

[![Try in PWD](https://github.com/play-with-docker/stacks/raw/cff22438cb4195ace27f9b15784bbb497047afa7/assets/images/button.png)](http://play-with-docker.com?stack=https://raw.githubusercontent.com/docker-library/docs/56798ba4051d863557e7e6256c452a9265745675/yourls/stack.yml)

Run `docker stack deploy -c stack.yml yourls` (or `docker-compose -f stack.yml up`), wait for it to initialize completely, and visit `http://swarm-ip:8080`, `http://localhost:8080`, or `http://host-ip:8080` (as appropriate).

## Adding additional libraries / extensions

This image does not provide any additional PHP extensions or other libraries, even if they are required by popular plugins. There are an infinite number of possible plugins, and they potentially require any extension PHP supports. Including every PHP extension that exists would dramatically increase the image size.

If you need additional PHP extensions, you'll need to create your own image `FROM` this one. The [documentation of the `php` image](https://github.com/docker-library/docs/blob/master/php/README.md#how-to-install-more-php-extensions) explains how to compile additional extensions.

The following Docker Hub features can help with the task of keeping your dependent images up-to-date:

-	[Automated Builds](https://docs.docker.com/docker-hub/builds/) let Docker Hub automatically build your Dockerfile each time you push changes to it.
-	[Repository Links](https://docs.docker.com/docker-hub/builds/#repository-links) can ensure that your image is also rebuilt any time `yourls` is updated.

# License

View [license information](https://github.com/YOURLS/YOURLS/blob/master/LICENSE) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `yourls/` directory](https://github.com/docker-library/repo-info/tree/master/repos/yourls).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.