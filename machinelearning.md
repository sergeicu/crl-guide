

### NVIDIA 

Each GPU enabled machine would have its own NVIDIA drivers. 

As always, you will need to match your CUDA toolkit to the driver.

For your own machine - it would not be so difficult. 

 

The problem may start to arise if you want to `ssh` into another machine to use its GPU - as you will need to match to its driver and your CUDA toolkit also.This is where things may start breaking down. That's where conda may come handy. Or a smart '.bashrc' script. 

I guess you won't be needing help on this first, but if you have some problems later - let me know i may be able to help. 


















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




#### JupyterLab 

I personally use jupyter lab for prototyping in python and bash scripting. 

If you are planning to work with python - I can give you a tutorial on how to setup jupyter lab for remote work.

It is extremely convenient tool because you do NOT need VNCserver in this case. 

Simply you can access your BCH computer via Jupyter Lab (in Chrome browser). 


#### VScode 

I use VScode as my preferred IDE for more complex development. It has a lot of nice debugging tools, similar to PyCharm or Eclipse. 

However, it has amazing features for remote work. For example I do not need to use VNCserver. I can start VScode on my laptop and work with my code and data directly as if I was at the office. 






### CONDA

The most useful tool of all for me had been `conda/anaconda`. 

In most cases I was able to virtualize everything via conda, without having to run `yum` or `snap`. 

As you probably know, conda can be used to manage dependencies between packages that are <span style="text-decoration:underline;">not </span>only python. 

Typically, if I want to install any new software, I always google search first for `&lt;library_name> conda`. 




### Reading Images

Alternatively, if you want to have more control <span style="text-decoration:underline;">and  </span>you need to perform MRI image operations INSIDE your C++/Python code - use `​ITK`. 

ITK has many tools for working with nifti related files - including managment of header related items - such as orientation, affine matrices, etc. 

This is also in my bash. 

Or, you can also use `pynnrd` or `nibabel` libraries for working with .nrrd and .nii.gz files respectively. 

You can install these via `conda`. I prefer this over ITK. 
