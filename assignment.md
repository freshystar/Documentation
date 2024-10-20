# Running Docker using a Virtual Machine tool (Multipass)
 
 Docker is a software plateform that allows you to build, test and deploy applications quickly. It can also be considered as a tool used to create and manage containers. Installling docker on our host machine is good but not safe as some malicious hackers could use these containers as a means to access our machine. Furthermore, the program isolation containers offer is not that optimal thus putting our machine to a potential risk.

 ## Removing Docker from Host Machine

If you've docker installed on your host machine, you'll have to uninstall it in order to avoid any unpleasant situation. Docker desktop creates symlinks for the binaries in `/usr/local/bin`, which means they're automatically included in PATH on most systems. 

```bash
$ /usr/local/bin
$ sudo rm -rf docker*
```
 
 ## Installing multipass on Linux OS(Ubuntu)
  
  Multipass is a tool to generate cloud-style Ubuntu VMs. One shouldn't talk of multipass as a Virtual Machiine but as a tool used to generate VMs. Multipass is available as a `snap` package on Linux. The `snap daemon` is pre-installed in `Ubuntu 18.04 and above`. Once you've `snapd` available on your system, you can install multipass by running the following command:

  ```bash
  $ sudo snap install  multipass
  ```

  ## Creating a docker instance on multipass

  To create an instance, just run:
  ```bash
  $ multipass launch docker --name docker-vm
  ```
  
  The above command will create a docker image `docker-vm` from the docker instance using an image of the latest LTS version of Ubuntu(22.04.5). Multipass will assign a default configuration to your image created.

  You can check the details of your instance with the following command:
  ```bash
  $ multipass info docker-vm
  ```
   
   ## Opening a shell prompt in docker-vm

   To open a shell prompt in docker-vm, execute the following command:
   ```bash
   $ multipass shell docker-vm
   ```
    
  You can run commands as you would do on any Ubuntu Installation.

  ## Executing a command in  docker-vm

  To ease our work, we can configure our shell script with an `alias` commmand in order to run commands directly on the command line. To do that, we will first have to edit our shell's file.
  ```bash
  $ nano .<shell name>rc
  ```
Once in the shell's file, you can add this at the end of the file's content:
```bash
alias docker="multipass exec docker-vm -- docker"
```
Then you can save and exit the file.
source the file in order to execute the lines of the code in the file as if they were printed at the command line directly.
```bash
$ source .<shell name>rc
```
 After sourcing, you can simply tap:
 ```bash
 $ dosker ps
 ```
 This is just an example of a command you can execute in your docker-vm. This command will show you all the remote running containers on your machine.

 Congratulations!!!, you are just from creating an instance`docker-vm` from a VM tool`multipass`. You're ready to go. 

