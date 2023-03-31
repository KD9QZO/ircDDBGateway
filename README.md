This is the ircDDB Gateway. It allows a D-Star Repeater to interface into callsign routing via ircDDB and all of the different reflector types. It includes many facilities, including:

* Supports Icom stacks.
* Supports homebrew repeaters.
* Icom DD mode under Linux with Internet access.
* Callsign routing via ircDDB.
* D-Plus REF reflectors.
* DExtra XRF reflectors.
* DCS reflectors.
* XLX reflectors.
* CCS7 routing.
* D-RATS data transfers.
* Gateway DPRS data to APRS-IS.
* Full multi lingual text and voice announcements.
* DTMF or UR call control.
* Remote control interface.
* StarNet server.
* Ability to set policies for reflector usage.

There are many external programs that allow for inserting voice or text messages, as well as remote control operation.

They all build on 32-bit and 64-bit Linux as well as on Windows using Visual Studio 2017 on x86 and x64.

This software is licenced under the GPL v2.

# Build and installing
## Regular build
```shell
make
make -f MakefileGUI #only required if you want to build the GUI programs
sudo make install
```
## Drop-in replacement for dl5di OpenDV packages
This will conpile the program to be used as a drop in replacement for the no longer maintained DL5DI OpenDV packages. Systemd files to run ircddbgatewayd as daemon will also be installed.
```shell
export TARGET=opendv
make
make -f MakefileGUI #only required if you want to build the GUI programs
sudo make install
```
Note that you may need to use `sudo -E make install` to pass the environment variables, or just `sudo TARGET=opendv make install` to correctly create the opendv user/directories, depending on your system configuration.

Now you should edit the configuration in the file /etc/ircddbgateway to match your needs.

When building in TARGET=opendv mode, the necessary systemd unit files will be installed. To ensure ircddbgatewayd starts at system boot, and then immediately start it, use:
```shell
sudo systemctl enable ircddbgatewayd.service
sudo service ircddbgatewayd start
```

If you wish to remove the manually installed files you may use `sudo make uninstall`.
Note that this will remove the systemd unit, but will not first stop or disable the service. To do so, first use:
```shell
sudo systemctl disable --now ircddbgateway.service
```
