# Yocto-Tutorial-Bootlin
Creating and customizing a Yocto Project involves several steps, including setting up your build environment, configuring your build, adding custom layers and recipes, and generating your desired image. Here’s a step-by-step tutorial to help you get started with Yocto.

material link: https://bootlin.com/doc/training/embedded-linux-qemu/embedded-linux-qemu-labs.pdf
## Building a cross-compiling toolchain
 - After this lab, you will be able to:
   - Configure the crosstool-ng tool
   - Xecute crosstool-ng and build up your own cross-compiling toolchain
  
  ### What is toolchain
    - a toolchain is a set of programming tools that are used to perform a complex software development task or to create a software product
    Getting Crosstool-ng
Let’s download the sources of Crosstool-ng, through its git source repository, and switch to a commit that
we have tested:
```
git clone https://github.com/crosstool-ng/crosstool-ng
cd crosstool-ng/
git checkout c5a17024
```
  ### Building and installing Crosstool-ng
``` ./bootstrap```  To generate configure script to get help use ```./ct-ng help```
  ### Configure the toolchain to produce
  

  
   
