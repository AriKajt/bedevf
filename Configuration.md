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

----------------------------------------------------------------
Debugging HyperV:
----------------------------------------------------------------
If you cant see any created Virual Machines under Hyper V Manager:
    a) Open Hyper-V Manager.
    b) In the menu, click on Action in the top-left corner.
    c) Choose Connect to Server.
    d)In the dialog box that appears:
        Choose Local Computer.
        Click OK.
    If you encounter error: Virtual Machine Management Service" (VMMS) is not running, do this:
    a) Start the Virtual Machine Management Service
    b) Press Windows + R to open the Run dialog box.
    c) Type services.msc and press Enter. This will open the Services window.
    d) Scroll down and locate the service named Hyper-V Virtual Machine Management.
    e) Check the service status:
        If it is not running, right-click on it and choose Start.
        If it’s already running, right-click and select Restart.

Failed unmounting /cdrom:
    a) Force shutdown through HyperV Management:
       1 - Right-click on the virtual machine in Hyper-V Manager 
            (e.g.,"AlgebraTest").
       2 - Select Turn Off. This is like forcing the power off 
            on a physical machine—use it if a normal shutdown fails. 
    b) Remove the Installation Media:
        1 - In Hyper-V Manager, right-click on the VM (e.g., "AlgebraTest") and  select Settings.
        2 - Go to the SCSI Controller or IDE Controller (where the CD/DVD drive is configured).
        3 - Find the virtual DVD drive that has the Ubuntu ISO attached.
        4 - Remove the mounted ISO by selecting None or simply unmount it by choosing Empty.
        5 - Restart the Virtual Machine.
----------------------------------------------------------------

----------------------------------------------------------------
Installing WSL
----------------------------------------------------------------
- Open PowerShell as Administrator:
    Right-click the Start button and select Windows PowerShell (Admin).
- Enable WSL:
    Run the following command in PowerShell to enable WSL and install the default Linux distribution (Ubuntu):

        wsl --install

- Install Ubuntu from the Microsoft Store:
    a) Go to the Microsoft Store, search for "Ubuntu", and choose the latest version (e.g., Ubuntu 22.04).
    b) Install it and launch it from the Start Menu.

- Configure Ubuntu:
    After installing Ubuntu, it will launch a terminal. You’ll be asked to create a username and password for your Linux user account.
----------------------------------------------------------------

----------------------------------------------------------------
Installing Apache:
----------------------------------------------------------------
1 - Update the system:

        sudo apt update

        sudo apt upgrade -y
        
2 - Install Apache Web Server:
        sudo apt install apache2

Common commands for Apache:
        sudo systemctl status apache2 # Check status of Apache
        sudo systemctl start apache2  # Start Apache
        sudo systemctl stop apache2   # Stop Apache
        sudo systemctl restart apache2 # Restart Apache

After installation, you can check if Apache is running 
by visiting http://localhost in your Windows browser.
----------------------------------------------------------------

----------------------------------------------------------------
Installing PHP:
----------------------------------------------------------------
1 - Update the system:
        sudo apt update
        sudo apt upgrade -y
2 - You will need to install PHP and the Apache PHP module:
        sudo apt install php libapache2-mod-php php-mysql
    a) To check if PHP is installed, create a test file:
            sudo nano /var/www/html/info.php
    b) Add the following content:
            <?php
            phpinfo();
            ?>
    Save and exit (CTRL + X, then Y and Enter).
    c) Then open your browser and visit http://localhost/info.php. 
    If PHP is installed correctly, you'll see a page with detailed information about your PHP configuration.
----------------------------------------------------------------

----------------------------------------------------------------
Installing MySQL:
----------------------------------------------------------------
1 - To install MySQL, run:
    sudo apt install mysql-server
2 - After installation, secure your MySQL installation:
        sudo mysql_secure_installation
    (Follow the prompts to set a root password and secure your MySQL setup.)
3 - Start MySQL:
        sudo systemctl start mysql
4 - To check if MySQL is running, use:
        sudo systemctl status mysql
5 - To access MySQL:
        sudo mysql -u root -p
----------------------------------------------------------------

