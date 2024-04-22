TASK:

(Deploy LAMP Stack)

Objective
- Automate the provisioning of two Ubuntu-based servers, named “Master” and “Slave”, using Vagrant.
- On the Master node, create a bash script to automate the deployment of a LAMP (Linux, Apache, MySQL, PHP) stack.
- This script should clone a PHP application from GitHub, install all necessary packages, and configure Apache web server and MySQL. 
- Ensure the bash script is reusable and readable.
- Using an Ansible playbook:
Execute the bash script on the Slave node and verify that the PHP application is accessible through the VM’s IP address (take screenshot of this as evidence)
Create a cron job to check the server’s uptime every 12 am.


SOLUTION:

Documentation of the steps taken to accomplish the above task.

`IP adresses`: Master : 192.168.33.24 and Slave : 192.168.33.25

1. `Set up master and slave VMs`: here, after initializing vagrant(vagrant init), I edited the vagrantfile with the "vi vagrantfile" command, I provisioned both the master and slave machines in one file.![Master and Slave VMS](./Provisioning%20two%20ubuntu-based%20servers.png)

2. `Validate vagrantfile` : after setting up the VMs, validate your vagrantfile to check for errors, then run "vagrant up" command.![](./Validation%20of%20vagrantfile.png)

3. `Vagrant setup`: run command: "vagrant ssh Master" to log in to the master node, You can run "vagrant ssh Slave" to log into the Slave node if you can split your screen to accomodate two terminals.

4. `Create and edit bashscript`:to create a bashscript, you can use the touch command e.g (touch lamp.sh) and use  (vi lamp.sh) or (nano lamp.sh) to edit bashscript and work on it.![](./lamp.sh)

5. `Generate ssh keys`: ssh keys are generated to link machines together OR to link slave node to the masternode. The ssh key is generated from the master node with command (ssh-keygen) and can be located in the id_rsa.pub file.![](./Generate%20ssh%20key%20.png) In the image, there's a split screen. The right part of the screen shows the slave node. In the slave node, you input the generated ssh keys from the  master node into the authorized_keys file in the ".ssh" directory. Then, you can now login to the slave node from the master node with command "ssh vagrant@ip address of the slavenode"; as seen on the left side of the split screen.

6. `Create inventory and playbook file` : Still on the masternode, I created and ansible directory (mkdir ansible) and created both the inventory file and playbook file in the ansible directory.![](./Create%20playbook%20and%20yaml%20files.png) In the above image, the playbook.yml file was later changed to a lamp.yml file for specification reasons based on the task given.

7. `Edit inventory file` : fill in the inventory file with the hosts(master and slave nodes) and it's ip address![](./Inventory%20file%20setup.png) I edited the file with command (vi inventory) but in the image i only viewed the details of the file with command (cat inventory).

Using the vim editor, you save and exit by pressing the escape bottun on your keypad, then press the colon button then type in 'wq' and the enter button.

8. `Ping inventory file`: I pinged the inventory file with command (ansible all -m ping -i inventory). ![](./Ping%20inventory%20file.png)

9. `Playbook`: the playbook file, which is the lamp.yml is a yaml file for automation. You edit the lamp.yml file using command (vi lamp.sh) or  (nano lamp.sh) depending on your preferred editor.![](./lamp.yml)

10. `lamp.yaml`: ![](./lamp.yml%20file%20execution%20success.png) The above image shows the execution of the lamp.yml file execution success after editing the .yml playbook file and executing it to ensure that your ansible playbook is valid.

11.`Access the laravel app with VMs ip address`: After all editing. It is expected as specified in the given task to execute the playbook file while on the masternode to run and execute the bashscript i.e the (lamp.sh) on the slave node. thus, ensuring that the laravel application is accessible through the Slavnode's Ip address(192.168.33.25).![](./Ip%20address%20evidence.png)


ERRORS ENCOUNTERED IN THE WORK PROCESS:
It is normal to arrive at errors while learning, but these errors kept me going to keep finding solutions to the ongoing work so I could arrive at the destination of the given task.                  


`Error 1`: I initially ran the script with the basic knowledge I had and arrived at an 'almost destination', then I went back to work on my script to reach the final destination.![](./Screenshot%20of%20accessing%20the%20app%20through%20the%20VMs%20ip%20address.png)

`Error 2`:Faced some issues in my bash script that kept me away from reaching the final destination of the laravel application.
![](./some%20errors%20faced%20in%20process.PNG)

The above image shows a different ip address from the actual ip address I used to run both master and slave nodes. This is because after facing several errors, I used the machines in the above image to test run my task before perfecting the given task on the actual Virtuam Machines I created for the assisgnment as seen below. More so, even in the image below with the valid ip address used to host the laravel application, I still faced some errors as seen in the image below.
![](./Errors%20encountered.png).

`Lesson`: Mistakes do happen, it's part of the whole process to be a world class engineer. 
