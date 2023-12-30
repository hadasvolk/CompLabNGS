# Setting up my personal computational laboratory

Dear course participants, one of the main goals of this course is to give you a glimpse into bioinformatics software with emphasis on genomics and to allow you to run your own experiments without the need to use professionals or other bioinformatics service providers. To achieve this goal, we need to make you Linux terminal users! Yay!

Linux is the operating system (OS) of science and more specifically - bioinformatics. The reason for this is probably partially historical, but it is also heavily rooted in the core of Linux being open source project and its superior computational abilities over the more user friendly systems most of us use on a daily basis. The vast majority of bioinformatics software is written for Linux and meant to be run as a command line or terminal applications. This is less common than most other software we are used to that has graphical interfaces and are built to Windows or Mac systems. That being said, MacOS is somewhat close to Linux being a Unix-Like operating system. Thus, Mac users can probably work their way through this course without using Linux, but I won’t be able to provide any assistance if you get stuck or break something as I am not an apple fan.

In case you are already a Linux user you can jump ahead and make sure you have Anaconda installed. Your lab might have a Linux cluster or HPC system you can use and want to work on, or you have a virtual Linux machine on the cloud, in Google Colab/ AWS, etc. Either way as long as you have Linux and access to the internet you should be golden. Otherwise, I will assume most participants are familiar with Windows only and have a Windows PC/laptop at their disposal.

## Getting my own Linux terminal

### Windows Subsystem for Linux - Windows users only
Assuming the machine on which you will be working on is not extremely old, you should be able to enable [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) functionality and to download a Linux distribution (more on Linux distributions in our second session). In a nutshell, WSL is a virtualization technology that allows you to run a full Linux OS without leaving your Windows. It is probably the easiest and most convenient way to experiment with the Linux terminal without sacrificing the easiness and familiarity of our Windows system. How do I get WSL you might ask? You can follow [this guide from Microsoft](https://learn.microsoft.com/en-us/windows/wsl/install) or check out [NetworkChuck](https://www.youtube.com/watch?v=27Wn921q_BQ) he can guide you through the basics (no need to install Kali). Otherwise, Google and ChatGPT will for sure have a solution convenient for you.

### Virtual Machine - Windows and Mac
A second alternative is to install a full Linux desktop under a virtual machine. There are many virtual machine software, VMware, VirtualBox and others. There are many guides online on how to get ubuntu as a VM on your machine. One way is [here](https://www.youtube.com/watch?v=nvdnQX9UkMY).

### Dual Boot - Windows and Mac
A third alternative is to install Linux as a second OS on your machine. This is a bit more complicated and requires you to partition your hard drive and install Linux on a separate partition. This is a good option if you want to use Linux as your main OS and you are not afraid of a little bit of tinkering.

## How do we get bioinformatics software on Linux?
Like all applications, bioinformatics software is written in a programming language. Most of the software we will use is written in C, C++, Python, Perl, Java, R and other languages. The source code of these applications is available online and can be downloaded and compiled on your machine. This is a bit more complicated than just downloading an executable file and running it, but it is not too complicated. The main problem with this approach is that you will need to compile each software you want to use and make sure you have all the dependencies installed. This is a bit of a hassle and can be very time consuming. Luckily, there are package managers that can do this for us. A package manager is a software that can download and install other software and all of their dependencies. This is very convenient and allows us to install software with a single command. There are many package managers for Linux, but the most popular ones are apt-get (Debian/Ubuntu), yum (RedHat/CentOS) and pacman (Arch). These package managers are great for installing software that is not bioinformatics related, but they are not very good at installing bioinformatics software. This is where bioconda comes in.

### Anaconda/Miniconda
Once you have settled on a Linux terminal we would like to install [Anaconda](https://www.anaconda.com/). Anconda is a package manager that has a very cool channel called [bioconda](https://bioconda.github.io/). This will allow us to effortlessly download bioinformatics software without too much fuss. First install anaconda or miniconda. For most users the [**Quick install for LINUX**](https://docs.conda.io/projects/miniconda/en/latest/#quick-command-line-install) should work. Afterwards head to the bioconda landing page to finish the installation.

### Testing my installation
Once you have installed anaconda and bioconda you can test your installation by running the following command in your terminal:
```bash
conda install -c bioconda samtools
```
This will install the samtools software. Samtools is a very popular software for manipulating SAM/BAM files. We will learn more about these file formats in a later session. For now, we just want to make sure we can install software using bioconda. Once the installation is complete you can run the following command to make sure samtools is installed:
```bash
samtools --help
```
This should print the help menu of samtools. If you see the help menu you are good to go. If you get an error message, please search for a solution online or ask for help in the **Issues** tab above.

## Good luck!