----------------------------------------------------------------
Configure PHP-APACHE-MySQL connection
----------------------------------------------------------------
1 - Configure Apache to Use PHP:
    - Apache should already be set up to run PHP, but you can check and configure it to ensure everything is working fine.
    - You can edit the Apache configuration file /etc/apache2/apache2.conf or any specific virtual host file in /etc/apache2/sites-available/.
2 - Create a Virtual Host for Your Project:
    a) If you are working on a specific project, it’s helpful to create a virtual host. For example, to set up a local environment for a project:
        sudo nano /etc/apache2/sites-available/myproject.conf
    b) Add the following content (replace myproject and the paths as necessary):

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

    c) Then enable the new site and reload Apache:
            sudo a2ensite myproject.conf
            sudo systemctl reload apache2

    d) ! You’ll need to modify your hosts file in Windows to point myproject.local to 127.0.0.1. 
    - Open C:\Windows\System32\drivers\etc\hosts and add:
            127.0.0.1 myproject.local
    e) Enable .htaccess for Apache:
        In your project directory (/var/www/html/myproject), you can now use .htaccess files for URL rewrites or custom rules. Make sure you’ve set AllowOverride All in the Apache configuration, as shown earlier.

        TEST complete stack:
        - Open a browser and go to http://localhost. You should see the Apache default page.
        - For your PHP testing, go to http://localhost/info.php.
        - For MySQL, try accessing the database via the MySQL command line:
            mysql -u root -p
----------------------------------------------------------------

----------------------------------------------------------------
Installing Composer for PHP 
----------------------------------------------------------------
Composer is a dependency manager for PHP, useful for managing libraries and packages in your projects. You can install it globally on WSL by running the following:
    sudo apt install curl php-cli php-mbstring git unzip
    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer
----------------------------------------------------------------


----------------------------------------------------------------
Installing LAMP
----------------------------------------------------------------
1 - Update the Package List:
    sudo apt update
2 - Install Apache, MySQL, and PHP:
    sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y
This command installs:
        Apache web server
        MySQL database server
        PHP (along with necessary modules for Apache to run PHP)
4 - Confirm the status of Apache and MySQL:
    sudo systemctl status apache2
    sudo systemctl status mysql

Verify installation:
Check Apache:
    Open a browser on your Windows machine and go to http://localhost.
    If Apache is installed correctly, you should see the Apache default page.
Check PHP:
    Create a PHP info file to verify PHP is working.
    sudo nano /var/www/html/info.php
    Add the following content:
    <?php
    phpinfo();
    ?>
    Save the file (CTRL + X, then Y and Enter).
    Open http://localhost/info.php in your browser. If everything is installed correctly, you’ll see a detailed PHP information page.
Check MySQL:
    To log into MySQL:
        sudo mysql -u root -p
    Set up your root password and verify that you’re inside MySQL by checking the prompt:

    mysql> SHOW DATABASES;

Configure Apache
If you’re working on a specific project, you can configure Apache to serve your project directory by editing the default site configuration or creating a new one.
    Edit the default site config file:
        sudo nano /etc/apache2/sites-available/000-default.conf
    Set the DocumentRoot to your project folder, for example:
        DocumentRoot /var/www/html/myproject
    Restart Apache:
        sudo systemctl restart apache2

Enable .htaccess for Apache
If you want to use .htaccess files for custom configurations (e.g., URL rewrites), ensure that the Apache configuration allows overrides. In /etc/apache2/sites-available/000-default.conf, ensure this block is set as follows:
    <Directory /var/www/html>
    AllowOverride All
    </Directory>

    Then restart Apache:
        sudo systemctl restart apache2
----------------------------------------------------------------

----------------------------------------------------------------
Working with linux terminal:
----------------------------------------------------------------
File System Navigation
        ls – Lists files and directories.
            ls       # List all files in current directory
            ls -l    # List with detailed info
            ls -a    # List all files, including hidden ones
        cd – Change directory.
            cd /path/to/directory    # Navigate to a directory
            cd ..                    # Go up one directory level
            cd ~                     # Go to home directory
 File and Directory Management
        touch – Create an empty file.
            touch filename.txt
        mkdir – Create a new directory.
            mkdir directory_name
        rm – Remove a file.
            rm file_name
            rm -r directory_name  # Remove a directory and its contents
        rmdir – Remove an empty directory.
            rmdir directory_name
        cp – Copy files or directories.
            cp file_name destination/
            cp -r dir_name destination/  # Copy a directory recursively
        mv – Move or rename files.
            mv old_name new_name        # Rename a file
            mv file_name /path/to/destination/  # Move a file
        cat – Display the contents of a file.
            cat file_name
        nano – Edit a file with a simple terminal-based text editor.
            nano file_name
        vim – Edit a file with the Vim text editor.
            vim file_name
