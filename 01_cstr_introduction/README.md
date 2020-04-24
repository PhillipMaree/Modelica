# Modelica
Modelica Related project work for SoS simulation

#### Getting started

Running ./start.sh will start a docker container containing various numerical optimization and modellings tools related to this work. 

###Exteral OMEdit compile and export FMU instructions

Below are some instruction pointer to do model compilation and FMU export outside of the OMEdit environment. 

#### Simulate in OMEdit env

To simulate mpc you require the correct C/C++ compiler flags included.

-lstdc++ -lcasadi

####Getting started compiling

Step to make sure model compiles:

1. cd /build
2. omc -s ../MPC.mo
3. make -j -f MPC.makefile
4. ./MPC

####Getting started exporting FMU (when using embedded C extern function calls)

The export utility of Open modelica is far from perfect and at the moment I use some dubious footwork to get
things to work.

Steps to export FMU are (note this FMU is dependant on casadi being installed on system where FMU is deployed):

0. Generate both static 
1. In OMEdit, right click on library model->Export-FMU
2. cd <Project_Folder>/<Library_Name>/<Library_Name.fmutmp>/source
3. export LDFLAGS="-lcasadi -lstdc++" 
4. export CPPFLAGS=-I"/usr/include/omc/c/fmi/"
4. ./configure
5. make

Future ideas to streamline build:

[1.] libstdc++ use g++ to link and flags "-static-libstdc++"
[2.] export MODELICAUSERCFLAGS=-Wl,-Bdynamic -lnmpc before running OMEdit or omc to build the FMU (if I need dynamic)

