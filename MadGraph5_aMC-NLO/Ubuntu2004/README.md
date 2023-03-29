# MadGraph5_aMC-NLO Python 3 Docker Image for Ubuntu 20.04

Docker image based on Ubuntu 20.04 for Python 3 compliant [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo). 

## Distributed Software

The Docker image contains:

* [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo) `v3.4.2`
* Python 3.8
* [HepMC2](http://hepmc.web.cern.ch/hepmc/) `v2.06.11`
* [LHAPDF](https://lhapdf.hepforge.org/) `v6.5.4`
* [FastJet](http://fastjet.fr/) `v3.4.0`
* [PYTHIA](https://pythia.org/) `v8.309`
* [Delphes](https://cp3.irmp.ucl.ac.be/projects/delphes/) `v3.5.0`
* [ROOT](https://root.cern/) `v6.28.00`

Additionally contains MadGraph5 controlled dependencies for NLO processes:

* [CutTools](https://inspirehep.net/literature/768411)
* [IREGI](https://inspirehep.net/literature/1293923)
* [Ninja](https://github.com/peraro/ninja)
* [Collier](https://inspirehep.net/literature/1451658)

## Update notes

### There are some changes need to be done for the aarch64

* The ` -m64` flag is only used to specify that the compiled code should be 64-bit on x86-64 architecture (i.e., Intel or AMD) machines. On ARM-based architectures, such as Apple M1, the flag is not needed and will actually cause an error during compilation.
* The `-mcmodel` is `small`, `medium`, and `large` for x86-64 architecture (i.e., Intel or AMD), while it is `tiny`, `small`, and `large` for aarch64. Since most of the makefiles were designed for x86-64 architecture, we need to manually change `medium` to `small` to compile the package on aarch64 machines.

### `pythia8` "undefined reference to `pthread_create`" issue 

Need to add `-pthread` and `-lpthread` flages for configure, as the following
```
--cxx-common="-O2 -pedantic -pthread  -lpthread -W -Wall -Wshadow -fPIC -std=c++17"
```

