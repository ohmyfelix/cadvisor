<h1 align=center>Dockette / cAdvisor</h1>

<p align=center>
   Minimal Docker image for <a href="https://github.com/google/cadvisor">cAdvisor</a> (Container Advisor), mirroring <code>ghcr.io/google/cadvisor</code> under the <code>dockette/cadvisor</code> name on Docker Hub.
</p>

<p align=center>
🕹 <a href="https://f3l1x.io">f3l1x.io</a> | 💻 <a href="https://github.com/f3l1x">f3l1x</a> | 🐦 <a href="https://twitter.com/xf3l1x">@xf3l1x</a>
</p>

<p align=center>
  <a href="https://hub.docker.com/r/dockette/cadvisor/"><img src="https://badgen.net/docker/pulls/dockette/cadvisor"></a>
  <a href="https://bit.ly/ctteg"><img src="https://badgen.net/badge/support/gitter/cyan"></a>
  <a href="https://github.com/sponsors/f3l1x"><img src="https://badgen.net/badge/sponsor/donations/F96854"></a>
</p>

-----

## What it is

[cAdvisor](https://github.com/google/cadvisor) collects and exposes resource usage and performance data for running containers. See the upstream [README](https://github.com/google/cadvisor/blob/master/README.md) and [running docs](https://github.com/google/cadvisor/blob/master/docs/running.md) for full detail.

## Usage

Typical **Docker on Linux** host monitoring (aligned with the [upstream quick start](https://github.com/google/cadvisor/blob/master/README.md)); the UI and API listen on port **8080** inside the container:

```sh
docker run -d --name cadvisor --privileged --device=/dev/kmsg \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:ro \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --volume=/dev/disk/:/dev/disk:ro \
  --publish=8080:8080 \
  dockette/cadvisor:0.56.2
```

Then open `http://localhost:8080`. On rootless Docker, Podman, or non-default graph roots, the path to the container runtime state may differ from `/var/lib/docker`; adjust the bind mount to match your setup.

`--privileged` and `--device=/dev/kmsg` match the common upstream example for broad compatibility; you may be able to reduce privileges for your environment—see upstream [runtime options](https://github.com/google/cadvisor/blob/master/docs/runtime_options.md).

## Versions

Docker image tags use the **numeric** form (e.g. `0.56.2`), matching `ghcr.io/google/cadvisor`. GitHub [releases](https://github.com/google/cadvisor/releases) use a `v` prefix (e.g. v0.56.2) for the same version.

| Image tag | Equivalent upstream | Docker Hub |
|-----------|---------------------|------------|
| `dockette/cadvisor:0.56.2` | `ghcr.io/google/cadvisor:0.56.2` | [tags](https://hub.docker.com/r/dockette/cadvisor/tags/) |
| `dockette/cadvisor:latest` | same as `0.56.2` (rolling) | [tags](https://hub.docker.com/r/dockette/cadvisor/tags/) |

This image is a **thin republish**: the Dockerfile uses `FROM ghcr.io/google/cadvisor:${CADVISOR_VERSION}` so runtime behavior matches that upstream tag.

For **cAdvisor versions before v0.53.0**, the historical registry was `gcr.io/cadvisor/cadvisor` instead of GHCR; this repo only republishes the modern GHCR tags.

-----

Consider supporting [f3l1x on GitHub Sponsors](https://github.com/sponsors/f3l1x) if you rely on this. Thanks for using it.
