# Setting Up a Working Environment on a Virtual Machine using Hyper-V
**Note:** Hyper-V is available on Windows: Pro/Enterprise/Education editions.

## 1. Enable Hyper-V
1. Open Control Panel:
   - Start Menu → Type **"Turn Windows features on or off"**.
   - Enable **Hyper-V** (checkbox) - ensure "Hyper-V Management Tools" and "Hyper-V Platform" are also enabled.
   - Click **OK** and restart your computer.

## 2. Create a New Virtual Machine in Hyper-V
1. **Open Hyper-V Manager**:
   - Search **"Hyper-V Manager"** in the Start Menu.
2. **Create a New VM**:
   - On the right panel, click on **New → Virtual Machine**.
   - Follow the New Virtual Machine Wizard steps:
     1. **Specify Name and Location**:
        - Name your virtual machine (e.g., `"UbuntuServer"`).
        - Optionally, specify a location to save VM files.
     2. **Specify Generation**:
        - Choose **Generation 1** for compatibility issues.
        - Choose **Generation 2** for modern Ubuntu versions (recommended).
     3. **Assign Memory**:
        - Allocate at least **2048 MB (2 GB)**.
     4. **Configure Networking**:
        - Select the Virtual Switch (e.g., **“Default Switch”**) for network access.
     5. **Connect Virtual Hard Disk**:
        - Choose **Create a virtual hard disk** and specify the size (e.g., 20 GB or more).
     6. **Installation Options**:
        - Choose **Install an operating system from a bootable image file**.
        - Browse and select the Ubuntu Server ISO file.
   - Click **Finish** to create the VM.

## 3. Configure the Virtual Machine
1. Right-click on the newly created VM → select **Settings**.
   - **Processor**: Increase the number of virtual processors if supported (e.g., 2 or 4).
   - **Network Adapter**: Ensure it’s connected to the correct virtual switch.
   - **Security**: Disable Secure Boot if you encounter ISO compatibility issues.
   - **Additional Hard Drives**: Add more virtual hard drives under the SCSI Controller if needed.

## 4. Start the Virtual Machine and Install Ubuntu Server
1. In Hyper-V Manager, right-click on the virtual machine and select **Connect**.
2. In the new window, click **Start** (green button) to boot the VM from the Ubuntu Server ISO.
3. Follow the Ubuntu Server installation prompts:
   1. **Choose Language**: Select and press Enter.
   2. **Keyboard Layout**: Choose your keyboard layout.
   3. **Network Configuration**: Should obtain IP automatically via DHCP. Configure manually if necessary.
   4. **Storage Configuration**: Choose **Use an Entire Disk** and select the virtual hard disk.
   5. **Profile Setup**: Enter your name, server name, username, and password.
   6. **SSH Server**: Select **Install OpenSSH Server** if needed.
   7. **Featured Server Snaps**: Choose additional software (optional).
4. Once the installation is complete, the VM will prompt you to restart.

## 5. Post-Installation Configuration
1. Log in using the username and password you created.
   1. **Update the Server**:
      ```bash
      sudo apt update && sudo apt upgrade -y
      ```
   2. **Install Additional Software** (if needed):
      - OpenSSH (if not installed during setup):
        ```bash
        sudo apt install openssh-server
        ```
      - Other essential packages:
        ```bash
        sudo apt install net-tools curl vim
        ```

