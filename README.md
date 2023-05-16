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

## Install WSL2

In the Start Menu, find the "x64 Native Tools Command Prompt for VS 2019" item.
Right Click, select More then "Run as Administrator"

```
wsl --install
```

Restart after installation.

Then run:
```
wsl --install -d Ubuntu-20.04
```
Setup username and password
Restart your computer to finish installation on Windows.

To login to the linux system in wsl
```
wsl --distribution Ubuntu-20.04 --user <user_name>
```
## Install Ros2 Foxy in WSL

Run the following commands.

```
sudo apt update
sudo apt upgrade
```
Make sure you have a locale which supports UTF-8
```
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```

Ensure that the Ubuntu Universe repository is enabled.
```
sudo apt install software-properties-common
sudo add-apt-repository universe
```
Now add the ROS 2 GPG key with apt.
```
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```
Then add the repository to your sources list.
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
Update your apt repository caches after setting up the repositories.

```
sudo apt update
sudo apt upgrade
```

Desktop Install (Recommended): ROS, RViz, demos, tutorials.
```
sudo apt install ros-foxy-desktop python3-argcomplete

```

Set up your environment by sourcing the following file.
```
# Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/foxy/setup.bash
```

Isaac sim is already connected to ROS2 Foxy installed in windows. ROS2 Foxy in the Linux system would automatically communicate with its version in windows. verify it using the following commands.

Run in Linux (wsl) terminal:
```
source /opt/ros/foxy/setup.bash
ros2 run demo_nodes_cpp talker
```
Run in windows terminal:
```
c:\opt\ros\foxy\x64\setup.bat
ros2 run demo_nodes_py listener
```

You can see the data published in wsl terminal in windows terminal.

