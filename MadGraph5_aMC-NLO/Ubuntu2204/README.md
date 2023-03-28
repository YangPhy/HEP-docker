# MadGraph5_aMC-NLO Python 3 Docker Image

Docker image based on Ubuntu 22.04 for Python 3 compliant [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo). 

## Distributed Software

The Docker image contains:

* [MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo) `v3.4.2`
* Python 3.10
* [HepMC2](http://hepmc.web.cern.ch/hepmc/) `v2.06.09`
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

### The `tirpc` issue 

In Ubuntu 22.04 and future versions, the `/usr/include/rpc` is moved to `/usr/include/tirpc`

* To compile Fastjet, need to set flags 'LIBS=-ltirpc CPPFLAGS=-I/usr/include/tirpc' for configure
* For ExRootAnalysis, need to change `CXXFLAGS += $(ROOTCFLAGS) -Wno-write-strings -D_FILE_OFFSET_BITS=64 -DDROP_CGAL -I. -I/usr/include/tirpc` and ` LIBS = $(ROOTLIBS) -ltirpc` in the `Makefile`

### The `PYTHONPATH` issue

In Ubuntu 22.04, the `.../lib/python3.8/site-packages` is changed to `.../lib/python3.10/dist-packages`

For the following packages, the `PYTHONPATH` of `LHAPDF` need to be set different from its official instruction

* Fastjet
* LHAPDF


