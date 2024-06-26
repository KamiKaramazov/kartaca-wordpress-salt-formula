# Installing and setting up Vagrant on Windows 10
### 1) Install [VirtualBox](https://www.virtualbox.org/).
### 2) Install [Vagrant](https://www.vagrantup.com/).
### 3) Create a file and test the server:
1. Create a file named ``My_First_Vagrant`` then open a terminal inside the file directory and execute the following command to initialize the Vagrant environment:

    ``
    vagrant init generic/ubuntu2204
    ``

    ![image1](Images\image1.png)

2. Execute the following command to download the virtual machine. This process may take some time to complete:

    ``
    vagrant up
    ``

3. Once the machine is downloaded, connect to the machine via SSH by executing the following command:

    ``
    vagrant ssh
    ``

    ![image2](Images\image2.png)

4. Once connected, print the system information using the following command:

    ``
    uname -a
    ``

5. To shut down the virtual machine, execute the following command:

    ``
    vagrant halt
    ``

These steps ensure that the Vagrant environment is set up correctly and can be used reliably.

### 3) Alternative Options
1. Download https://github.com/UtahDave/salt-vagrant-demo. You can use git or download a zip of the project directly from GitHub:

    ![image3](Images\image3.png)

2. Extract the zip file you downloaded, and then open a command prompt to the extracted directory:

    ``
    cd %homepath%\Downloads\salt-vagrant-demo-master
    ``

3. Run vagrant up to start the demo environment:

    ``
    vagrant up
    ``

---
# INSTALL SALTSTACK
>If you used the Vagrant project that is linked in the [previous section](https://docs.saltproject.io/en/getstarted/fundamentals/index.html), SaltStack is already installed and the connections to each minion are already accepted. You can complete the tasks in the *Accept Connections* below to verify that your minions are connected.

If you want to change minions OS just edit the `Vagrantfile` like this:

    ["minion1",    "#{net_ip}.11",    "1024",    os ],
    ["minion2",    "#{net_ip}.12",    "1024",    "generic/centos9s" ]


## ACCEPT CONNECTIONS

At the command prompt, cd into the vagrant-demo-master directory and run the following command to log in to your Salt master:

``
vagrant ssh master
``

After you connect, run the following command to become the root user:

``
sudo su
``

### VIEW ALL KEYS

On the Salt master, you can quickly view all Salt minion connections and view whether the connection is accepted, rejected, or pending.

``
salt-key --list-all
``

![image4](Images\image4.png)

*If **'salt-key'** not found, you can be installed with:*

``
apt install salt-master
``

If you don't saw the all minions try this command to check the minion activity:

``
salt-key --accept minion1
``

### ACCEPT A SPECIFIC KEY

Before a Salt minion can connect, you must accept its key.

``
salt-key --accept=<key>
``

### ACCEPT ALL KEYS

``
salt-key --accept-all
``