File Permissions
    chmod – Change file permissions.
        chmod 755 file_name      # Give read, write, and execute permissions to owner
        chmod +x file_name       # Add execute permission
        chmod -r 644 file_name   # Remove write permission for group and others
    chown – Change file ownership.
        sudo chown user:group file_name
Network Management
    ssh – Secure shell to connect to a remote server.
        ssh username@hostname_or_ip
Package Management (Debian/Ubuntu-based systems)
    apt update – Update the package list.
        sudo apt update
    apt upgrade – Upgrade all installed packages.
        sudo apt upgrade
    apt install – Install a package.
        sudo apt install package_name
    apt remove – Remove a package.
        sudo apt remove package_name
Sudo and User Management
    sudo – Run commands with superuser privileges.
        sudo command
    adduser – Add a new user.
        sudo adduser new_user
    passwd – Change user password.
        sudo passwd user_name
Other Useful Commands
    history – Show command history.
        history

Helpful Shortcuts
    Ctrl + C – Terminate a running command.
    Ctrl + Z – Suspend a running command.
    Ctrl + D – Log out from the terminal.
    Tab – Autocomplete file and directory names.
----------------------------------------------------------------

----------------------------------------------------------------
Configuring GIT:
----------------------------------------------------------------
1. Install Git
Download Git:

Go to the Git for Windows download page and download the installer.
[text](https://gitforwindows.org/)

Install Git:
- Run the installer and follow the installation instructions.
- Choose the default options unless you have specific needs.
- Make sure to select "Use Git from the command line and also from 3rd-party software" during installation.

2. Verify the Installation:

- Open Command Prompt or PowerShell.
Run:
git --version
(If Git is installed correctly, you should see the Git version number.)

3. Configure Git in VS Code
- Open VS Code.
- Press Ctrl + Shift + P to open the Command Palette.
- Type Git: Enable and select Git: Enable if it’s not already enabled.

4. Configure Git User Information
- Open the Terminal in VS Code:
    	Go to View > Terminal or press Ctrl + ` (backtick).
a) Set your Git username and email:
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"

Working with repository:
1. Initialize repository from VS code:
a) Create repository in VS code
b) Initialize the Git Repository:
    - Click on the Source Control icon in the sidebar (or press Ctrl + Shift + G).
    - Click Initialize Repository.
        This will create a .git folder in your project directory, indicating that it's now a Git repository.
c) Create a .gitignore File (Optional):
    - If you want to exclude certain files or folders from being tracked, create a .gitignore file.
    - Right-click in the file explorer, select New File, and name it .gitignore.
    - Add file/folder patterns you want to exclude, e.g.:
                            node_modules/
                            .env
                            *.log
d) Stage Changes:
    - Make some changes or create a new file.
    - In the Source Control panel, you’ll see a list of modified files.
    - Click the + (plus) icon next to the file to stage it or click + next  to the Changes label to stage all changes

e) Commit Changes:
    - Enter a commit message in the input box at the top of the Source Control panel (e.g., "Initial commit").
    - Click the ✔ (checkmark) icon to commit the changes.
e) Create a New GitHub Repository from VS Code
1. Install GitHub Extension (Optional):
    - Go to the Extensions view (Ctrl + Shift + X).
    - Search for "GitHub Repositories" and install it.
2. Sign In to GitHub
    - In VS Code, open the Command Palette with Ctrl + Shift + P.
    - Type "Sign In to GitHub" and select it.
    - Follow the instructions to authenticate with GitHub.
3. Add Remote to GitHub:
    - Open the Command Palette with Ctrl + Shift + P.
    - Type "Publish to GitHub" or "Git: Publish to GitHub" and select it.
    - If you are signed in to GitHub, VS Code will prompt you to create a new GitHub repository.
    - Enter a repository name when prompted (or keep the default folder name).
    - Choose whether to make the repository public or private.
4. Push Local Repository to GitHub:
    - After setting up the repository name, VS Code will automatically add the GitHub remote and push your local commits.
    - You should see a message indicating that the repository was successfully published.




2. Create repository manually on Github, push to Github from local:

a) Create a New Repository on GitHub:
- Go to GitHub and sign in.
- Click the + icon in the top right corner and select New Repository.
- Fill out the repository name and other details.
- Choose Public or Private.
- DO NOT initialize with a README if you already have a local repository.
b) Add GitHub Remote to VS Code:
- In VS Code, open the terminal (Ctrl + `).
- Add the remote URL of the GitHub repository:
    git remote add origin https://github.com/YourUsername/YourRepoName.git
