# MadGraph5_aMC-NLO Python 3 Docker Image

Docker image for Python 3 compliant [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo).

## Linux distributions

The dockerfiles support both AMD64 and aarch64 platforms 

* [Ubuntu 20.04](Ubuntu2004/README.md)
* [Ubuntu 22.04](Ubuntu2204/README.md)

## Installation

- Check the [list of available tags on Docker Hub](https://hub.docker.com/r/yangphy/mg5_amc_nlo/tags) to find the tag you want.
- Use `docker pull` to pull down the image corresponding to the tag. For example:

```
docker pull yangphy/mg5_amc_nlo:Ubuntu20.04-aarch64-root-1.0.0
```