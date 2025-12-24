# Docker

Interchangable with `podman`

<!-- markdownlint-disable-next-line line-length -->
> **Keywords:** podman docker dockerhub image registry container build tag login push upload



## General

Don't forget to use `sudo docker`, it's necessary in most cases unless you
explicitly set up non-privileged docker.



## Build a Dockerfile

> `podman-build(1)`

Simply build the Dockerfile:

```sh
podman build .
```

But you probably want to tag it:

```sh
podman build -t <tag> .
```



## Tag an image

> `podman-tag(1)`

```sh
podman tag <image>[:tag] (<target>[:tag] ...)
```

Also `podman image tag`



## Log in

> `podman-login(1)`

Prepare a Personal Access Token if appropriate (most likely yes). Then:

```sh
podman login
```

Enter username, and PAT as password.



## Push an image

> `podman-push(1)`

First you'll need to [log in to the registry](#log-in). Then:

```sh
podman push <image> [destination]
```

If the image tag contains the registry path, then `destination` is not
required. Otherwise, specify both the image and the full destination path

#### Examples

```sh
# Push to a container registry
podman push quay.io/podman/stable

# Push to a container registry with another tag
podman push myimage quay.io/username/myimage
```

Also `podman image push`
