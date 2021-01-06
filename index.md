## CRL Guide 

This is a very early draft of the CRL guide. It was originally written as an informal email for new CRL members - Aziz and Cemre. Over time this guide will be expanded to include detailed information on most **_used_** and most **_useful_** tools for CRL members, and <span style="text-decoration:underline;">not only</span> for new starters.   

We would like you to help us to contribute to this guide as much as possible. We want this guide to be useful for _your_ daily work as well as for others. 

Currently, this guide covers a range of different topics such as: 



*   how to setup your VNC Viewer for remote work
*   how to manage data and document storage on your CRL machine 
*   how to quickly access your pay / insurance / zoom profile on the BCH intranet
*   how to register for BCH Google Drive 
*   (early draft of) links to basic educational topics on linux, MR physics, neuroanatomy, github, etc 

Over time, new sections will be added such as: 



*   how to create basic splash webpage for your new paper 
*   how to publish on arxiv 
*   how to send jobs to Research Computing CPU / GPU cluster
*   how to create a Jupyter Lab environment for remote work
*   where to learn about Docker containers 

**About this early draft:**

Currently, this guide is available in two formats - as a webpage (which is easily editable with _your _github profile) and as a Google Doc. In the coming weeks the single format of the webpage will be split into several subpages that are much easier to navigate.

**To contribute / edit this guide:**

If you want to contribute to this guide - you can edit it on Github or via Google Docs. 

