
* * *
## Howto install and manage several Python versions 

This howto installs a new Python version on a system where a different python is already installed. 

Download Python tarball from the [python website](http://www.python.org) and uncompress it: 
    
    $ tar zxvf Python-2.7.5.tgz

Compile Python and point into the configure script which directory will be used as destination folder. 

    $ cd Python-2.7.5
    $ ./configure --prefix=/opt/python27
    $ make
    $ sudo make install

Create (or update) the alternative file: (assuming our already installed version is located on _/usr/bin/python2.6_): 
 
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.6 10
    sudo update-alternatives --install /usr/bin/python python /opt/python27/bin/python2.7 50

Where: 

* /usr/bin/python is the location where the link pointing to /etc/alternatives/python will be created. This file is usually created on a directory that belongs the $PATH variable. 
* _python_ is the new entry on /etc/alternatives
* _/usr/bin/python2.6_ and _/opt/python27/bin/python2.7_ are the two Python binaries installed on the system: python2.6
    installed from the repository and python2.7 installed manually.
* 10 and 50 are the priorities. Alternatives will use the entry with highest priority (python2.7 in our example) 

From now on, when we type _python_ on console, we will run python2.7. 

In case we want to switch between versions, for example use 2.6 instead of 2.7: 

    sudo update-alternatives --config python 

the system will show a menu where we can select which version we want to make the default one: 


    There are 2 choices for the alternative python (providing /usr/bin/python).

      Selection    Path                         Priority   Status
      ------------------------------------------------------------
          * 0            /opt/python27/bin/python2.7   50        auto mode
            1            /opt/python27/bin/python2.7   50        manual mode
            2            /usr/bin/python2.6            10        manual mode 

          Press enter to keep the current choice[*], or type selection number: 2
          update-alternatives: using /usr/bin/python2.6 to provide /usr/bin/python

So, now typing _python_ on console means we run Python 2.6.

Finally, in case we want to install a third python version (let's say 3.4) and make it the default one: 

    $ cd Python-3.4
    $ ./configure --prefix=/opt/python34
    $ make
    $ sudo make install
    $ sudo update-alternatives --install /usr/bin/python python /opt/python34/bin/python3.4 60


