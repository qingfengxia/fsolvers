# Multiphysics FEM solver based on Fenics

[![Build Status](https://travis-ci.org/qingfengxia/FenicsSolver.svg?branch=master)](https://travis-ci.org/qingfengxia/FenicsSolver.svg) [![Coverage Status](https://coveralls.io/repos/github/qingfengxia/FenicsSolver.svg/badge.svg?branch=master)](https://coveralls.io/github/qingfengxia/FenicsSolver.svg?branch=master)

This is a sub-projects of [intelligient engineering design](https://qingfengxia.github.io/)

by Qingfeng Xia, 2017~

This is derived from my personal independent research, although I am not yet financially independent in the University of Oxford. This solver has features beyond commercial commercial solvers, in its capability to solve multibody, multi-physics, multiscale and reduced-order nonlinear problems.

This software project is an essential part of my research ambition in *Measurement and modelling at extreme conditions* and *Automated and intelligent engineering design*.

![Schematic of automated engineering design pipeline](https://forum.freecadweb.org/download/file.php?id=73587)

> **Note**   Fenics-X, the next generation Fenics, is expected in 2020. The API change in FenicsX should not affect FenicsSolver's json input format. If the mesh input format can support complicate boundary mesh, the previous effort of GUI inside FreeCAD would be more useful to solve more realistic engineering problem.  I am investigating a standard solver input format, to enable coupling with other multi-physics solver.

## License

LGPL licensed as [FreeCAD](https://github.com/FreeCAD/FreeCAD) and [fenics-project](https://fenicsproject.org/)

## Screenshot

There has been some effort to give a GUI for setup FenicsSolver in [FreeCAD's CFD module](https://github.com/qingfengxia/Cfd) Features include boundary condition selection and setup in GUI,  mesh and FenicsSolver input generation, but it is not a top priority in regarding research.

![FenicsSolver as a FEM solver in CfdWorkbench of FreeCAD](FenicsSolver_FreeCAD.png?raw=true "FenicsSolver as a CFD solver in CfdWorkbench of FreeCAD")

## Description

A set of multi-physics FEM solvers based on Fenics with GUI support(via integration Fenics into FreeCAD FemWorkbench and CfdWorkbench), focusing on multi-body, reduced-order nonlinear problem and mutlti-solver coupling.It functions like COMSOL or Moose, but it is free and it is made of Python.

+ Solvers implemented:
  - Scalar Transport (heat transfer, mass transfer, electric potential, etc)
  - Naiver Stokes incompressible laminar flow,
  - linear elasticity, nonlinear (hyper-elastic) elasticity, large deformation, plasticity

+ Solvers under development:
  - scalar transport using DG
  - viscoelastic
  - Naiver Stokes compressible laminar flow
  - Maxwell electromagnetics
  - drift-diffusion (plasma and semiconductor)
  - wave propagation

+ coupling of above solvers
  - flow-structure interaction (coded but not yet tested)
  - thermal, chemical, electrical, structure process (yet completed)

+ Coupling to external solvers:
  - turbulent flow and multiphase flow will be implemented by coupled to external CFD solver, OpenFOAM.
  - see the sister project OpenFOAM preprocessor within FreeCAD Cfd workbench <https://github.com/qingfengxia/Cfd>


## Installation

It is python2 and python3 compatible, just as fenics itself. For Fenics version 2017.2 on ubuntu, Python3 is recommended, since there is some binary string/unicode problem in Python 2. Fenics 2017.2 also remove VTK plotting, and most of plotting in FenicsSolver examples are ignored.

general installation guide on Linux: <https://fenicsproject.org/docs/dolfin/dev/python/installation.html>
link to install lastest Fenics via PPA on ubuntu: <https://launchpad.net/~fenics-packages/+archive/ubuntu/fenics>
```
sudo add-apt-repository ppa:fenics-packages/fenics
sudo apt-get update
sudo apt-get install fenics python-dolfin
#Fenics 2018.1 has only python3
#sudo apt-get install fenics python3-dolfin
```

copy this folder to any place on the python search path (PYTHON_PATH), assuming fenics has been installed.

```
git clone https://github.com/qingfengxia/FenicsSolver.git
```

installation via PIP will be implemented later once API is stable, but an early preview v0.1 could be privided
```
#make sure you have install Fenics, then install by pip(python) or pip3(python3)
sudo pip install FenicsSolver  # not working
```

to install the latest version for python3 directly form github, this will not install test files
```
pip3 install git+https://github.com/qingfengxia/FenicsSolver.git#FenicsSolver
# Ubuntu16.04 pip3 seems too old to install matplotlib.
# fenics 2019.1 can be installed from pip
```



## To cite this code

My journal papers using this code:

1. [Quasi-static  finite element modelling of thermal distribution and heat partitioning  for the multi-component system of high speed metal cutting](https://scholar.google.co.uk/scholar?oi=bibs&cluster=14068789234387025355&btnI=1&hl=en), Q Xia, DRH Gillespie - Journal of Materials Processing Technology, 2019

2. [Quasi-Static Thermal Modeling of Multiscale Sliding Contact for Unlubricated Brush Seal Materials](https://scholar.google.co.uk/scholar?oi=bibs&cluster=17170664792619422119&btnI=1&hl=en)

   Q Xia, DRH Gillespie, AK Owen, G Franceschini - Journal of Engineering for Gas Turbines and Power, 2019

## Acknowledgement

Thanks for my family members' (esp, Mrs J Wang) understanding and support, so I can work at home.



## Tested version

This package is under heavy refactoring, considered alpha.

This package is python 2 and python 3 compatibe.
Fenics version 2017.1 tested is on Ubuntu16.04 and python 2.7 with/without FreeCAD 0.17 dev.
Fenics version 2017.2 tested is on Ubuntu16.04 and Python 3, without FreeCAD GUI.
Fenics version 2019.1 tested is on Ubuntu18.04 and Python 3, with FreeCAD 0.19 dev.

Run the python script files with "test_" suffix, which are gtest compatible.

## Documentation:

**doxygen/sphinx** generated document is planned, yet completed

## How to contribute

There are lots of places to be improve:
+ Code review, esp. json solver setup input data structure, naming, It should be well-design and stable
+ testing on different Linux platform

new features:
+ limits for variable
+ a general higher order temporal integral
+ DG scalar transportation, currently, the DG solver does not work with 3D geometry.
+ Maxwell equation

## Roadmap and progress

see also my presentation at Fenics 18: [Automated Mechanical Engineering Design using Open Source CAE Software Packages](doc/Fenics18_Xia.pdf)

### Initial demonstration (Sep 2017)

A series of object oriented solvers: *ScalerEquationSolver*, *CoupledNavierStokesSolver* and *LinearElasticitySolver*, derived from *BaseSolver*, while a few other are under active development.

Case setup: json file format is the text case setup file, mapping directly to and from python dict data structure.

### FreeCAD GUI integration (Nov 2017)

2D and 3D xml mesh and case setup writing has been implemented within [CfdWorkbench](https://github.com/qingfengxia/Cfd), this feature has yet been push to FreeCAD master.

Meanwhile, FreeCAD developer *joha2* has added mesh export function in FemWorkbench, once the boundary mesh can be exported, case setup for fenics solver will be write in FreeCAD workbench.


###  Coupling of multiple solvers (implemented in 2018, not yet fully tested)

Fluid-structure interaction coupling has a initial implementation in segregate coupling mode, see engine seal FSI simulation:
![2D FSI simulation of labyrinth seal](doc/fsi_velmag.mp4)

Tight coupling of all physical fields is under design, target on thermal modelling of complicated systems like bearing, motor, etc.

### Coupling with external solvers OpenFOAM (some work has been done, but yet completed, scheduled to 2019)

VTK is the data exchange format for one-way coupling from OpenFOAM to FenicsSolver, from Foam to VTK and VTK to Foam (mesh and internal field data files)
Two-way coupling should be implemented with the multiphysics coupling library [preCICE](https://github.com/precice/precice)

a video/presentation of my *13th OpenFOAM Workshop* presentation can be found here:
[Coupling OpenFOAM with FeniCS for multiphysis simulation](https://www.iesensor.com/blog/2018/06/25/coupling-openfoam-with-fenics-for-multiphysis-simulation-openfoam-workshop-13-presentation/)

###  Update code to be compatible with Fenics 2019.1 on Python3 (2019)

almost done

### Coupling with electomagnetic, structural and thermal simulation (2019)

#### thermal-elastic-plastic coupling
#### pip packaging and installation guide
#### Travis CI integration

### Update API for Fenics-X (2020)






