Setting Up a Working Environment on a Virtual Machine using Hyper-V
Note: Hyper-V is available on Windows: Pro/Enterprise/Education editions.

1. Enable Hyper-V
Open Control Panel:
Start Menu → Type "Turn Windows features on or off".
Enable Hyper-V (checkbox) - ensure "Hyper-V Management Tools" and "Hyper-V Platform" are also enabled.
Click OK and restart your computer.
2. Create a New Virtual Machine in Hyper-V
Open Hyper-V Manager:
Search "Hyper-V Manager" in the Start Menu.
Create a New VM:
On the right panel, click on New → Virtual Machine.
Follow the New Virtual Machine Wizard steps:
Specify Name and Location:
Name your virtual machine (e.g., "UbuntuServer").
Optionally, specify a location to save VM files.
Specify Generation:
Choose Generation 1 for compatibility issues.
Choose Generation 2 for modern Ubuntu versions (recommended).
Assign Memory:
Allocate at least 2048 MB (2 GB).
Configure Networking:
Select the Virtual Switch (e.g., “Default Switch”) for network access.
Connect Virtual Hard Disk:
Choose Create a virtual hard disk and specify the size (e.g., 20 GB or more).
Installation Options:
Choose Install an operating system from a bootable image file.
Browse and select the Ubuntu Server ISO file.
Click Finish to create the VM.
3. Configure the Virtual Machine
Right-click on the newly created VM → select Settings.
Processor: Increase the number of virtual processors if supported (e.g., 2 or 4).
Network Adapter: Ensure it’s connected to the correct virtual switch.
Security: Disable Secure Boot if you encounter ISO compatibility issues.
Additional Hard Drives: Add more virtual hard drives under the SCSI Controller if needed.
4. Start the Virtual Machine and Install Ubuntu Server
In Hyper-V Manager, right-click on the virtual machine and select Connect.

In the new window, click Start (green button) to boot the VM from the Ubuntu Server ISO.

Follow the Ubuntu Server installation prompts:

Language: Select and press Enter.
Keyboard Layout: Choose your keyboard layout.
Network Configuration: Should obtain IP automatically via DHCP. Configure manually if necessary.
Storage Configuration: Choose Use an Entire Disk and select the virtual hard disk.
Profile Setup: Enter your name, server name, username, and password.
SSH Server: Select Install OpenSSH Server if needed.
Featured Server Snaps: Choose additional software (optional).
Once the installation is complete, the VM will prompt you to restart.

5. Post-Installation Configuration
Log in using the username and password you created.
Update the Server:
bash
Copy code
sudo apt update && sudo apt upgrade -y
Install Additional Software (if needed):
OpenSSH (if not installed during setup):
bash
Copy code
sudo apt install openssh-server
Other essential packages:
bash
Copy code
sudo apt install net-tools curl vim
6. Accessing the Server
Use the Hyper-V console to interact directly with the server.
If you installed SSH, connect from your host machine:
bash
Copy code
ssh username@server-ip
Replace username with your username and server-ip with the IP address of the virtual machine.
Debugging Hyper-V
If You Can't See Any Created Virtual Machines in Hyper-V Manager:
Open Hyper-V Manager.
Click on Action in the top-left menu.
Choose Connect to Server.
Select Local Computer and click OK.
If You Encounter the Error: "Virtual Machine Management Service" (VMMS) is Not Running:
Start the Virtual Machine Management Service:
Press Windows + R → type services.msc → press Enter.
Find Hyper-V Virtual Machine Management in the Services window.
Check service status:
If not running, right-click and choose Start.
If already running, right-click and select Restart.
Error: Failed Unmounting /cdrom
Force Shutdown:
Right-click the virtual machine in Hyper-V Manager (e.g., "AlgebraTest") → select Turn Off.
Remove Installation Media:
In Hyper-V Manager, right-click the VM → select Settings.
Go to SCSI Controller or IDE Controller → find the virtual DVD drive with the Ubuntu ISO attached.
Unmount the ISO (choose None or Empty).
Restart the Virtual Machine.
Installing WSL (Windows Subsystem for Linux)
Open PowerShell as Administrator:
Right-click the Start button and select Windows PowerShell (Admin).
Enable WSL:
bash
Copy code
wsl --install
Install Ubuntu from the Microsoft Store:
Go to the Microsoft Store, search for "Ubuntu", and install the latest version.
Launch Ubuntu from the Start Menu and set up your Linux username and password.
Installing Apache
Update the System:

bash
Copy code
sudo apt update
sudo apt upgrade -y
Install Apache Web Server:

bash
Copy code
sudo apt install apache2
Common Apache Commands
Check status:
bash
Copy code
sudo systemctl status apache2
Start Apache:
bash
Copy code
sudo systemctl start apache2
Stop Apache:
bash
Copy code
sudo systemctl stop apache2
Restart Apache:
bash
Copy code
sudo systemctl restart apache2