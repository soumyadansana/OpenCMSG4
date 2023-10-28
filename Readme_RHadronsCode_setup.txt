######## README for original RHadrons project ###################
Step 1: Download the latest code
Step 2: Change the setup.sh to following - 
```
export ROOTSYS=$ROOTSYS
export G4INSTALL=/home/soumya/Downloads/geant4/geant4.10.04.p03
export G4WORKDIR=$PWD
export G4SYSTEM="Darwin-g++"
source /home/soumya/Downloads/geant4/geant4.10.04.p03-install/share/Geant4-10.4.3/geant4make/geant4make.sh
```
- This sets the environment and links to corresponding installation places of geant4 stuff
Step 3: source setup.sh and make
Step 4: Lots of debug options will appear due differences between geant4.9 and geant4.10 ; Debug / Update them. Some instances:
      - Units not recognized (GeV, TeV etc) -> add "using namespace CLHEP;" at the start of the files
      - G4MultipleScattering.h not found -> replaced with G4eMultipleScattering -> Lots of errors where header needs to be updated or removes because old
Step 5: There will be issues with libraries not found -> Fix by creating symbolic links after finding their actual name/headers (taken from https://stackoverflow.com/questions/16710047/usr-bin-ld-cannot-find-lnameofthelibrary)
      - ERROR: /usr/bin/ld: cannot find -lQtOpenGL 
      - Solution: try to find library with ld -lQtOpenGL --verbose -> will point to possible directories where it looked (eg. - /usr/lib/x86_64-linux-gnu/libQtOpenGL.so)
                  Go through the folder, most likely the .so exists but with different name (eg. /usr/lib/x86_64-linux-gnu/libQt5OpenGL.so) 
                  Create symbolic link to this to the directory where make looks for the link (eg. sudo ln -s /usr/lib/x86_64-linux-gnu/libQt5OpenGL.so /usr/lib/libQtOpenGL.so)
Step 6: The code should at this point at least compile.
