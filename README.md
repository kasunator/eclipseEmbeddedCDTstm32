# eclipseEmbeddedCDTstm32
Windows Eclipse embedded CDT installation instructions
The installations instructions are in the following link
https://eclipse-embed-cdt.github.io/

Eclipse embedded CDT installation instructions 
The installations instructions are in the following link
https://eclipse-embed-cdt.github.io/

Prerequisites for the Eclipse embedded CDT 
• node/npm/xpm - although not mandatory, but highly recommended, the second prerequisite is xpm (the xPack Package Manager), which is a Node.js portable application;
• Windows Build Tools - to build projects, on Windows it is necessary to install make, available from the xPack Windows Build Tools;
• Arm toolchain - to build Arm projects, an Arm toolchain like the xPack GNU Arm Embedded GCC is required;
• RISC-V toolchain - similarly, for RISC-V projects, a RISC-V toolchain like the xPack GNU RISC-V Embedded GCC is required;
• SEGGER J-Link - to debug projects, a JTAG probe is necessary together with the software to access it, for example the SEGGER J-Link software;
• OpenOCD - for some boards, xPack OpenOCD might also be useful;
• QEMU Arm - to run debug sessions without actual hardware, the xPack QEMU Arm emulator is necessary (the blinky tutorial mandates it).

	1) Install node/npm/xpm
How to install node and npm for windows: details in https://xpack.github.io/install/
Download the Windows Installer (.msi) from the Node.js download page and install it as usual, with administrative rights.
The result is a folder like C:\Program Files\nodejs, added to the system path since it includes the node.exe binary.

To check the installation  if you run the following you will get the response.
C:\>where node.exe
C:\Program Files\nodejs\node.exe
C:\>node --version
v16.14.2


Update the npm : 
A version of npm, usually a bit older, comes packed with Node.

C:\>where npm.cmd
C:\Program Files\nodejs\npm.cmd
C:\>npm --version
8.X.X


It is recommended to update it to the latest version:
C:\>npm install --global npm@latest

After executing  "C:\>npm install --global npm@latest" command  I can see that the new npm version changed to 9.1.3

C:\Users\kasun.beddewela>npm -v
9.1.3


Note: By default, global node packages are installed in the user home folder, in %APPDATA%\npm (like C:\Users\kasun.beddewela\AppData\Roaming\npm); and this path is not in the default environment.
So add this path to the %Path% manually. ( I did not have to do this, npm install  added it to the path automatically)

If you cant find the new version location %APPDATA%\npm in the %path%  or if the "npm -v"  gives the old version then you can run these commands
C:\> set Path=%APPDATA%\npm;%Path%

To make this setting persistent, also issue the following:

C:\> setx Path "%APPDATA%\npm;%Path%"


How to install xpm for windows : details form https://xpack.github.io/xpm/install/

Note: On Windows, by default, global Node.js packages are installed in the user home folder, in %APPDATA%\npm (like C:\Users\kasun.beddewela\AppData\Roaming\npm), and managing packages does not require administrative rights


Execute the following command 
C:\> npm install--global xpm@latest


The result is a some new of files in added the %APPDATA%\npm folder, you should be able to see xpm.cmd and xpm files inside  %APPDATA%\npm folder.

	2) Install Windows Build Tools
	
On Windows, install make and the rest of the build tools

C:> xpm install--global @xpack-dev-tools/windows-build-tools@latest

If this was successful you should be able to see new files in the following location 
%APPDATA%\xPacks\@xpack-dev-tools\windows-build-tools\x.x.x-x.x

You can uninstall 
C:> xpm uninstall --global @xpack-dev-tools/windows-build-tools --verbose

To test if successfully  installed, run the following command
C:\> %USERPROFILE%\AppData\Roaming\xPacks\@xpack-dev-tools\windows-build-tools\x.x.x-x\.content\bin\make --versi

	3) Now install ARM tool chain 
Install GCC compiler for ARM embedded
C:> xpm install --global @xpack-dev-tools/arm-none-eabi-gcc@latest --verbose

Install qemu , this is an emulator I don’t wthink this is needed 
C:\> xpm install --global @xpack-dev-tools/qemu-arm@latest --verbose

Install Open OCD this is a debugger etra to the JLINK 
C:\> xpm install --global @xpack-dev-tools/openocd@latest --verbose

Install Cmake Package 
C:\> xpm install --global @xpack-dev-tools/cmake@latest --verbose

Install ninja
C:\> xpm install --global @xpack-dev-tools/ninja-build@latest --verbose

Install meson build ( what is mason build?? )
C:\> xpm install --global @xpack-dev-tools/meson-build@latest --verbose


	4) install Eclipse IDE for Embedded C/C++ Developers
	The recommended method to install new Eclipses with the plug-ins is to use the Eclipse IDE for Embedded C/C++ Developers packages, which pack together
	
	• the Eclipse IDE for C/C++ Developers standard distribution with
	• the Eclipse Embedded CDT plug-ins
Just download and extract or use the eclispe installer to and install Eclipse IDE for Embedded C/C++ Developers.

    5) Requirements for JLINK debugging 

	• one or more Eclipse Debugging plug-ins
	• the GDB debugger (client) application: 
	• the GDB server application: 
	• the hardware drivers required by the JTAG/SWD probe

Eclipse debugging plug-ins
The debugging plug-ins come together with the other Eclipse Embedded CDT plug-ins; if you install the full Eclipse IDE for Embedded C/C++ Developers, package, they are included.
The GDB debugger (client) application

This is part of the tool chain  and it is located at the same  folder as all GNU toolchain binaries (compiler, linker, etc). You have to use the gdb client to debug an application, that came with the gdb compiler that was used to build it. 

The GDB server application: 
The GDB server is part of the Jlink package, Yo can download it form the Segger website at https://www.segger.com/downloads/jlink/.
 After installation  it is located at SEGGER\JLINK install location
In my case it is at C:\Program Files\SEGGER\JLink_V754b\JLinkGDBServerCL.exe

The hardware drivers required by the JTAG/SWD probe
These drivers are installed when you install the segger binaries https://www.segger.com/downloads/jlink/

How to test of JLINK gdb server is working 
Plug in the JLINK debugger and navigate to the location the JLINK GDB server is installed
In my case it is at C:\Program Files\SEGGER\JLink_V754b and execute the following command 
JLinkGDBServer -if SWD -device STM32F407VG