# Your CRL Machine

## CentOS 

Practically all CRL machines come with Linux CentOS 7 preinstalled (which is a distribution fork from RHEL/RedHat), which is more stable than Ubuntu (Debian). 

Furthermore, the hospital has a policy on operating systems and right now CentOS is allowed, and Ubuntu is not officially allowed.  It requires an exception from the ISD security team to run ubuntu.(This is in part historical.  e.g. many years ago, Dell would sell a computer with RHEL but not with Ubuntu.)

In case you want to setup our own Ubuntu, you could try to setup dual boot (Davood, a member of CRL works like this). If you want to run Ubuntu, Simon could help you (he configured Ubuntu for CRL website). I personally have not done this to save time. Instead - I improved my workflow by getting `sudo` access to my own machine and using `conda` where possible. 



## Configuring Your Bash Profile 

You will need to configure your bash profile for quick access to CRL shared software tools - e.g. matlab, itksnap, misterI, crkit, etc. 

If you install any new software, you should link to it via $PATH or aliases. 

In general, learning to configure your bash profile well would greatly simplify the day to day struggles. 

Our best bash experts are of course Sean, Clemente, Simon. You can ask them for a copy of their bash to start with. Best thing to start with is to copy the bash profile of someone who is a power user with their permission. 

Serge's bash (all messy) is [here](https://drive.google.com/file/d/1jtAbLmEDQQYUKd_AXxLMZX4Ewh0bCiIQ/view?usp=sharing).

## Shell scripting 

Learning how to get around in Linux would help you greatly on the day to day tasks in your Linux OS. One of the skills is learning how to write simple bash shell commands, and chain them together. 

[This FSL tutorial](http://fsl.fmrib.ox.ac.uk/fslcourse/lectures/scripting/all.htm) on shell scripting is a must for all that use Linux. 


## Image Viewing Tools




## Installing New Software

### With sudo 
Root access (sudo access) will help you to manage many future installations on my own machine. Ask Sean Clancy for help with giving you root permissions to your own CRL machine. 

Subsequently, you could install new software via `sudo yum install`. Typically a search for `yum install <tool_you_need>` should yield results for common libraries. 

Alternatively, you can try `sudo snap install`. You will need to install snap first before using it. [Click here](https://snapcraft.io/install/snapd/centos) for more info. 

For the brave ones - you can of course compile from source. Hat off to you, sir/ma'am, for your courage. 

### Without sudo 

If you are a developer, you will benefit greatly from using a package manager such as `conda` (miniconda or anaconda). In most cases, you can avoid using `yum` by using conda commands. Conda downloads precompiled binary executables direct to your environment. What's more important, conda is a package manager that checks for dependency conflicts with all your other conda uploaded software for a given environment. This means that if you are building in python (and beyond!), your libraries will not break from dependency conflicts. Learn more about conda in [softwarebestpractices](softwarebestpractices) section. 

## Remote Work


### VNCserver 

Most CRL members use this tool to login to their BCH machine remotely with  a graphical interface. 

Instructions on installing VNCserver are given [here](). 


### Nomachine.com 

This is another tool suggested by Simon. [https://www.nomachine.com/](https://www.nomachine.com/)


## CentOS 
Most CRL machines run centOS 7 Linux. If you want to add dual-boot to all for another operating system on your machine, e.g. to configure an Ubuntu Linux, you can ask Simon for help. E.g. Davood runs Ubuntu for day-to-day research purposes. 






### System Management 

[the following is a note from Simon after he had read this guide] 

_- system management is largely done by ansible.  As much as possible each user workstation should be configured in the same way. This is done by running ansible scripts that make each workstation have the same environment._

_- yum and its replacement dnf (and future replacements like flatpak) manage packages via repositories. today our workstations are configured via  a script that downloads and installs all of the components needed to have the workstation on the hospital network, to provide compilers etc. it would only be if you inherited a mismanaged workstation that that would not be in place already , or if you bought a new workstation._