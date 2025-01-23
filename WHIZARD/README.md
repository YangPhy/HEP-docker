# WHIZARD Docker Image

Docker image based on Ubuntu 22.04 for [WHIZARD](https://whizard.hepforge.org/). 

## Distributed Software

The Docker image contains:

* [WHIZARD](https://whizard.hepforge.org/) `v3.1.2`
* Python 3.10
* [HepMC2](http://hepmc.web.cern.ch/hepmc/) `v2.06.11`
* [LHAPDF](https://lhapdf.hepforge.org/) `v6.5.4`
* [FastJet](http://fastjet.fr/) `v3.4.0`
* [PYTHIA](https://pythia.org/) `v8.309`

## Installation

- Check the [list of available tags on Docker Hub](https://hub.docker.com/r/yangphy/whizard/tags) to find the tag you want.
- Use `docker pull` to pull down the image corresponding to the tag. For example:

```
docker pull yangphy/whizard:Ubuntu22.04-aarch64-1.0.0
```

## Update notes

### There are some changes that need to be done for the `aarch64`

* The ` -m64` flag is only used to specify that the compiled code should be 64-bit on x86-64 architecture (i.e., Intel or AMD) machines. On ARM-based architectures, such as Apple M1, the flag is not needed and will actually cause an error during compilation.
* The `-mcmodel` is `small`, `medium`, and `large` for x86-64 architecture (i.e., Intel or AMD), while it is `tiny`, `small`, and `large` for aarch64. Since most of the makefiles were designed for x86-64 architecture, we need to manually change `medium` to `small` to compile the package on aarch64 machines.

### The `tirpc` issue 

In Ubuntu 22.04 and future versions, the `/usr/include/rpc` is moved to `/usr/include/tirpc`

* To compile `WHIZARD` and `FastJet`, need to set flags `LIBS=-ltirpc CPPFLAGS=-I/usr/include/tirpc` for configure

### The `PYTHONPATH` issue

In Ubuntu 22.04, the `.../lib/python3.8/site-packages` is changed to `.../lib/python3.10/dist-packages`

For the following packages, the `PYTHONPATH` of `LHAPDF` needs to be set differently from its official instruction

* Fastjet
* LHAPDF


