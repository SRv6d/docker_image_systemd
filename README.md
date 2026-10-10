# Systemd Docker Images

[![Build and Publish Images](https://github.com/SRv6d/docker_image_systemd/actions/workflows/build-and-publish.yml/badge.svg?branch=main)](https://github.com/SRv6d/docker_image_systemd/actions/workflows/build-and-publish.yml)

Base Docker images with systemd as PID 1. Use them to test deployments of services managed by systemd inside containers.

## Supported Images

The supported versions are Debian stable and oldstable, plus Ubuntu LTS releases in standard support. Images are rebuilt weekly to receive upstream security updates.

| Image | Supported tags | Platforms |
| --- | --- | --- |
| [`srv6d/debian-systemd`](https://hub.docker.com/r/srv6d/debian-systemd) | `bookworm`, `12`; `trixie`, `13` | `linux/amd64`, `linux/arm/v7`, `linux/arm64` |
| [`srv6d/ubuntu-systemd`](https://hub.docker.com/r/srv6d/ubuntu-systemd) | `jammy`, `22.04`; `noble`, `24.04`; `resolute`, `26.04` | `linux/amd64`, `linux/arm/v7`, `linux/arm64` |

Debian `buster` (`10`) and `bullseye` (`11`), and Ubuntu `focal` (`20.04`), remain available on Docker Hub for existing users. They are end of life and are no longer rebuilt.

## Running systemd

Run these images on a Linux Docker host with a shared cgroup namespace and cgroup filesystem:

```console
docker run --detach --name systemd-test \
  --privileged \
  --cgroupns=host \
  --volume /sys/fs/cgroup:/sys/fs/cgroup:rw \
  srv6d/debian-systemd:trixie

docker exec systemd-test systemctl is-system-running --wait
# running

docker rm --force systemd-test
```

`--privileged`, `--cgroupns=host`, and the cgroup mount allow systemd to act as PID 1 and manage cgroups in the container.

## License

[GNU General Public License v3.0](./LICENSE)

## Author Information

Marvin Vogt (m@rvinvogt.com)
