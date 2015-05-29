# Welcome!

Welcome to the Kharchenko lab! These are a few potentially useful tips and resources to help you get started. 

# Computing Resources

## Harvard `Orchestra`

The [`Orchestra`](https://rc.hms.harvard.edu/#orchestra) cluster is a shared high-performance computing environment serving a large research community with diverse research requirements and workflows. The cluster comprises more than 400 Linux compute nodes and 4500 cores, provides access to 10TB of disk space on a high-performance Isilon storage cluster for ongoing computational tasks, and allows for multiple job submissions via Platform Computing’s LSF resource management system, thereby allowing for powerful computations to be completed quickly. Tens of thousands of jobs run on the cluster every day! We work on `Orchestra` frequently so you will need to get an `Orchestra` account:

### Getting started on `Orchestra`

**Register for an eCommons ID**  
Go to http://ecommons.med.harvard.edu/ and follow guidelines for New User Registration. Your new eCommons ID will be emailed shortly.

**Register for an `Orchestra` account**  
Go to https://rc.hms.harvard.edu/account.html and use your new eCommons ID. New user accounts are added to the request tracking system queue, so it may take a few hours for them to set up your account.

Now you're ready to `ssh` onto `Orchestra` using your new eCommons ID and password:  
```
ssh your_eCommons_ID@orchestra.med.harvard.edu
```

### Additional useful tips and hints

**Lazy SSH**
Get to work faster! Life's too short to spent it typing out passwords. Set up [lazy `ssh`](http://jefworks.com/stupid-must-knows-lazy-ssh/) so you can log in to `Orchestra` or other virtual servers using short aliases and without being prompted for a password. 

Example `~/.ssh/config` file:  
```
Host or
   HostName orchestra.med.harvard.edu
   User your_eCommons_ID
   ServerAliveInterval 15
   ServerAliveCountMax 3
   ForwardX11 yes  
   ForwardX11Timeout 596h
```

We recommend enabling `X11` forwarding (`ForwardX11 yes`) so you can view the plots you generate as you're working. You may also need to prevent `X11` from timing out with the `ForwardX11Timeout 596h` option. We also recommend using `ServerAliveInterval` option to prevent "Write failed: Broken pipe" errors. The value `ServerAliveInterval` defines the interval in seconds between two operations that keeps to connection alive. Decrease this number if broken pipe errors persist.

**Using different software versions**
The proper way to load different software versions (for example, of `R`) on `Orchestra` is by loading as an environment module:  
```
module load stats/R/3.1.0
R
```  
Do not load from the installation directory such as `/opt/R-3.1.0/bin/R` as this may affected package dependencies and cause other issues.

**Setting up ESS**  

[ESS](http://ess.r-project.org/) is an add-on to emacs to allow easy editing of scripts while running R or other stat packages. Those who use emacs may want to consider setting up ESS to interact with R. 

To enable ESS, you will need to install it in your local directory such as your home directory:
```
cd /path/to/local_directory/
git clone https://github.com/emacs-ess/ESS.git 
cd ESS/
make
```

Modify `~/.emacs`
```
(add-to-list 'load-path "/path/to/local_directory/ESS/lisp/")
(load "ess-site")
```
You can also add to your load path a local themes library and load different [fun color themes](http://emacsthemes.caisah.info/)

Now when you create a new `.R` file with `emacs`, you can execute commands via `ESS` as usual with `C-c C-c`. 

**Managing your jobs**



## `pk` servers
We also have dedicated servers that are just for us! `pk` is a two-CPU Xeon server with 12TB of storage hosted at the Markely Group data center. To work on `pk`, you will need a different account:

### Getting started on `pk`

Ask Peter to get you an account. You will be able to get onto `pk` via `ssh`:
```
ssh your_username@pklab.med.harvard.edu
```  

### Additional useful tips and hints

Many of the tips and hints for `Orchestra` are also applicable for `pk` but here are a few additional tips and hints more relevant to `pk`. 

*** Using web-based R-studio ***  
To connect to the `pk` R-studio, you need to create a tunnel: 
```
ssh -L8787:localhost:8787  your_username@pklab.med.harvard.edu
```
Then you can open a browser and go to `localhost:8787` in order to access R-studio. You will have to sign in again using your `pk` credentials. 

Author: Jean Fan, Peter Kharchenko