## 6. Accessing the Server
1. Use the Hyper-V console to interact directly with the server.
2. If you installed SSH, connect from your host machine:
   ```bash
   ssh username@server-ip
Replace username with your username and server-ip with the IP address of the virtual machine.

# Debugging Hyper-V

## If You Can't See Any Created Virtual Machines Under Hyper-V Manager
1. **Open Hyper-V Manager**.
2. In the menu, click on **Action** in the top-left corner.
3. Choose **Connect to Server**.
4. In the dialog box that appears:
   - Choose **Local Computer**.
   - Click **OK**.

### If You Encounter the Error: "Virtual Machine Management Service (VMMS) is Not Running"
1. **Start the Virtual Machine Management Service**:
   1. Press **Windows + R** to open the Run dialog box.
   2. Type `services.msc` and press Enter. This will open the Services window.
   3. Scroll down and locate the service named **Hyper-V Virtual Machine Management**.
   4. Check the service status:
      - If it is not running, right-click on it and choose **Start**.
      - If it’s already running, right-click and select **Restart**.

## Failed Unmounting /cdrom
1. **Force Shutdown Through Hyper-V Management**:
   1. Right-click on the virtual machine in Hyper-V Manager (e.g., "AlgebraTest").
   2. Select **Turn Off**. This is like forcing the power off on a physical machine—use it if a normal shutdown fails.
2. **Remove the Installation Media**:
   1. In Hyper-V Manager, right-click on the VM (e.g., "AlgebraTest") and select **Settings**.
   2. Go to the **SCSI Controller** or **IDE Controller** (where the CD/DVD drive is configured).
   3. Find the virtual DVD drive that has the Ubuntu ISO attached.
   4. Remove the mounted ISO by selecting **None** or simply unmount it by choosing **Empty**.
   5. Restart the Virtual Machine.

---

# Installing WSL (Windows Subsystem for Linux)

1. **Open PowerShell as Administrator**:
   - Right-click the Start button and select **Windows PowerShell (Admin)**.
2. **Enable WSL**:
   - Run the following command in PowerShell to enable WSL and install the default Linux distribution (Ubuntu):
     ```bash
     wsl --install
     ```
3. **Install Ubuntu from the Microsoft Store**:
   1. Go to the Microsoft Store, search for **"Ubuntu"**, and choose the latest version (e.g., Ubuntu 22.04).
   2. Install it and launch it from the Start Menu.
4. **Configure Ubuntu**:
   - After installing Ubuntu, it will launch a terminal. You’ll be asked to create a username and password for your Linux user account.

---

# Installing Apache

## 1. Update the System
    
    sudo apt update
    sudo apt upgrade -y
    

# 2 - Install Apache Web Server

To install Apache Web Server, run the following command:

       
        sudo apt install apache2
        

## Common commands for Apache:
- sudo systemctl status apache2  # Check status of Apache
- sudo systemctl start apache2   # Start Apache
- sudo systemctl stop apache2    # Stop Apache
- sudo systemctl restart apache2 # Restart Apache

After installation, you can check if Apache is running by visiting `http://localhost` in your Windows browser.

---

# Installing PHP

## 1 - Update the system:
```bash
sudo apt update
```
```bash
sudo apt upgrade -y
```

## 2 - You will need to install PHP and the Apache PHP module:
```bash
sudo apt install php libapache2-mod-php php-mysql
```

### Verify PHP Installation
a) Create a test file:
```bash
sudo nano /var/www/html/info.php
```

b) Add the following content:
```php
<?php
phpinfo();
?>
```

c) Save and exit (CTRL + X, then Y and Enter)

d) Open your browser and visit http://localhost/info.php. 
If PHP is installed correctly, you'll see a page with detailed information about your PHP configuration.

---

# Installing MySQL

1 - To install MySQL, run:
```bash
sudo apt install mysql-server
```

2 - After installation, secure your MySQL installation:
```bash
sudo mysql_secure_installation
```
(Follow the prompts to set a root password and secure your MySQL setup.)

3 - Start MySQL:
```bash
sudo systemctl start mysql
```

4 - To check if MySQL is running, use:
```bash
sudo systemctl status mysql
```

5 - To access MySQL:
```bash
sudo mysql -u root -p
```

---

# Configure PHP-APACHE-MySQL Connection

## 1 - Configure Apache to Use PHP:
- Apache should already be set up to run PHP, but you can check and configure it to ensure everything is working fine.
- You can edit the Apache configuration file `/etc/apache2/apache2.conf` or any specific virtual host file in `/etc/apache2/sites-available/`.

## 2 - Create a Virtual Host for Your Project:
a) If you are working on a specific project, it's helpful to create a virtual host:
```bash
sudo nano /etc/apache2/sites-available/myproject.conf
```

b) Add the following content (replace myproject and the paths as necessary):
```apache
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/myproject
    ServerName myproject.local

    <Directory /var/www/html/myproject>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

c) Then enable the new site and reload Apache:
```bash
sudo a2ensite myproject.conf
sudo systemctl reload apache2
```

d) Modify hosts file in Windows to point myproject.local to 127.0.0.1:
- Open `C:\Windows\System32\drivers\etc\hosts` and add:
```
127.0.0.1 myproject.local
```

e) Enable .htaccess for Apache:
In your project directory (`/var/www/html/myproject`), you can now use .htaccess files for URL rewrites or custom rules.

## Test Complete Stack:
- Open a browser and go to http://localhost
- For PHP testing, go to http://localhost/info.php
- For MySQL, try accessing the database via the MySQL command line:
```bash
mysql -u root -p
```

---

# Installing Composer for PHP 
```bash
sudo apt install curl php-cli php-mbstring git unzip
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

