# Sherpa Docker Image

Docker image based on Ubuntu 20.04 for [Sherpa](https://sherpa-team.gitlab.io/). 

## Distributed Software

The Docker image contains:

* [Sherpa](https://sherpa-team.gitlab.io/)`v2.2.15`
* Python 3.8
* [HepMC2](http://hepmc.web.cern.ch/hepmc/) `v2.06.11`
* [LHAPDF](https://lhapdf.hepforge.org/) `v6.5.4`
* [FastJet](http://fastjet.fr/) `v3.4.0`
* [PYTHIA](https://pythia.org/) `v8.309`

## Installation

- Check the [list of available tags on Docker Hub](https://hub.docker.com/r/yangphy/sherpa/tags) to find the tag you want.
- Use `docker pull` to pull down the image corresponding to the tag. For example:

```
docker pull yangphy/sherpa:Ubuntu20.04-aarch64-1.0.0
```

## Update notes

### There are some changes need to be done for the aarch64

* The ` -m64` flag is only used to specify that the compiled code should be 64-bit on x86-64 architecture (i.e., Intel or AMD) machines. On ARM-based architectures, such as Apple M1, the flag is not needed and will actually cause an error during compilation.
* The `-mcmodel` is `small`, `medium`, and `large` for x86-64 architecture (i.e., Intel or AMD), while it is `tiny`, `small`, and `large` for aarch64. Since most of the makefiles were designed for x86-64 architecture, we need to manually change `medium` to `small` to compile the package on aarch64 machines.




