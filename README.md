# Self C++ SDK

Self is an architecture that enables Watson services in devices that perceive by vision, audition, olfaction, sonar, infrared energy, temperature, and vibration. Self-enabled devices express themselves and interact with their environments, other devices, and people through speakers, actuators, gestures, scent emitters, lights, navigation, and more.

The SDK allows users of the "Self" middle-ware to implement their own sensors, agents, classifiers, extractors, and more using C++.


# Binaries
You can download the latest build of the binaries from the following URL:
http://75.126.4.99/xray/?action=/download&packageId=Self-SDK-bin.zip

# Building Examples

## Building for Windows

1. Install Visual Studio 2015.
2. Open the solution found in vs2015/self-sdk.sln
3. Right click on the "self-sdk" project and select "Set as Startup Project".
4. Right click on the "self-sdk" projet, open properties. In the Debugging tab of the properties, you will need to change "Working Directory" to "$(TargetDir)".
5. Select Build->Build Solution
6. Select Debug->Start Debugging to run the project with debugging

NOTE: If using SourceTree, it may get stuck when trying to pull using SSH. Exectue the following commands on the command line to fix the problem with the git client trying to be interactive:
* cd "C:\Program Files (x86)\Atlassian\SourceTree\tools\putty"
* plink git@github.ibm.com

## Building for OSX
1. Set up [CMake](http://doc.aldebaran.com/2-1/dev/cpp/install_guide.html#required-buidsys). To install CMake by using Homebrew, run `brew install cmake`.
  * To install Homebrew, run the following command in your terminal: ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
2. Set up [qiBuild](http://doc.aldebaran.com/2-1/dev/cpp/install_guide.html#qibuild-install).
  * `pip install qibuild` (NOTE: it is highly recommended to download [anaconda python version 2.7](https://www.continuum.io/downloads) to have pip correctly configured)
  * `qibuild config --wizard` (use default setup for steps by pressing 1 twice)
2. Download [the Mac Toolchain for Mac (C++ SDK 2.1.4 Mac 64)](https://community.aldebaran.com/en/resources/software) and unzip the package into `~/toolchains/naoqi-sdk-mac64/`.
3. Run the following commands:
  * cd {self root directory}
  * qibuild init  
  * qitoolchain create mac ~/toolchains/naoqi-sdk-mac64/toolchain.xml
  * quibuild add-config mac --toolchain mac
  * ./scripts/install_mac.sh [user@host] [profile]
  
This stages the executables in the SELF/sdk/bin/mac directory on your local computer. You can change into that directory and run the unit_test and self_instance executables.

PS: If you run into issues with the build, you might have to change a couple of Boost header files, as described here: https://github.com/Homebrew/legacy-homebrew/issues/27396 (specifically, you might have to replace your copy of Boost's boost/atomic/detail/cas128strong.hpp and boost/atomic/detail/gcc-atomic.hpp with the latest available in the Boost directory)

## Building for Linux
1. Set up qibuild and CMake. You can use your Linux package manager to install CMake, and any distribution of Python (2.7 recommended) to install qibuild through pip.
2. Download the [Linux Toolchain for Linux (C++ SDK 2.1.4 Linux 64)](https://community.aldebaran.com/en/resources/software) and unzip the package into `~/toolchains/naoqi-sdk-linux64/`.
3. Run the following commands:
  * cd {self root directory}
  * qitoolchain create linux ~/toolchains/naoqi-sdk-linux64/toolchain.xml
  * qibuild init
  * qibuild add-config linux --toolchain linux
  * ./scripts/install_linux.sh [profile]
  
## Building for Nao/Pepper using OSX

1. Setup qibuild & cmake, see http://doc.aldebaran.com/2-1/dev/cpp/install_guide.html for instructions on getting those installed.
2. Download the "Cross Toolchain" for Mac from https://community.aldebaran.com/en/resources/software and unzip into ~/toolchains/ctc-mac64-atom.2.4.2.26/.
3. Run the following commmands:
  * cd {self-sdk root directory}
  * qibuild init
  * qitoolchain create nao ~/toolchains/ctc-mac64-atom.2.4.2.26/toolchain.xml
  * qibuild add-config nao --toolchain nao --default
  * ./scripts/install_nao.sh [user@host] [profile]
  
This installs SELF on the remote machine whose user name and IP address you supply. You can go to the ~/self/latest directory on that machine and run run_self.sh. This has been tested on Red Hat Enterprise 6.6 and 6.7.