---

# Installing LAMP

1 - Update the Package List:
```bash
sudo apt update
```

2 - Install Apache, MySQL, and PHP:
```bash
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y
```

This installs:
- Apache web server
- MySQL database server
- PHP (with necessary modules for Apache)

3 - Confirm the status of Apache and MySQL:
```bash
sudo systemctl status apache2
sudo systemctl status mysql
```

# Verify Installation

## Check Apache
- Open browser on Windows machine
- Navigate to `http://localhost`
- Confirm Apache default page displays

## Check PHP
1. Create PHP info file:
```bash
sudo nano /var/www/html/info.php
```

2. Add content:
```php
<?php
phpinfo();
?>
```

3. Save file (CTRL + X, then Y and Enter)
4. Open `http://localhost/info.php`
5. Verify detailed PHP information page appears

## Check MySQL
1. Log into MySQL:
```bash
sudo mysql -u root -p
```

2. Verify databases:
```sql
mysql> SHOW DATABASES;
```

---

# Configure Apache

## Project Directory Configuration
1. Edit default site configuration:
```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

2. Set DocumentRoot:
```apache
DocumentRoot /var/www/html/myproject
```

3. Restart Apache:
```bash
sudo systemctl restart apache2
```

## Enable .htaccess
1. In configuration file, ensure:
```apache
<Directory /var/www/html>
    AllowOverride All
</Directory>
```

2. Restart Apache:
```bash
sudo systemctl restart apache2
```

---

# Linux Terminal Commands

## File System Navigation
- `ls`: List files/directories
  - `ls`: List all files in current directory
  - `ls -l`: Detailed listing
  - `ls -a`: Show hidden files

- `cd`: Change directory
  - `cd /path/to/directory`: Navigate to directory
  - `cd ..`: Go up one directory level
  - `cd ~`: Go to home directory

## File and Directory Management
- `touch filename.txt`: Create empty file
- `mkdir directory_name`: Create new directory
- `rm file_name`: Remove file
- `rm -r directory_name`: Remove directory and contents
- `rmdir directory_name`: Remove empty directory
- `cp file_name destination/`: Copy file
- `cp -r dir_name destination/`: Copy directory recursively
- `mv old_name new_name`: Rename file
- `mv file_name destination/`: Move file
- `cat file_name`: Display file contents

## Text Editors
- `nano file_name`: Simple terminal-based editor
- `vim file_name`: Advanced terminal editor

## File Permissions
- `chmod 755 file_name`: Give read/write/execute to owner
- `chmod +x file_name`: Add execute permission
- `chmod -r 644 file_name`: Remove write permission

## File Ownership
- `sudo chown user:group file_name`: Change file ownership

## Network Management
- `ssh username@hostname_or_ip`: Secure shell to remote server

## Package Management
- `sudo apt update`: Update package list
- `sudo apt upgrade`: Upgrade installed packages
- `sudo apt install package_name`: Install package
- `sudo apt remove package_name`: Remove package

## User Management
- `sudo command`: Run with superuser privileges
- `sudo adduser new_user`: Add new user
- `sudo passwd user_name`: Change user password

## Other Commands
- `history`: Show command history

## Helpful Shortcuts
- `Ctrl + C`: Terminate running command
- `Ctrl + Z`: Suspend running command
- `Ctrl + D`: Log out from terminal
- `Tab`: Autocomplete file/directory names

# Configuring GIT

## 1. Install Git

### Download Git
Go to the [Git for Windows download page](https://gitforwindows.org/) and download the installer.

### Install Git
- Run the installer and follow the installation instructions
- Choose the default options unless you have specific needs
- Make sure to select "Use Git from the command line and also from 3rd-party software" during installation

## 2. Verify the Installation

- Open Command Prompt or PowerShell
- Run:
```bash
git --version
```
(If Git is installed correctly, you should see the Git version number.)

## 3. Configure Git in VS Code
- Open VS Code
- Press `Ctrl + Shift + P` to open the Command Palette
- Type Git: Enable and select Git: Enable if it's not already enabled

## 4. Configure Git User Information
- Open the Terminal in VS Code:
    Go to View > Terminal or press `Ctrl + ` ` (backtick)
- Set your Git username and email:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Working with Repository

### 1. Initialize Repository from VS Code
a) Create repository in VS Code
b) Initialize the Git Repository:
    - Click on the Source Control icon in the sidebar (or press `Ctrl + Shift + G`)
    - Click Initialize Repository
        This will create a .git folder in your project directory, indicating that it's now a Git repository

