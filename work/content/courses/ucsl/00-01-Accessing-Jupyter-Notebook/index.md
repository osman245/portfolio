### Acessing Jupyter Notebook on CUSP CDF (preferred way)
Depending on the Operating System that you are using, you should simply follow the instructions on cusp datahub.

For Linux and Mac OS: https://datahub.cusp.nyu.edu/sites/default/files/documents/guides/Jupyter_Notebook_from_your_browser_Mac.pdf
For Windows OS: 
https://datahub.cusp.nyu.edu/sites/default/files/documents/guides/Jupyter_Notebook_from_your_browser_Windows.pdf
All the packages that we need to use are already installed for you.

### Setting Up Jupyter Notebook locally on your machine (Method 1)

If you are familiar with Docker, then there is a pre-built container that you can use following the instructions here: https://github.com/Mohitsharma44/ucsl-image

### Setting Up Jupyter Notebook locally on your machine (Method 2)


These instructions can be followed only if you are using either a Mac OS or Linux based OS

#### Mac OS
- Installing Brew (if you already don't have it)
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
- Update Brew:
`brew update
- Install Python
```
brew install python
``` 
> (or `brew install python3` if you want to use python3)

#### Linux Flavored OS (assuming Ubuntu)
- Using your favorite package manager install Python
```
sudo apt-get install python
```
> (or `sudo apt-get install python3` if you want to use python3)

- Install python package manager
```
sudo apt-get install python-pip
```
> (or `sudo apt-get install python3-pip` if you want to use python3)

#### Common Commands for Mac and Linux 
> (even windows if you have managed to install python and pip on it)

- Install jupyter
```
pip install jupyter
```
> (or `pip3 install jupyter` if you want to use python3)

- Installing Numpy, Matplotlib, Scipy, Pandas
```
pip install numpy matplotlib scipy pandas packages
```
> (use `pip3` for python3)

> If, for Linux flavored OS, the above command gives you a dependency error, replace it with
```
sudo apt-get install python-<package name>
```

----------

If you want to have an option of using either python2 or python3, run:
```
python2 -m pip install ipykernel
python2 -m ipykernel install --user
```
> - replace `python2` with `python3` if you ran all the above commands for python3
> - remember to install the "packages" for python2 and python3

> Remember .. No matter where you set up your development environment, the assignments have to be uploaded on CDF (check the Welcome notebook for more instructions)