- Verify the remote URL is set correctly:
    git remote -v
c) Push Local Repository to GitHub:
- Push your local commits to GitHub:
    git push -u origin main
- If your default branch is master, use:
    git push -u origin master
(The -u flag sets the upstream branch so you can use git push without specifying origin main next time.)
d) Confirm Your Changes on GitHub



2. Clone already created repository from Github:
- Get the SSH URL:
    Go to the repository on GitHub and copy the SSH URL (e.g., git@github.com:YourUsername/YourRepoName.git).
- Clone the Repository:
    git clone git@github.com:YourUsername/YourRepoName.git
- Open the Cloned Folder in VS Code:
    You can use the File > Open Folder menu to navigate to the cloned folder or use the terminal command:
       code YourRepoName
(Replace YourRepoName with the name of the cloned folder.)



Working with GIT - GENERAL:

Fetch, Pull, and Push Changes
- Fetch: Get updates from GitHub without merging
- Pull: Get updates from GitHub and merge them with your local repository.
- Push: Send your local commits to GitHub.
Commands:
    (Ctrl + Shift + P), type Git: Fetch and select it.
    git pull
    git push

Creating and Switching Branches

A) Create a New Branch:
    git checkout -b new-branch-name
OR
    Press Ctrl + Shift + P and type Git: Create Branch.

B) Switch Branches:
    (Ctrl + Shift + P) and type Git: Checkout to to switch branches.

C) Push a New Branch to GitHub:
    git push -u origin new-branch-name

Authentification with SSH:
1) Open the Terminal in VS Code
 - Open the integrated terminal by pressing Ctrl + ` (the backtick key, below Esc on most keyboards) or by going to View > Terminal.
2) Check for Existing SSH Keys
- Check if you have existing SSH keys:
    ls -al ~/.ssh
If you see files like id_rsa and id_rsa.pub, you already have an SSH key. If so, skip to step 4. If not, continue to the next step.
3) Generate a New SSH Key
- Generate the SSH key:
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
(Replace "your_email@example.com" with your GitHub email address.)
- You’ll be prompted to specify a file location to save the key:
 Press Enter to use the default location (~/.ssh/id_rsa).
Optionally, add a passphrase for extra security. Press Enter if you don’t want to set a passphrase.
4) Start the SSH Agent:
    eval "$(ssh-agent -s)"
- Add the SSH key to the agent:
    ssh-add ~/.ssh/id_rsa
(If you used a custom name for your SSH key (e.g., github_id_rsa), replace id_rsa with that name.)
5) Add the SSH Key to Your GitHub Account
- Copy the SSH public key to the clipboard:
    cat ~/.ssh/id_rsa.pub
Copy the output that starts with ssh-rsa. You can also use the clip command to directly copy to the clipboard if you are on Windows:
    clip < ~/.ssh/id_rsa.pub
- Add the Key to GitHub:
    Go to GitHub and log in.
    Click on your profile picture in the top right corner and go to Settings.
    In the left sidebar, click on SSH and GPG keys.
    Click on the New SSH key button.
    Add a Title (e.g., "VS Code SSH Key") and paste the SSH key into the Key field.
    Click Add SSH key.
6) Test the SSH Connection to GitHub
- In the VS Code terminal, test the SSH connection:
    ssh -T git@github.com
If successful, you should see a message like:
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
7) Set Up Git Configurations in VS Code
- Set your GitHub username and email:
    git config --global user.name "Your GitHub Username"
    git config --global user.email "your_email@example.com"
- Check your configurations:
    git config --list
