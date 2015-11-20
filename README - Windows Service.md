# OSVR-win-installer
Windows installer for OSVR server application
Installer script built with NSIS.

## NSIS script: setup_service.nsi##

- Uses the following plugins
	- LogEx.dll
	- nsProcess.dll
	- newadvsplash.dll
	- SimpleSC.dll
	- AccessControl.dll

## Requirements for running the script:##
-	Name of the script is: setup_service.nsi
-	Desired distribution directory can be specified at compile time by defining *distroDirectory*
-	If *distroDirectory* is not passed in at compile time, the value is defaulted to ../Distro
-   You want a Profiler directory located inside ../Distro/ along with the bin directory, the profile directory should contain the OSVR configuration utility.
-	Uses registry value to determine if installed version is newer or older than version contained in the installer
-   The installer will warn but still install if it finds a newer version installed
- The following items must be in the script directory
	- splash.bmp
	- osvr_server.ico
	- OSVR_Service.exe (You need to either rename OSVR_Service_32.exe or OSVR_Service_64.exe to OSVR_Service.exe)
	- license.txt (Apache 2.0 license)
- A batchfile is provided for Continuous Integration convenience. It takes as its only argument the path that you would like to pass on to define as the distroDirectory
	- the batch file must be modified on the CI target such that the path to makensis.exe is properly set

## Installer capabilities: ##
- checks for free drive space before installing
- checks that installed version is less than the version about to be installed
- logs messages with timestamps to diagnose installer/uninstaller issues
- uses osvr.ico for start menu and uninstaller entry in the control panel
- uninstall shows up in the control panel
- deletes all OSVR files upon uninstall
- cleans up registry upon uninstall
- stops the OSVR Service before uninstalling or updating without user intervention
- install and uninstall do not require restart
- creates a service called "OSVR Service"
- starts the OSVR Service after installer completes
- starts the configuration utility once the intaller completes.
- read version number from osvr_server.exe in the distribution
- read distro install size from distribution to use to check for available disk space
- installs a registry key to facilitate plugin installations: HKLM/Software/OSVR/installationDirectory
- installs an environment variable to facilitate plugin installations: OSVR\_INSTALL_DIR

## Improvements: ##
- Utilise modern UI
- osvr_server.exe needs to be converted into a proper service
