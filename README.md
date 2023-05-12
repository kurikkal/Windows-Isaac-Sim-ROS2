# Windows-Isaac-Sim-ROS2

##Install Visual Studio 2019
Install from this link

https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16&src=myvs&utm_medium=microsoft&utm_source=my.visualstudio.com&utm_campaign=download&utm_content=vs+community+2019

Make sure that the Visual C++ features are installed.
An easy way to make sure they’re installed is to select the Desktop development with C++ workflow during the install.Make sure that no C++ CMake tools are installed by unselecting them in the list of components to be installed.


##Install Windows Package Manager
Chocolatey is a package manager for Windows. It is used to make it easy to install tools and libraries needed for building and running ROS projects. The following instructions redirect the chocolatey install location into the c:\opt, so that you can clean or move a ROS environment from that one location.

In the Start Menu, find the "x64 Native Tools Command Prompt for VS 2019" item.
Right Click, select More then "Run as Administrator"
Copy the following command line:
```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```
Paste it into the command window.
Approve any prompts
Once it has completed, close the command prompt to complete the install.
Install Git:

Reopen the Visual Studio Command Window as described above.
Please install Git using the command here, even if you have it installed as an application:
```
choco upgrade git -y
```
Close and Reopen the Visual Studio Command Window as described above.

Ensure Git is now available in the Visual Studio command window:
```
git --version
```

##Installing ROS 2 Binaries
From the start menu, look for x64 Native Tools Command Prompt for VS 2019.
Open the command prompt as administrator.
Run the following to install ROS 2 Foxy.
```
mkdir c:\opt\chocolatey
set ChocolateyInstall=c:\opt\chocolatey
choco source add -n=ros-win -s="https://aka.ms/ros/public" --priority=1
choco upgrade ros-foxy-desktop -y --execution-timeout=0 --pre
```
You can close the command prompt now.

Now you have ROS 2 ros-foxy-desktop installed.

Open a Developer Command Prompt
From the start menu, look for x64 Native Tools Command Prompt for VS 2019.
Run the shortcut as administrator.
Once the developer command prompt is open, to activate the ROS 2 environment, run
```
c:\opt\ros\foxy\x64\setup.bat
```

##Isaac Sim
You will need to do the following to activate a ROS2 command prompt for windows.

From the start menu, look for x64 Native Tools Command Prompt for VS 2019.

Run the shortcut as administrator.

Once the developer command prompt is open, run 
```
c:\opt\ros\foxy\x64\setup.bat
```

Run
```
set FASTRTPS_DEFAULT_PROFILES_FILE=C:\Users\yadun\AppData\Local\ov\pkg\isaac_sim-2022.2.1\ros2_workspace\fastdds.xml
```
Change the path according to where it is stored in your system.

Run
```
cd C:\Users\yadun\AppData\Local\ov\pkg\isaac_sim-2022.2.1
```

Run 
```
isaac-sim.bat
```
Enable omni.isaac.ros2_bridge from the extension manager window.
