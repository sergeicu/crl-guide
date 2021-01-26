
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