The github version is published here - [https://github.com/sergeicu/crl-guide/edit/main/README.md](https://github.com/sergeicu/crl-guide/edit/main/README.md). To edit it - please email serge with your github username and he will add you to the repository so you can make changes. Over time - this github repository will be migrated to an appropriate CRL organization account. 

If you are editing the Google Doc - please edit the Google Doc in 'suggesting mode'. To do this - click 'editing' in the top right corner of the google doc, and change 'editing' to 'suggesting' mode. 


## <span style="text-decoration:underline;">Table of Contents</span>


[TOC]



## <span style="text-decoration:underline;">Your CRL machine </span>


### CENTOS

Practically all CRL machines come with Linux CentOS 7 preinstalled (which is a distribution fork from RHEL/RedHat), which is more stable than Ubuntu (Debian). 

Furthermore, the hospital has a policy on operating systems and right now CentOS is allowed, and Ubuntu is not officially allowed.  It requires an exception from the ISD security team to run ubuntu.(This is in part historical.  e.g. many years ago, Dell would sell a computer with RHEL but not with Ubuntu.)

In case you want to setup our own Ubuntu, you could try to setup dual boot (Davood, a member of CRL works like this). If you want to run Ubuntu, Simon could help you (he configured Ubuntu for CRL website). I personally have not done this to save time. Instead - I improved my workflow by getting `sudo` access to my own machine and using `conda` where possible. 

 


### SUDO

Having sudo access had helped massively to manage certain required installations on my own machine. 

You can request sudo access for your machine from Sean. 

e.g. I use `sudo yum install` to install packages / software (a.k.a. like apt-get on ubuntu ) 

I also use `snap` wherever possible instead of `yum` to avoid conflicts (which do arise when you use `yum`). 

[https://snapcraft.io/docs/installing-snap-on-centos](https://snapcraft.io/docs/installing-snap-on-centos)

However, in general, I do not use `yum` or `snap` very often at all. I've only used in rare cases where I really need very low level dependency installations. Instead - I mostly use `conda`. 


### System Management 

[the following is a note from Simon after he had read this guide] 

_- system management is largely done by ansible.  As much as possible each user workstation should be configured in the same way. This is done by running ansible scripts that make each workstation have the same environment._

_- yum and its replacement dnf (and future replacements like flatpak) manage packages via repositories. today our workstations are configured via  a script that downloads and installs all of the components needed to have the workstation on the hospital network, to provide compilers etc. it would only be if you inherited a mismanaged workstation that that would not be in place already , or if you bought a new workstation._


### CONDA

The most useful tool of all for me had been `conda/anaconda`. 

In most cases I was able to virtualize everything via conda, without having to run `yum` or `snap`. 

As you probably know, conda can be used to manage dependencies between packages that are <span style="text-decoration:underline;">not </span>only python. 

Typically, if I want to install any new software, I always google search first for `&lt;library_name> conda`. 


### NVIDIA 

Each GPU enabled machine would have its own NVIDIA drivers. 

As always, you will need to match your CUDA toolkit to the driver.

For your own machine - it would not be so difficult. 

 

The problem may start to arise if you want to `ssh` into another machine to use its GPU - as you will need to match to its driver and your CUDA toolkit also.This is where things may start breaking down. That's where conda may come handy. Or a smart '.bashrc' script. 

I guess you won't be needing help on this first, but if you have some problems later - let me know i may be able to help. 


### BASHRC

I attach here a copy of my .bash profile 

[https://drive.google.com/file/d/1jtAbLmEDQQYUKd_AXxLMZX4Ewh0bCiIQ/view?usp=sharing](https://drive.google.com/file/d/1jtAbLmEDQQYUKd_AXxLMZX4Ewh0bCiIQ/view?usp=sharing)

What do I need to add to my .bashrc or .bash_profile file located in your home directory (/home/chxxxxxx):



1. Visualization: itksnap, misterI, crlviz (it is the crkit, i.e. the crl c++ written itk code binaries that is described elsewhere)
2. Path to binaries such as dicom toolkit (dcmtk), optimization (using BOBQA) for matlab

I had cleaned it to make it as easily understandable for you both. 

You will specifically want to add the following sections from my bash: 

- CRKIT 

- clemente's bash 

- non conda installed software - servers 


### New Lab Members 

_[the following was suggested by Simon after he had read this guide]_

- new lab members should write a brief bio about themselves and send me the bio and a picture/headshot to put on the web site.

- each time someone has a paper accepted, they should write a brief blurb about it and provide the manuscript to be added to the web site.


## <span style="text-decoration:underline;">CRL tools</span> 


### Image processing tools - CRKIT 

This is a collection of tools developed internally at CRL for all sorts of imaging tasks. 

Most of these are C++ binaries. 

Many of these are already incorporated into CRL libraries, e.g. in DCE reconstruction. 

There are also many other useful commands like: 

- crlConvertBetweenFileFormats

- crlDcmConvert

- dcmdump 

etc 

There are more than 300 different functions here. 

One big problem is that there isn't really any easy documentation or tutorial to follow (that I know of!) 

I will ask someone at CRL later to give us all a tutorial on this via Zoom. 

I myself wanted to learn about it for a long time. 


### Image processing tools - FSL and ITK 


#### Inside terminal 

I found FSL library to be extremely useful when working with nifti images for various kinds of image processing operations. 

All commands are invoked inside the linux terminal. 

Especially useful is the `fslmaths` function. 

You can find path to it in my bashrc. 

I assume that CRKIT also has similar functions (but someone has to guide us on these in a tutorial). 


#### In your code 

Alternatively, if you want to have more control <span style="text-decoration:underline;">and  </span>you need to perform MRI image operations INSIDE your C++/Python code - use `​ITK`. 

ITK has many tools for working with nifti related files - including managment of header related items - such as orientation, affine matrices, etc. 

This is also in my bash. 

Or, you can also use `pynnrd` or `nibabel` libraries for working with .nrrd and .nii.gz files respectively. 

You can install these via `conda`. I prefer this over ITK. 


### Matlab - raw data 

To read raw data matlab I use a library called VBVD 

[https://github.com/CIC-methods/FID-A/tree/master/inputOutput/mapVBVD](https://github.com/CIC-methods/FID-A/tree/master/inputOutput/mapVBVD)

There is an updated version of VBVD (VBVD2) written by Onur. Ask him for path.   


### Matlab - general 

Another member of our lab, Tess Wallace, is currently on maternity leave.

She has developed a huge number of very useful tools for working with MRI images in matlab. 

You can add her matlab code to your path here - it is pretty well documented - 

/fileserver/motion/tess/Code/​


### Image viewers- ITKsnap and misterI 

These are two different software tools for viewing files. 

I do not use misterI very much but it is very useful for DCE stuff. 

This tool was developed by Benoit in our lab. 

It is heavily used by Jaume, Clemente. 

The path to misterI is in my bash. 

I prefer to use ITKsnap myself. This is a public tool that you can download online. 

It loads .nii.gz, .nrrd, .vtk images. 

You can also view 4D files in it. 

I can show you tips and tricks how this works. 

I think Sila uses this also heavily, like myself. 

Finally, there is also a tool called crlViz. I haven't used it much. 

Ask Onur for more info on this. 


### Remote work - VNCserver, Jupyterlab, VScode 


#### A note on secure work 

Once you are logged into BCH VPN with your PulseSecure app on your laptop, your ipaddress is technically that of BCH. 

BCH recommends to be connected onPulseSecure <span style="text-decoration:underline;">only </span>when you really need to access BCH resources. So don't forget to disconnect PulseSecure after you finished for the day, or if you do not need to use servers/data from BCH (e.g. when reading papers etc). 


#### VNCserver 

Most people at CRL prefer to use this tool to login to their BCH machine directly via a graphical interface. 

Then you can start Terminal, Matlab, etc as if you are in the office. 

I include instructions on how to install VNCserver at the bottom of this email. 


#### Nomachine.com 

This is another tool suggested by Simon. I haven’t used it personally but Simon prefers it. [https://www.nomachine.com/](https://www.nomachine.com/)

“This remote access works with Windows , Mac OS and linux, and between all 3 OS in the same way. It is what I use.” [Simon]


#### JupyterLab 

I personally use jupyter lab for prototyping in python and bash scripting. 

If you are planning to work with python - I can give you a tutorial on how to setup jupyter lab for remote work.

It is extremely convenient tool because you do NOT need VNCserver in this case. 

Simply you can access your BCH computer via Jupyter Lab (in Chrome browser). 


#### VScode 

I use VScode as my preferred IDE for more complex development. It has a lot of nice debugging tools, similar to PyCharm or Eclipse. 

However, it has amazing features for remote work. For example I do not need to use VNCserver. I can start VScode on my laptop and work with my code and data directly as if I was at the office. 


## <span style="text-decoration:underline;">CRL CPUs</span>

Aside from your own CRL machine, we have a large number of machines in the lab. 

These are either smaller machines or large servers. 

Smaller machines are typically assigned to lab members as personal workstations. 

Some smaller machines are unallocated and can be used to run batch jobs. 

Larger servers are much bigger and faster - you can schedule computationally heavy jobs on these. 

E.g. DCE GRASP reconstruction code will only run on machines that have at least 100Gb+ of RAM free. 

You can find the list of CRL lab machines here  - 

 

[you need to be inside VPN ] - [http://leko.tch.harvard.edu/](http://leko.tch.harvard.edu/) > click `confluence` > login with your CRL confluence username and password (you must ask Sean to give you access - this is NOT the same as your BCH account) 

SERVERS: 

[http://leko.tch.harvard.edu:8090/display/SYSADMIN/Server+Listings](http://leko.tch.harvard.edu:8090/display/SYSADMIN/Server+Listings)

PERSONAL WORKSTATIONS: 

[http://leko.tch.harvard.edu:8090/display/SYSADMIN/Personal+Workstation+Listing](http://leko.tch.harvard.edu:8090/display/SYSADMIN/Personal+Workstation+Listing)

Here is my personal list of CRL servers that are good to use for compute: 

[https://docs.google.com/spreadsheets/d/1JiM8Ef2Qg0oSVbDzldjbk7uTFKU0MNKOzaZck_QgzAY/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1JiM8Ef2Qg0oSVbDzldjbk7uTFKU0MNKOzaZck_QgzAY/edit?usp=sharing)

to access each machine use ssh from the terminal of your CRL machine. 

e.g. `ssh ankara` 

or 

`ssh -X ganymede` (if you want to start a graphical user interface (GUI), like Matlab, or if you are working inside VNCserver) 


## <span style="text-decoration:underline;">CRL INTERNAL storage</span>

Many of the CRL machines that were described in the section above are used as mount points for CRL storage devices. 

Most of these have many terrabytes of space. 

When you open the Terminal on your BCH machine, your default working directory is `/home/&lt;your_username>`

However, this directory is NOT hosted on your BCH machine. 

In fact, it mounted on a server that sits outside of Boston somewhere. 

Fullpath to `/home` mount is`crlfs8.tch.harvard.edu:/mnt/mpathg/home`

`/home/` and many other storage locations that would be available to you are BACKED UP. Which means that if these servers go down, we could largely restore your data. The backup is typically done either daily or weekly, depending on the storage device. 


### Storage devices mounted on your machine 

To view the full list of storage devices that are mounted (aka visible) on your BCH machine run `df -h` inside the terminal. 

The output of `df -h` will have many lines, which would include the following (this is part of my list for example): 

crlfs8.tch.harvard.edu:/mnt/mpathg/home                16T  7.4T  8.7T  46% /home

crlfs8.tch.harvard.edu:/mnt/mpathf/motion              16T   16T  223G  99% /fileserver/motion

crlfs9.tch.harvard.edu:/mnt/mpathf/abd                 16T   16T  298G  99% /fileserver/abd

crl-rdynaspro4:/c/export                              9.1T  6.3T  2.8T  70% /fileserver/external/rdynaspro4

crlpurestorage1.tch.harvard.edu:/fastscratch           60T  7.5T   53T  13% /fileserver/fastscratch

crlfs7.tch.harvard.edu:/mnt/vd-1/optwork/matlab        15T   12T  2.4T  83% /opt/matlab

Quick intro:

- crlfs8 - is the filesystem 

- /fileserver/motion - is the location that you can access inside your terminal to see files stored on this filesystem 

- 16T - is the total space on the filesystem 

- 223G - is the remaining free space 


### Important locations: 

/home

is where everybody's home directory is stored. It has 12Gb file limit. After you surpass that limit, you won't be able to create new files. It is recommended that you use this space to store your code, bash scripts, presentations, etc. Not image data or experiment data. /home is backed up, so if it goes down we can recover it. 

/fileserver/motion

used for Onur's and Tess' projects. You can important image and experiment data here.  

/fileserver/abd

used for Sila's projects, including DCE. You can store important image and experiment data here. 

/fileserver/external/rdynaspro4

this is where all DCE reconstructions and code are. We use this to store DCE code as well as reconstructed clinical DCE data. 

​

/fileserver/fastscratch 

use this location to store any data that does not need backup and can be reproducible. e.g. training weights of networks. Easily reproducible experiments,etc 

/fileserver/scratch 

same as above 

/opt/matlab

e.g. this is where the common matlab install is mounted. You can point your bash profile to this location for matlab. e.g. see my bash profile 


### To add a mount locations: 

If you know how to mount devices, you can add extra devices by editing your /etc/fstab file. 


### Your own machine

Your own BCH machine also has storage. You can of course store data here. However it is not backed up. 

e.g. /local 


### New storage devices 


#### Simon and Research Computing

In addition to the above locations, Simon has recently acquired another filesystem. 

It is given to him by Research Computing and has ~400T of space, of which 200Tb are free, I believe. 

This file system would NOT be mounted on your BCH machine automatically by default. 

IF you want to access this filesystem, you need to ssh into either `auster`, `eurus`, `zephyr`, `boreas` machines. 

i.e. `ssh boreas` 

Then, you will see it within `df -h` output. 

The file location is called: 

/fileserver/Rad-Warfield-e2

It is important to note that this is a mount that uses BCH GOOGLE Drive - and therefore you CANNOT store PHI (identifiable) data on it . 

If you want Simon to mount this location on your machine - you need to ask him about it - however you need to be listed on relevant IRBs to be able to use it (I believe). 


#### Sila's new storage device 

As Sila mentioned earlier, she had recently purchased a new storage device and it would be made available. 

We will need to ask Sean to help us mount it on our BCH machines after this. 


## <span style="text-decoration:underline;">CRL GPUs </span>

_[This section of the starter pack is being actively edited - content may change heavily]_

There are only a handful of machines at CRL. 

My machine - rayan - has 12Gb GPU 

Sila's machine - ankara - has 8Gb and 24 Gb GPUs 

Cemre’s machine - gamakichi - needs new driver. 

Simon’s machine - kajrakin - has 24Gb GPU 



machine - carlsen - has 4Gb GPU 


<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: Definition term(s) &uarr;&uarr; missing definition? </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>






Finally, Ali and Davood have their own cluster of 4x Titan XP GPUs (12Gb each), which they use heavily.  

Research Computing has 5 more GPUs: 

Tesla K80,

Tesla T4,

Titan RTX,

Quadro RTX

[http://websvc4.tch.harvard.edu:8090/display/RCK/Computing+Resources](http://websvc4.tch.harvard.edu:8090/display/RCK/Computing+Resources)

(need VPN to view the page) 


### Simon’s notes on Research Computing access (CPU and GPU) 

(copied from SImon’s email) 

Three things to know :

1.

We have 400,000 GB of disk space accessible on e2.

The directory /fileserver/Rad-Warfield-e2 is accessible on boreas,auster,zephyr,eurus

and on e2 as  : /lab-share/Rad-Warfield-e2

Due to BCH policies about separation of PHI and non-PHI data, the first place to look to store your non-PHI data is

/lab-share/Rad-Warfield-e2/Public

2.

If there was a need to efficiently transfer data between any of the CRL file servers and e2 , it can be done using rsync e.g.

rsync -e ssh -auz /my/local/storage .

3.

log in to e2 is via ssh authenticated by public key encryption without the need for any password.

If there are any difficulties, please ask me.

--- 

Two important factors are the treatment of PHI, and the UNIX approach with group permissions that Research Computing uses.

The key to understand is that the group id, and user id, is issued by research computing, and is based on the IRB protocol covering the research, and is not issued by the CRL.

Once such id numbers have been issued, they can be promulgated through the CRL, so that there is no mismatch when viewing the information from different computers.


### Yao’s notes on Research Computing E2 cluster usage 

[contact Yao for more information]

I use the GPUs on E2 to train my very deep neural networks, eg, with over 2M parameters. We are limited to have 50GB drive space only on E2, so I wrote  a python script to periodically transfer the data and results in piece to and from my workstation via SFTP service.


## <span style="text-decoration:underline;">GETTING STARTED</span>


## <span style="text-decoration:underline;">BCH IT account</span>

With the BCH IT account you can 

1. access BCH email

2. login to your BCH CRL machine 

3. access CRL storage devices and machines

4. access relevant BCH services like insurance, pay, zoom, research computing, etc 

In the above section I already told you about 3. 

Next I will tell you about 4. 


## <span style="text-decoration:underline;">BCH IT onboarding </span>

(for Aziz only)

Aziz - to get the account you will receive instructions from BCH IT. 

Just a note - BCH has recently heavily upgraded security for remote work. 

So you will need to complete a seemingly infinite list of admin tasks.

e.g.  

- provide BCH IT people with your personal phone number

- hold a special call with them verify your identity

- download Duo Mobile app on your phone

- download Pulse Secure app on your laptop

- encrypt your own laptop and phone. 

Once again - don't worry about these - you will get instructions how to do it. If any questions - ask us. 


## <span style="text-decoration:underline;">BCH research safety and security </span>

You will be required to pass various research safety and security related courses via a system called NetLearning. 

This would take at least some hours also, so plan ahead. 

There may be additional administrative to do in regards to Sila/Onurs IRBs, which are project dependent. They will tell you more about it. 


## <span style="text-decoration:underline;">CITI TRAINING</span>

In addition to NetLearning, you will also need to pass CITI courses. 

The link to the internal CITI instructions is here: [http://web2.tch.harvard.edu/biobank/mainpageS3005P46.html.](http://web2.tch.harvard.edu/biobank/mainpageS3005P46.html)

You will need to create a CITI account and list Boston Children's Hospital as your institution, and then complete the appropriate training/s. In your case, I recommend completing the CITI Biomedical course and the Conflict of Interest Training. 

Once you've completed your courses, send your CITI transcript to Sean, and he will arrange to have you added to CHERP and the appropriate IRB/s. 


## <span style="text-decoration:underline;">Web2 intranet</span>

There is a large amount of admin related things that you can do here - 

[http://web2.tch.harvard.edu/index.html](http://web2.tch.harvard.edu/index.html) [web2]

in order to access this intranet site you need to be logged in to BCH VPN. 

Most useful things are: 

1. elect your benefits (like health insurance stuff)

2. manage your pay 

3. pass NetLearning courses

4. change your BCH password remotely 

5. find tools to encrypt your phone and laptop 

7. schedule your own Zoom invites (with no time limit)

How to get to these things: 

for 1 or 2. - [web2] (see link above) > Human Resources (top tab) > People Soft (side tab)

for 3. - [web2] (see link above) > Human Resources (top tab) > Net Learning (side tab)

for 4. - [web2] > eHelp (side tab) > accounts and password (side tab) 

for 5. - [web2] > eHelp (side tab) > BYOD (side tab) 

for 6. - [web2] > Zoom (side tab) 


## <span style="text-decoration:underline;">Getting help </span>

First port of admin related or technical related help is Sean :) 

If you have general technical IT issues - email <span style="text-decoration:underline;">IThelpdesk@childrens.harvard.edu</span>

If you have general non IT issues - email <span style="text-decoration:underline;">help.desk@childrens.harvard.edu</span>

However, help desk is rather slow. Sometimes it takes days to get a response. If you need help right away it is best to just call them. 

Go to [web2] > eHelp to find phone contact details for IT or HR services. 


## <span style="text-decoration:underline;">Research Computing </span>

[we will do a general CRL introduction to these over the coming weeks because I am myself very new to this and want to learn]

Research Computing has 

A. cluster of compute machines that can be accessed remotely 

B. extra storage space, including unlimited Google Drive Storage. 


### For A - Compute Cluster  

All info is here -

[https://www.researchcomputing.org/computing-and-hosting-solutions](https://www.researchcomputing.org/computing-and-hosting-solutions)

 

[http://websvc4.tch.harvard.edu:8090/display/RCK/Servers%2C+Cloud%2C+and+HPC](http://websvc4.tch.harvard.edu:8090/display/RCK/Servers%2C+Cloud%2C+and+HPC) 

(to access the 2nd link you need to have VPN access) 

I haven't done much on this end yet, but I hope to investigate this together with you later. 


### For B - BCH Drive

As I already said, our own lab has lots of internal storage devices and typically we use this for work. 

However, recently we also started using Research Computing Google Drive, which has "unlimited" space. 

However there are some current limitations - for example you cannot store PHI (patient identifiable) data on it <span style="text-decoration:underline;">yet</span>. 

To register BCH Google Drive - 

[http://websvc4:8090/display/RCK/GSuite](http://websvc4:8090/display/RCK/GSuite)

(you need to be connected to VPN to access this site) 

Once BCH IT people grant you access to the Google Drive - you can literally use it as normal Google Drive via web browser. 

As I understand, you can also mount the Google Drive to your office machine (and your encrypted work laptop). However I have not found out yet how to do this properly. 


### Notes from Simon on BCH Google Drive 

Google drive is very nice. The hospital policies are here:

http://websvc4.tch.harvard.edu:8090/display/RCK/Google+Shared+Drive+Management

On mac and windows it can be mounted similar to a network drive.

On linux, Rclone can be used to transfer large amounts of data to and from google drive.

Via the hospital, we have access to unlimited amounts of google drive storage rate limited at 100GB/day for non-PHI data.

For PHI data, a policy has been established:

http://websvc4.tch.harvard.edu:8090/display/RCK/BCH+Google+Drive+for+PHI

We have shared google drives for data from SAIL including MRI, Ultrasound and PET/CT.


## <span style="text-decoration:underline;">Learning </span>


### Suggestions from Simon on linux crash course: 

You might find some resources to teach the truly new e.g.

[https://www.vikingcodeschool.com/web-development-basics/a-command-line-crash-course](https://urldefense.proofpoint.com/v2/url?u=https-3A__www.vikingcodeschool.com_web-2Ddevelopment-2Dbasics_a-2Dcommand-2Dline-2Dcrash-2Dcourse&d=DwMDaQ&c=qS4goWBT7poplM69zy_3xhKwEW14JZMSdioCoppxeFU&r=b4Nb-lF5XBCiHWj64StekdJQgylGzYqrVQ9qwCO9n5Om_qHh04diXz6BW5PQjq3i&m=NGbZh8kPEQ97Y4he2ABoq02lgiLg4k5TLVs6hLN-vMQ&s=GfDU9g1nn8qxry77FZWcHnHdTMEOVshZvlx36xfAn4c&e=)

[https://www.edx.org/course/introduction-to-linux](https://urldefense.proofpoint.com/v2/url?u=https-3A__www.edx.org_course_introduction-2Dto-2Dlinux&d=DwMDaQ&c=qS4goWBT7poplM69zy_3xhKwEW14JZMSdioCoppxeFU&r=b4Nb-lF5XBCiHWj64StekdJQgylGzYqrVQ9qwCO9n5Om_qHh04diXz6BW5PQjq3i&m=NGbZh8kPEQ97Y4he2ABoq02lgiLg4k5TLVs6hLN-vMQ&s=2gHv_Z0KTDDsaaldTrgM9CZI8CUvzYEh8DkrPA4pF2Y&e=)


### Suggestions from Serge on unix shell scripting crash course 

I absolutely love this guide 

[http://fsl.fmrib.ox.ac.uk/fslcourse/lectures/scripting/all.htm](http://fsl.fmrib.ox.ac.uk/fslcourse/lectures/scripting/all.htm)


### Crash course on MR physics, Neuroanatomy, MRI Artifacts, Git, Grant Writing, Python, Diffusion MRI

I found these guide from Martinos to be invaluable and very relevant - 

[https://gate.nmr.mgh.harvard.edu/wiki/whynhow/index.php/Main_Page](https://gate.nmr.mgh.harvard.edu/wiki/whynhow/index.php/Main_Page)

I will add more links over time (IF YOU HAVE ANY NICE LINKS FOR ANY TOPICS THAT MAY BE USEFUL TO OTHERS AT CRL  - please add them here with your name!)  


## <span style="text-decoration:underline;">Appendix </span>


### Installing and running VNCserver 

To setup VNCserver you need to 

A. install VNC Viewer on your laptop. 

B. install VNCserver on your BCH machine  

C. Start vncserver 

For A - download the binary from public website - search for `realvnc` or `tigervnc` on google. 

For B - you can try to install vncserver yourself via `yum` or `snap` on your BCH machine. 

e.g. `sudo yum install tigervnc-server​` 

I personally had some trouble here and had to ask Sean for help because my machine had some miscalibrations of GPL libraries. 

For C - as long your BCH machine has not been restarted - you will need to run `vncserver` _only once_ in the terminal of your BCH machine

On your BCH machine terminal: 

$ vncserver >> to initialize vncserver after restart or to start it for the first time 

$ vncserver -list >> to view list of currently running sessions  

$ vncserver -kill &lt;sessionID> >> to kill any running session 

How to setup VNCviewer on your laptop: 

1. Start VNCviewer on your laptop, click New Connection

2. ssh into your BCH machine via terminal and get the exposed DNS server address like this - 

$ nslookup &lt;youBCHmachinename> 

>> for me this command yields: 

 >> Non-authoritative answer: 

 >> Name: rayan.tch.harvard.edu 

 >> Address: _10.16.6.179  _

3. Add VNCserver like this ->  `&lt;DNS_ip_address>:**590**&lt;sessionID>` 

e.g. 10.16.6.179:5901

Note that the green section would be different for your own machine. 590 is the standard port. &lt;sessionID> will be different for you (you can get it from `vncserver -list` command)

4. Add name for your connection. Click ok. 

5. You can repeat this process again for other machines if necessary. e.g. if you SSH into other machines at CRL you can run vnc there also (as long as it is installed) 


### [info] Suggestions for improvements to CRL guide 


##### Suggestions from Simon 

I would put these in the categories of:

1. UNIX

2. programming

3. anatomy

4. imaging

I have saved this lab template as a good starting point:

[https://osf.io/4vfg7/](https://urldefense.proofpoint.com/v2/url?u=https-3A__osf.io_4vfg7_&d=DwMDaQ&c=qS4goWBT7poplM69zy_3xhKwEW14JZMSdioCoppxeFU&r=b4Nb-lF5XBCiHWj64StekdJQgylGzYqrVQ9qwCO9n5Om_qHh04diXz6BW5PQjq3i&m=NGbZh8kPEQ97Y4he2ABoq02lgiLg4k5TLVs6hLN-vMQ&s=c-u2SoB9KzHYzwSvJ2gswvZZ0bhJrLEdHh-vSWTYq6g&e=)

I also like the overall thrust of this information:

[https://github.com/HBClab/LabManual](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_HBClab_LabManual&d=DwMDaQ&c=qS4goWBT7poplM69zy_3xhKwEW14JZMSdioCoppxeFU&r=b4Nb-lF5XBCiHWj64StekdJQgylGzYqrVQ9qwCO9n5Om_qHh04diXz6BW5PQjq3i&m=NGbZh8kPEQ97Y4he2ABoq02lgiLg4k5TLVs6hLN-vMQ&s=7K7OzOqyK1kxjB98I1xvF6FoOzbbYSznmSyx8iwlh_0&e=)

Besides explaining to people how to find what they need, I think it is helpful to articulate the skills they need.


##### Suggestions from Aziz 

[https://github.com/neu-spiral/SPIRAL-Handbook/wiki](https://urldefense.proofpoint.com/v2/url?u=https-3A__github.com_neu-2Dspiral_SPIRAL-2DHandbook_wiki&d=DwMDaQ&c=qS4goWBT7poplM69zy_3xhKwEW14JZMSdioCoppxeFU&r=b4Nb-lF5XBCiHWj64StekdJQgylGzYqrVQ9qwCO9n5Om_qHh04diXz6BW5PQjq3i&m=NGbZh8kPEQ97Y4he2ABoq02lgiLg4k5TLVs6hLN-vMQ&s=CXLD2Uh_BP_uOFFIieyWwf3_dFMWE_jgKsTMr8V-XT0&e=)


##### Suggestions from Serge 

[https://gate.nmr.mgh.harvard.edu/wiki/whynhow/index.php/Main_Page](https://gate.nmr.mgh.harvard.edu/wiki/whynhow/index.php/Main_Page)


##### Confluence server 

The current way to manage docs for CRL is via confluence: 

E.g. leko.tch.harvard.edu (only works via VPN) 

This is problematic because it does not give access for people to easily edit the webpages. Especially those that are not technical. 

The new proposal is: 



*   Our requirement is that CRL guide MUST be stored on Github 
    *   This enables any user with access to github to EASILY edit it 
    *   The language of github documentation is markdown, which is significantly easier to understand and edit than HTML 
    *   This format encourages everyone in the lab to use Github more often, which is a great and necessary skill for all in any case 
*   Optionally, the docs should be publishable in a web format; here are a couple of examples 
    *   Github Pages (Easiest) 
        *   The best option of the three presented here 
        *   [https://pages.github.com/](https://pages.github.com/)
    *   Conda (expensive) 
        *   [https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
        *   Published via ‘readthedocs.com’ -> can be edited directly on github 
        *   Need to find an open source company like this 
    *   Keras.io (only via Jupyter Notebooks) 
        *   [https://keras.io/guides/functional_api/](https://keras.io/guides/functional_api/)
        *   Write instructions as Jupyter Notebook, then export as Python file, then commit to Github repo, then setup a website that fetches this python file 
        *   The result is a webpage that has Google Collab code and github code. 


### [TODO] System Imaging Collaboratory - flywheel 

_TODO_

_[the following was suggested by Simon after he had read this guide]_

_- you should describe the Research Imaging Collaboratory, built on containerized image analysis pipeline and Flywheel from flywheel.io that we are currently installing._


### [TODO] CRL Github 

_TODO _



*   _Publish guidance on how to be added to CRL lab org github_


### [TODO] Reproducibility Series

_I am preparing a ‘Research Reproducibility Series’ for CRL in the coming weeks. _

_This will consist of collaborative workshops to learn the following tools (see below). _



*   _Tools _
    *   _Git _
        *   _Inc: Git 101, Github, Github pages, Videos _
    *   _Docker _
    *   _Conda _
    *   _Jupyter Lab _
    *   _Microsoft Visual Studio Code IDE _
    *   _Research Computing _
        *   _Using BCH Google Drive _
        *   _Using CPUs and GPUs _
    *   _Deep Learning _
        *   _Tricks and Tips (advanced) _
    *   _Overleaf _
*   _Research profile _
    *   _Google scholar, Harvard ID thing, Research Gate _
*   _Grant writing @ CRL _
    *   _Need to ask Simon to lead this _

_The series would be structured like this: _



*   _The group will meet each week to pick a particular topic for the next week, e.g. Github _
*   _A group lead will share some resources (suggested articles and videos) for the group to read _
*   _The participants will go away and learn on their own by reading / watching the suggested resources (and maybe finding more interesting stuff) _
*   _Each participant will also have their own individual mini project assigned for the week, so that they can learn on the topic._
*   _E.g. take your most recent paper and turn it into a github repository, make small modifications and push the changes, create a new branch, create TODO list _
*   _On the next week the group will meet to review progress, discuss, and pick a new topic with new mini project _

_The series would <span style="text-decoration:underline;">not </span>be structured as lectures. There is plenty of material online to learn from. Instead the series would be a collaborative effort to work together and support and discuss together. _

_After the series finishes the shared resources will be published on CRL github pages. _


### Misc

Tools to create flowcharts: 



*   Draw.io integration with Google Drive 

Tools to write Markdown files: 



*   https://stackedit.io/


-----------------------------------


## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/sergeicu/crl-guide/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/sergeicu/crl-guide/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