c) Create a .gitignore File (Optional):
    - If you want to exclude certain files or folders from being tracked, create a .gitignore file
    - Right-click in the file explorer, select New File, and name it .gitignore
    - Add file/folder patterns you want to exclude, e.g.:
```
node_modules/
.env
*.log
```

d) Stage Changes:
    - Make some changes or create a new file
    - In the Source Control panel, you'll see a list of modified files
    - Click the + (plus) icon next to the file to stage it or click + next to the Changes label to stage all changes

e) Commit Changes:
    - Enter a commit message in the input box at the top of the Source Control panel (e.g., "Initial commit")
    - Click the ✔ (checkmark) icon to commit the changes

### Create a New GitHub Repository from VS Code
1. Install GitHub Extension (Optional):
    - Go to the Extensions view (`Ctrl + Shift + X`)
    - Search for "GitHub Repositories" and install it

2. Sign In to GitHub:
    - In VS Code, open the Command Palette with `Ctrl + Shift + P`
    - Type "Sign In to GitHub" and select it
    - Follow the instructions to authenticate with GitHub

3. Add Remote to GitHub:
    - Open the Command Palette with `Ctrl + Shift + P`
    - Type "Publish to GitHub" or "Git: Publish to GitHub" and select it
    - If you are signed in to GitHub, VS Code will prompt you to create a new GitHub repository
    - Enter a repository name when prompted (or keep the default folder name)
    - Choose whether to make the repository public or private

4. Push Local Repository to GitHub:
    - After setting up the repository name, VS Code will automatically add the GitHub remote and push your local commits
    - You should see a message indicating that the repository was successfully published

## 2. Create Repository Manually on Github, Push from Local

### A) Create a New Repository on GitHub
- Go to GitHub and sign in
- Click the + icon in the top right corner and select New Repository
- Fill out the repository name and other details
- Choose Public or Private
- DO NOT initialize with a README if you already have a local repository

