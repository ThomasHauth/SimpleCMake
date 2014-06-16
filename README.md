-- Introduction to using Eclipse with CMSSW --

The Eclipse IDE is a versatile application which can host various 
program-language specific plugins. The plugin for C/C++ is called CDT.

You can download an Eclipse Release with CDT already installed here:

http://www.eclipse.org/downloads/

look for the download 
"Eclipse IDE for C/C++ Developers"

Other plugins exist: Java, Python, Latex, ...

For the following examples, log into a CERN lxplus node using
ssh -Y lxplus.cern.ch

You can extract and run the downloaded Eclipse with the following commands:

wget http://mirror.switch.ch/eclipse/technology/epp/downloads/release/kepler/SR2/eclipse-cpp-kepler-SR2-linux-gtk-x86_64.tar.gz
tar xzf eclipse-cpp-kepler-SR2-linux-gtk-x86_64.tar.gz
eclipse/eclipse

## Simple CMake Project

You can use this simple cmake-based test program to test-drive the Eclipse IDE:

git clone https://github.com/ThomasHauth/SimpleCMake
cd SimpleCMake
cmake -G"Eclipse CDT4 - Unix Makefiles"

Now start Eclipse ( if not already running )
Select the folder containing the SimpleCMake folder as workspace
and import the SimpleCMake project:

-> File -> Import .. -> Existing Code as Makefile Project

The file import_existing_project.png shows where you can find this command.

Select "GNU Autotools Toolchain" as Toolchain. This should set the 
required include path automatically so you have working intelli sense.
If this did not work, you need to set the path to the C++ 
include headers by hand:

-> Right click on "SimpleCMake" in the ProjectExplorer
   -> Properties
     -> C/C++ General
      -> Path and Symbols
        -> GNU C++
          -> Add

Add these path to the include folders:
/usr/include/c++/4.4.7/
/usr/include/c++/4.4.7/x86_64-redhat-linux

Image import_project_settings.png shows you how the settings during
the project import should look like.

Press Ctrl+B to build the project.

** Test out some features:
- Project Explorer
- Compiling
- Errors
- Debug
- Git 
- Perspective and Windows
- Source browsing
- Refactoring Tools
- Auto formating
- Git integration is hidden behind right-click in the Project Explorer and 
  then "Team ..."

## CMMSW Project

Setup a CMSSW environment with scram, as known:

source /afs/cern.ch/cms/cmsset_default.sh
scram p CMSSW_5_3_19
cd CMSSW_5_3_19
cmsenv
git-cms-addpkg TrackingTools/TrackFitters
scram b -j8

Start eclipse now, only after you have set the CMSSW environment. Be sure to 
run "scram b" at least once before importing so Eclipse can find the make files.

Use the folder containing CMSSW_5_3_19 as workspace. Run the same importing procedure
as described for the simple project and make sure you select CMSSW_5_3_19/src to import.
This enables Eclipse to auto-discover and use the git repository contained in src.

Change the build command to "scram b"

-> Right click on the Project Name in the Project Explorer
  -> Properties
     -> C/C++ Build
        -> uncheck "Use default build command"
        -> type into the "Build command" field: "scram -j8"

Image scram_b_setup.png shows you how the changed settings look like.

Press Ctrl+B to test the new settings.

In the same properties window, you need to add the include headers:
 -> C/C++ General
  -> Path and Symbols
    -> GNU C++

For the CMSSW source tree:

${CMSSW_RELEASE_BASE}/src/

For the C++ header ( might depend on your compiler version ):
${COMPILER_RUNTIME_OBJECTS}/include/c++/4.7.2/x86_64-unknown-linux-gnu/
${COMPILER_RUNTIME_OBJECTS}/include/c++/4.7.2/

The image cmssw_paths.png shows you how the settings for the include 
path should look like.

** Test out some features:
- jump to declaration of types in the CMSSW code base
- Macro expansion in module.cc
- intelli sense on CMSSW types
- show include browser on a .cc file



