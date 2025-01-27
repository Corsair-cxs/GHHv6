# Gray Hat Hacking v6 Chapter 17
This directory contains all the components necessary for Chapter 17.

## Lab Information  
The following VMs will be setup for this lab:
- Domain Controller
  - IP: 10.0.0.10   
  - Domain Admin: ghhadmin
  - DA Password: GrayHat6!
- Target Computer
  - IP: 10.0.0.20
  - Target User: target
  - Target Password: Winter2021!
- Util Computer
  - IP: 10.0.0.30
  - User: Administrator
  - Password: GrayHathack1ing!
- Kali Computer
  - IP: 10.0.0.40
  - User: kali
  - Pass: SSH key setup with the lab

## Setting up the Lab    
1. Make sure you have completed all the steps at (https://github.com/GrayHatHacking/GHHv6/tree/main/CloudSetup).
1. Go into the Lab/terraform directory and copy the `terraform.tfvars-orig` to `terraform.tfvars`. Edit the file with your
   favorite editor and then replace the contents of the key_path variable with the path to your SSH key. An example
   might look like:   
   `key_path="/home/kali/.ssh/id_rsa`
1. Go into the Lab subdirectory and run `build.sh` to start the environment build. It will ask you are sure you want to create resources.
when it does, type in `yes`.
1. This will create resources that may cost you money. If you want to destroy the lab between uses, 
run `destroy.sh`. Answer `yes` when it asks if you are sure, and the resources will be deleted.
   
## Retrieving the IP addresses of the machines
Once the build.sh script is completed, it should print the IP addresses of the hosts
out to the screen. If you forget these IP addresses, you can go into the terraform directory
in the lab and type in "terraform show" and it will show you the status of your
lab as well as show you the IP addresses of the relevant boxes

## What does each machine do?

### Domain Controller
This system is the domain controller for our lab. The target VM is a member of 
a domain in order to make the scenario more realistic.  This system is critical so it
should not be shut down

### Target system
This is the system you will be attacking during the lab. It should be the only system besides
the Kali box that you would need to interact with in the lab environment unless you
do additional work on your own.

### Util box
This box builds a number of tools that we will build in the lab so you can have
experience with the latest versions of the tools.  If you do not want to use this box
for experimentation, building tools, or other tasks it can be destroyed after
the lab is provisioned. There is a terminate-util.sh script for this task.

### Kali box
This is the Kali attack system that will be used in the lab. 
   
## Notes
By default this lab allows ANYONE who knows the credentials to connect to it. For new users
it may be confusing to figure out where they are connecting from. If you would like to make this more
secure, you can limit the lab to your IP only by adding a line into the `terraform.tfvars` file that contains 
allow list information like this:   
`ip_allowlist = ["1.2.3.4/32","4.5.6.7/24"]`
