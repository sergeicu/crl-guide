

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