### B) Add GitHub Remote to VS Code
- In VS Code, open the terminal (`Ctrl + ` `)
- Add the remote URL of the GitHub repository:
```bash
git remote add origin https://github.com/YourUsername/YourRepoName.git
```
- Verify the remote URL is set correctly:
```bash
git remote -v
```

### C) Push Local Repository to GitHub
- Push your local commits to GitHub:
```bash
git push -u origin main
```
- If your default branch is master, use:
```bash
git push -u origin master
```
(The -u flag sets the upstream branch so you can use git push without specifying origin main next time.)

### D) Confirm Your Changes on GitHub

## Clone Already Created Repository from Github
- Get the SSH URL:
    Go to the repository on GitHub and copy the SSH URL (e.g., `git@github.com:YourUsername/YourRepoName.git`)
- Clone the Repository:
```bash
git clone git@github.com:YourUsername/YourRepoName.git
```
- Open the Cloned Folder in VS Code:
    You can use the File > Open Folder menu to navigate to the cloned folder or use the terminal command:
```bash
code YourRepoName
```
(Replace YourRepoName with the name of the cloned folder.)

## Working with GIT - GENERAL

### Fetch, Pull, and Push Changes
- **Fetch**: Get updates from GitHub without merging
- **Pull**: Get updates from GitHub and merge them with your local repository
- **Push**: Send your local commits to GitHub

Commands:
```bash
(Ctrl + Shift + P), type Git: Fetch and select it
git pull
git push
```

### Creating and Switching Branches

#### A) Create a New Branch
```bash
git checkout -b new-branch-name
```
OR
Press `Ctrl + Shift + P` and type Git: Create Branch

#### B) Switch Branches
Press `Ctrl + Shift + P` and type Git: Checkout to switch branches

#### C) Push a New Branch to GitHub
```bash
git push -u origin new-branch-name
```

## Authentication with SSH

### 1) Open the Terminal in VS Code
 - Open the integrated terminal by pressing `Ctrl + ` ` (the backtick key, below Esc on most keyboards) or by going to View > Terminal

### 2) Check for Existing SSH Keys
- Check if you have existing SSH keys:
```bash
ls -al ~/.ssh
```
If you see files like id_rsa and id_rsa.pub, you already have an SSH key. If so, skip to step 4. If not, continue to the next step.

### 3) Generate a New SSH Key
- Generate the SSH key:
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
(Replace "your_email@example.com" with your GitHub email address.)
- You'll be prompted to specify a file location to save the key:
 Press Enter to use the default location (~/.ssh/id_rsa)
Optionally, add a passphrase for extra security. Press Enter if you don't want to set a passphrase.

### 4) Start the SSH Agent
```bash
eval "$(ssh-agent -s)"
```
- Add the SSH key to the agent:
```bash
ssh-add ~/.ssh/id_rsa
```
(If you used a custom name for your SSH key (e.g., github_id_rsa), replace id_rsa with that name.)

### 5) Add the SSH Key to Your GitHub Account
- Copy the SSH public key to the clipboard:
```bash
cat ~/.ssh/id_rsa.pub
```
Copy the output that starts with ssh-rsa. You can also use the clip command to directly copy to the clipboard if you are on Windows:
```bash
clip < ~/.ssh/id_rsa.pub
```

- Add the Key to GitHub:
    - Go to GitHub and log in
    - Click on your profile picture in the top right corner and go to Settings
    - In the left sidebar, click on SSH and GPG keys
    - Click on the New SSH key button
    - Add a Title (e.g., "VS Code SSH Key") and paste the SSH key into the Key field
    - Click Add SSH key

### 6) Test the SSH Connection to GitHub
- In the VS Code terminal, test the SSH connection:
```bash
ssh -T git@github.com
```
If successful, you should see a message like:
`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`

### 7) Set Up Git Configurations in VS Code
- Set your GitHub username and email:
```bash
git config --global user.name "Your GitHub Username"
git config --global user.email "your_email@example.com"
```
- Check your configurations:
```bash
git config --list
```




# XAMPP Configuration Instructions

To set up XAMPP so that your database, PHP, and VS Code files are connected and visible on `localhost`, follow these instructions:

## 1. **php.ini Configuration**
The `php.ini` file is the main configuration file for PHP. It is typically located in `C:\xampp\php\php.ini`. Here are some common settings to check or adjust:

- **Enable MySQL/MariaDB extensions**: Make sure these extensions are enabled (remove the semicolon `;` if they are commented out):
  ```ini
  extension=mysqli
  extension=pdo_mysql
  ```
- **Error Reporting**: To make debugging easier, you might want to enable error reporting:
  ```ini
  display_errors = On
  error_reporting = E_ALL
  ```

## 2. **httpd.conf (Apache Configuration)**
This file is located in `C:\xampp\apache\conf\httpd.conf`. Key settings include:

- **Document Root**: Make sure the document root points to the folder where your project files are. Look for:
  ```apache
  DocumentRoot "C:/xampp/htdocs"
  <Directory "C:/xampp/htdocs">
  ```
  If you are working on a specific project folder like `IntraConnect`, adjust it to:
  ```apache
  DocumentRoot "C:/xampp/htdocs/IntraConnect"
  <Directory "C:/xampp/htdocs/IntraConnect">
  ```

- **Port Settings**: By default, XAMPP uses port 80. If you need to change it, update:
  ```apache
  Listen 80
  ServerName localhost:80
  ```

## 3. **Virtual Hosts (Optional)**
If you want to set up a custom URL like `http://myproject.local`, you can edit the `httpd-vhosts.conf` file:
- This file is usually located at `C:\xampp\apache\conf\extra\httpd-vhosts.conf`.
- Add an entry like this:
  ```apache
  <VirtualHost *:80>
      DocumentRoot "C:/xampp/htdocs/IntraConnect"
      ServerName myproject.local
  </VirtualHost>
  ```
- Add the custom domain to your hosts file: Edit `C:\Windows\System32\drivers\etc\hosts` and add:
  ```
  127.0.0.1 myproject.local
  ```

## 4. **my.ini (MySQL Configuration)**
Located in `C:\xampp\mysql\bin\my.ini`. You don't usually need to make major changes here, but you can set the port if you have a custom configuration:
- Default MySQL port:
  ```ini
  port=3306
  ```

## 5. **VS Code Setup**
- **Open Project Folder**: In VS Code, open the project folder from `C:\xampp\htdocs\IntraConnect`.
- **PHP Debugging**: Install the PHP Debug extension in VS Code.
- **Live Server Extension**: If you want to preview changes in real-time, install the "Live Server" extension for VS Code. However, for PHP files, it's recommended to access them via `localhost` in your browser.

## 6. **Accessing Your Project**
- Open your browser and type `http://localhost/IntraConnect` (or `http://myproject.local` if you set up a virtual host).
- Your files should now be accessible, and PHP should connect to the database as configured in your PHP files.

