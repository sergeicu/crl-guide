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