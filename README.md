# Yocto-Tutorial
Creating and customizing a Yocto Project involves several steps, including setting up your build environment, configuring your build, adding custom layers and recipes, and generating your desired image. Here’s a step-by-step tutorial to help you get started with Yocto.

material link: https://bootlin.com/doc/training/embedded-linux-qemu/embedded-linux-qemu-labs.pdf
## Building a cross-compiling toolchain
 - After this lab, you will be able to:
   - Configure the crosstool-ng tool
   - execute crosstool-ng and build up your own cross-compiling toolchain
  
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
  ```
./configure --enable-local
  make
```
  used during the build process of some software, especially open-source projects.

  - if U got this error while configure

![image](https://github.com/Rabie45/Yocto-Tutorial/assets/76526170/db8173f3-71ba-4882-bcec-4af995e48ea8)

Use this command ```sudo apt install libtool-bin libtool-doc```
  ### Configure the toolchain to produce
A single installation of Crosstool-ng allows to produce as many toolchains as you want, for different architectures, with different C libraries and different versions of the various components.
  - Go to target options press ```space```
 ![image](https://github.com/Rabie45/Yocto-Tutorial/assets/76526170/2642451f-a640-4158-bea8-18e0583c6011)
  - Go to Target Arch
![image](https://github.com/Rabie45/Yocto-Tutorial/assets/76526170/cb951c4e-b5b1-46f5-9470-b6a1363414ab)
  - Move to arm press ```space```
![image](https://github.com/Rabie45/Yocto-Tutorial/assets/76526170/f70ec198-47a8-467a-ad5e-11edcc27071e)
Produce the toolchain
        -  ```./ct-ng build``` to build the crosstool
Your compiler has been built now

   ### Bootloader - U-Boot
       - **s a widely used and popular open-source bootloader specifically designed for embedded systems running Linux.**
```
git clone https://gitlab.denx.de/u-boot/u-boot
cd u-boot
git checkout v2023.01
export CROSS_COMPILE=arm-linux-gnueabihf-
make menuconfig
```
![image](https://github.com/Rabie45/Yocto-Tutorial/assets/76526170/c8b2f0a7-4919-4141-b729-69ccd1b3d266)
![image](https://github.com/Rabie45/Yocto-Tutorial/assets/76526170/fe2abea3-b322-444b-aacb-32926d620af3)

press ```/``` to search for the variables

``` sudo apt install qemu-system-arm``` to download qemu arm

```qemu-system-arm -M vexpress-a9 -m 128M -nographic -kernel u-boot```
• -M: emulated machine
• -m: amount of memory in the emulated machine
• -kernel: allows to load the binary directly in the emulated machine and run the machine with it. This
way, you don’t need a first stage bootloader. Of course, you don’t have this with real hardware


 ### Yocto
 
   - Yocto Project is an open-source collaborative effort aimed at creating custom Linux distributions for embedded systems and Internet of Things (IoT) devices. It's a popular choice for developers due to its flexibility, 
      wide hardware support, and community backing. the manual https://docs.yoctoproject.org/
   - Types of Yocto Components:
 - Recipes: These are the fundamental components containing instructions on how to build a specific piece of software. Recipes typically include:

      Downloading source code
      Configuring build options
      Compiling the software
    Packaging the resulting binaries and libraries
     Packages: These are the final outputs of recipes, containing compiled executables, libraries, and other files needed by an application.

     - Layers: Yocto Project employs a layered approach where recipes are organized into layers. Layers can be:

      - Machine-specific: Containing recipes for components specific to a particular hardware platform.
      - Board-support packages (BSPs): Providing hardware abstraction layers and drivers for specific boards.
      - Software-specific: Offering recipes for specific software packages or libraries.


 ### Yocto Installation:
   ### First:

 - make directory and give it a name (source) using this command

   ```mkdir source ```
   
 - then go to the directory u just created using this command

   ``` cd source ```


 - use the command shown in the documentation (https://docs.yoctoproject.org/2.1/yocto-project-qs/yocto-project-qs.html#yp-resources)
   
   ![1](https://github.com/Rabie45/Yocto_installation/assets/76526170/dba62a8c-ba33-485a-b102-4c467de6e996)


then clone poky repo (Poky is closely related to the Yocto Project for embedded Linux development. Here’s how they connect:
Yocto Project: This is the overarching framework that provides tools, processes, and metadata to build custom embedded Linux distributions.
Poky: Think of Poky as the reference implementation of the Yocto Project. It serves as a foundation and example, showcasing how to use Yocto Project features. Poky includes essential components)

``` git clone git://git.yoctoproject.org/poky```

![image](https://github.com/Rabie45/Yocto_installation/assets/76526170/5678f468-2e31-4dea-a3c8-a9c5228bd46f)



then check out the branch using this command

``` git checkout krogoth  ```


then initialize build environment as shown in documentation using
the additional build command to create a file called build and build the file on it

``` source oe-init-build-env ../../build  ```

![image](https://github.com/Rabie45/Yocto_installation/assets/76526170/da5bcf8c-da48-4906-ba5b-fc3f8389a2f2)


it must be looks like that

now you can try to write bitbake to see if it works or not

``` bitbake -h  ```

![image](https://github.com/Rabie45/Yocto_installation/assets/76526170/e2af4567-c763-4011-a077-5ccbb7d65f30)

if you got error like that

```traceback (most recent call last): File “/home/rabi3/Desktop/source/poky/bitbake/bin/bitbake”, line 19, in <module> import bb File “/home/rabi3/Desktop/source/poky/bitbake/lib/bb/init.py”, line 74, in <module> import bb.msg File “/home/rabi3/Desktop/source/poky/bitbake/lib/bb/msg.py”, line 20, in <module> import bb.event File “/home/rabi3/Desktop/source/poky/bitbake/lib/bb/event.py”, line 23, in <module> import bb.compat File “/home/rabi3/Desktop/source/poky/bitbake/lib/bb/compat.py”, line 7, in <module> from collections import MutableMapping, KeysView, ValuesView, ItemsView, OrderedDict ImportError: cannot import name ‘MutableMapping’ from ‘collections’ (/usr/lib/python3.10/collections/init.py) ```
you can use this command 


this is because you use python 3 which have deprecated functions so you have to use old distro with python 2.7 and this mentioned in the documentation
use this command 

```  sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1 ```

it would make python2.7.1 as default

the last step is to run this command to build



```bitbake core-image-minimal ```

![image](https://github.com/Rabie45/Yocto_installation/assets/76526170/cbc37d71-825d-4633-b5cf-c57ccd4f4249)

the command
 ``` bitbake core-image-minimal ```
 is used in the Yocto Project with Poky to build a specific type of embedded Linux system image.

if you got this issue 

![image](https://github.com/Rabie45/Yocto_installation/assets/76526170/7e7143e6-bf1b-46ee-8983-7818c6f8d1f6)

use this command 
``` sudo apt-get install zstd lz4 ```

and it may take a while (may be 4 hours).
### Layer:

a layer is a fundamental organizational unit that groups related recipes together.  These layers play a crucial role in managing the software components that make up your custom embedded Linux distribution.
## First create layer
 - ```bitbake-layers create-layer ../meta-custom``` To create the layer
   ![image](https://github.com/Rabie45/Custom-yocto-image/assets/76526170/aca483a0-f80a-4ab9-876f-766a39f9f433)

 - ```bitbake-layers add-layer ../meta-custom```   to add a new layer in Yocto simplifies the process of managing layers in your build environment.
   
   ![image](https://github.com/Rabie45/Custom-yocto-image/assets/76526170/53866b2e-e16d-4368-8932-9cfda1c794a1)

 - ```mkdir -p meta-diploma/recipes-core/``` to add some core files 
 - ```mkdir -p meta-diploma/recipes-core/images/``` to add the customized image
 - ```touch customize-minimal.bb```
 -
``` include recipes-core/images/core-image-minimal.bb
IMAGE_FEATURES += " ssh-server-dropbear "
IMAGE_INSTALL += " strace"
```
- include core-image-minimal configration
- add feature ssh
- add strace
- ```mkdir -p meta-diploma/recipes-core/base-files/```  to append your hostname to the image
- ```touch meta-diploma/recipes-core/base-files/base-files_%.bbappend ``` file name must have the same format
- open file add ```hostname = "YOUR HOST NAME" ```
- go to build file ``` cd build/```
- run ```bitbake customize-minimal```
- ![image](https://github.com/Rabie45/Custom-yocto-image/assets/76526170/2cf3dd8a-dca3-40e4-b9a0-30c16f05b344)
- run ```runqemu qemux86-64```

https://github.com/Rabie45/Custom-yocto-image/assets/76526170/afdbe420-f53a-4512-8572-0784487f7040

### Recipes: (وصفه)
 a recipe is the fundamental building block used to define how a specific piece of software gets included in your custom Linux distribution for embedded systems. It acts like a blueprint containing all the instructions and information necessary for the Yocto Project build system (BitBake) to download, configure, compile, and package the software.
How to add recipes to ur yocto project 
Recipes extention .bb
Example 
```
SUMMARY = "bitbake-layers recipe"
DESCRIPTION = "Recipe created by bitbake-layers"
LICENSE = "MIT"

python do_display_banner() {
    bb.plain("***********************************************");
    bb.plain("*                                             *");
    bb.plain("*  Example recipe created by bitbake-layers   *");
    bb.plain("*                                             *");
    bb.plain("***********************************************");
}

addtask display_banner before do_build
````
this explanation from gemini
SUMMARY = "bitbake-layers recipe": This line defines a short description of the recipe. It simply states that this recipe was created by bitbake-layers.
Description:

DESCRIPTION = "Recipe created by bitbake-layers": This line provides a more detailed description of the recipe. Again, it emphasizes the origin of the recipe.
License:

LICENSE = "MIT": This line specifies the license under which the software built by this recipe is distributed. In this case, it's the MIT License.
Python function:

python do_display_banner() { ... }: This defines a Python function named do_display_banner. The function body consists of several lines using the bb.plain function (likely from BitBake).
Function body:

bb.plain("***********************************************");: This line prints a line of asterisks to the console using the bb.plain function. This function is commonly used in BitBake recipes for informational or decorative purposes.
bb.plain("*                       *");: This line prints two lines with spaces and asterisks, likely creating a border around the banner message.
bb.plain("* Example recipe created by bitbake-layers  *");: This line prints the core message of the banner, indicating that this is an example recipe.
The lines following the first three with asterisks repeat the same pattern, likely forming a bottom border for the banner.
Adding the task:

addtask display_banner before do_build: This line instructs BitBake to execute the do_display_banner function as a task named display_banner. The before do_build part specifies that this task should run before the actual build process (do_build) starts.


### How to add a script to work with system v
what is systemv: https://www.youtube.com/watch?v=N1vgvhiyq0E
## Steps 
 - Go to the layer that you would create the project in
 - ```mkdir hello-startup-sv```
 - ``` cd hello-startup-sv``` then create the recipe ```touch hello-startup-sv.bb```
 - in hello-startup-sv.bb
``` SUMMARY = " Hello python"
LICENSE = "CLOSED"

SRC_URI = "file://startup-sv.sh \
file://hello-startup.py \
"


S = "${WORKDIR}"
RDEPENDS:${PN} = "python3 "
inherit update-rc.d
INITSCRIPT_NAME = "start-python"

INITSCRIPT_PARAMS = "start 99 5 . stop 0 1 6 ."

do_install(){
    install -d ${D}${sysconfdir}/init.d
    install -m 0755 ${WORKDIR}/startup-sv.sh ${D}${sysconfdir}/init.d/start-python
    install -d ${D}${bindir}
    install -m 0755 hello-startup.py ${D}${bindir}
}
```
 - Give the bash script to switch about parameter u based to the script
 - And the python  script it self
 - RDEPENDS:${PN} In Yocto, RDEPENDS is used to specify runtime dependencies for a package. To ensure that your package depends on Python 3 at runtime, you can use the RDEPENDS variable in your recipe file
 - ```mkdir files``` to put the scripts in
 - inherit update-rc.d (https://docs.yoctoproject.org/dev-manual/new-recipe.html   5.14)
![image](https://github.com/Rabie45/Yocto-image-with-startup/assets/76526170/1a98d5e4-8b98-4a11-83ac-093abef11085)

### How to add a script to work with systemd
systemd explination: https://www.youtube.com/watch?v=pPKdXw3Vg3c
## Steps 
 - Go to the layer that you would create the project in
 - ```mkdir hello-startup-sv```
 - ``` cd hello-startup-sv``` then create the recipe ```touch hello-startup-sv.bb```
 - in hello-startup-sv.bb
``` SUMMARY = " Hello python"
LICENSE = "CLOSED"

SRC_URI = "file://hello-startup-sysd.py \
file://sd-start.service\
"


S = "${WORKDIR}"
RDEPENDS:${PN} = "python3 "
inherit systemd


INITSCRIPT_PARAMS = "start 99 5 . stop 0 1 6 ."

do_install(){
    install -d ${D}${systemd_system_unitdir}
    install -m 0744 ${WORKDIR}/sd-start.service ${D}${systemd_system_unitdir}
    install -d ${D}${bindir}
    install -m 0744 hello-startup-sysd.py ${D}${bindir}
}
SYSTEMD_PACKAGES = "${PN}"
SYSTEMD_AUTO_ENABLE ??= "enable"
SYSTEMD_SERVICE:${PN} = "sd-start.service"
```
 - Create the service
```
[Unit]
Description="Hello world sysd"

[Service]
ExecStart=python3 /usr/bin/hello-startup-sysd.py






 
 




  

  
   
