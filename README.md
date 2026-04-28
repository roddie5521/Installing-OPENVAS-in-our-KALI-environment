### Installing-OPENVAS-in-our-KALI-environment
This piece will help us know how to quickly install __OPENVAS__ in our test or dev environment. OpenVAS helps quickly uncover gaps across both production and development environments.


OpenVAS is an open-source vulnerability scanning tool designed to assess endpoints, web applications, and networked systems for security weaknesses. It enables security professionals and system administrators to detect, analyze, and remediate vulnerabilities before they can be exploited. Widely adopted by organizations as part of their risk management strategy, OpenVAS helps quickly uncover gaps across both production and development environments.

The tool can be deployed using Docker or installed directly on operating systems such as Ubuntu or Debian. In this setup, we will install OpenVAS on Kali Linux within a virtualized environment.

### Prerequisites for Installing OpenVAS
Before proceeding with the installation of OpenVAS, it’s important to ensure that your system meets the following prerequisites:
1. __A Linux-based OS__
OpenVAS is primarily designed for Linux environments. It can run on most modern distributions, including:
Ubuntu/Debian-based distributions (e.g., Ubuntu, Linux Mint, Debian)
CentOS/RHEL-based distributions (e.g., CentOS, Fedora, Rocky Linux, AlmaLinux)
2. __Sufficient Resources__
OpenVAS requires sufficient system resources to perform vulnerability scans, especially for large networks. For optimal performance, it’s recommended to have:

At least 2GB of RAM (4GB or more for larger environments)
A multi-core processor (2 or more cores)
Around 10GB of free disk space (for storing databases and scan results)

3. __Root or Sudo Privileges__
Installation requires root or sudo access, as you will need to install packages and manage system configurations.

4. __Internet Connection__
Since OpenVAS requires downloading a range of dependencies, updates, and vulnerability tests, an internet connection is necessary during the installation process.

### Installing Openvas on Kali Linux
To install Openvas and its dependencies on our Kali Linux system run the following command:
__sudo apt update__                      
__sudo apt upgrade -y__
__sudo apt dist-upgrade -y__

<>

The next step is to run the installer, which will configure OpenVAS and download various network vulnerability tests (NVT) or signatures. Due to a large number of NVTs (50.000+),  the setting process may take some time and consume a lot of data. In the test setup we used for this tutorial, the complete setup process took 10 minutes, which is not bad.

__sudo apt install openvas__

<>

Run the following command to start the setup process:
__gvm-setup__

<>

After the configuration process is complete, all the necessary OpenVAS processes will start and the web interface will open automatically. 
The web interface is running locally on port 9392 and can be accessed through https://localhost:9392. 

OpenVAS will also set up an admin account and automatically generate a password for this account which is displayed in the last section of the setup output:

### Verify the Installation
You can verify your installation with.

__gvm-check-setup__

<>

### Password reset
Did you forget to note down the password? You can change the admin password using the following commands:

__gvmd --user=admin --new-password=passwd;__

The next step is to accept the self-signed certificate warning and use the automatically generated admin credentials to login on to the web interface:

<>

### Starting and stopping OpenVAS
Before starting to install the virtual appliance, the last step I have to consider is to start and stop the OpenVAS service. 
OpenVAS services consume a lot of unnecessary resources, so it is recommended that you disable these services when you are not using OpenVAS.
Run the following command to start the services:

__Sudo gvm-start__
 
To stop the OpenVAS services again, run:

__sudo gvm-stop__
 
### *Note: To create a new user :

**sudo runuser -u _gvm -- gvmd --create-user=admin2 --new-password=12345**


To change the password of the existing user:

**sudo runuser -u _gvm -- gvmd --user=admin --new-password=new_password**

### Configuration for a new target
Begin by navigating to Scans > Tasks and clicking on the purple magic wand icon to begin the basic configuration wizard. After successfully navigating to the wizard, you should see a pop-up window similar to the one shown above. You can set up the initial scan of the local host here to make sure everything is set up correctly.

Scanning may take a while. Please allow OpenVAS enough time to complete the scan. You will then see a new dashboard for monitoring and analyzing your completed and ongoing scans, as shown below.

<>

### Schedule the scanning process
Now that we know everything is normal, we can take a closer look at OpenVAS and how it works. Expand the car to scan and> start the task of creating a scan task for the managed computer.

### Creating a Task
To create a custom task, navigate to the star icon in the upper right corner of the taskbar and select New task.

<>

For this task, we'll be specializing only in the Name, Scan Targets, and Scanner Type, and Scan Config. In later tasks, we will be focusing on the opposite choices for additional advanced configuration and implementation/automation.
1.	Name: permits North American country to line the name the scan are going to be referred to as inside OpenVAS
2.	Scan Targets: The targets to scan, can embrace Hosts, Ports, and Credentials. to make a brand new target you may follow another pop-up, this can be lined later during this task.
3.	Scanner: The scanner to use by default will use the OpenVAS design but you'll be able to set this to any scanner of your selecting within the settings menu.
4.	Scan Config: OpenVAS has seven totally different scan sorts you can choose from and can be used supported however you're aggressive or what info you wish to gather from your scan.
### Assets
It permits visualizing the vulnerability of the parts akin to hosts or in operation systems:

<>

### Administration
As the name suggests, you can manage passwords, users, etc.:

<>


### Conclusion
You have successfully installed and configured OpenVAS on Kali Linux. With this powerful tool, you can now perform comprehensive vulnerability assessments and strengthen your security posture. Remember to only scan targets that belong to you or have legal permission to scan. If you found this guide helpful, please share it with others in the cybersecurity community.


