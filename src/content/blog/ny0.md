---
title: Ny0
date: 5/17/2024
---
## Content


## Python

### Notes

To use jupyter notebook in VS Code the ipykernel needs to be installed. The suggestion is to install in a virtual environment. The python installation is in /c/Python3.X wich is accessible to admin only. 

The questions pip vs conda vs anaconda referred to pipenv, virtualenv and other topics. In gen2 and gen3 laptops anaconda was installed and jupyter matlib was already present after selecting the anaconda kernel. If selecting another kernel the ipykernel did not work even if it was forced installed. 

In ASUS laptop there are three python installation: 
```
C:\Users\creeperpandatrex>where python
C:\Python312\python.exe
C:\Python311\python.exe
C:\Users\creeperpandatrex\AppData\Local\Microsoft\WindowsApps\python.exe
```

### commands to install pipenv as --user, not as admin. 

I tried

```
pip install pipenv with no --user

```

It did could not write on /c/Python3.10 location

Used instead

```
pip install pipenv --user

```

it installed in %appdata%\Python\Pythonn312\scripts. WARNING!!!


```
Installing collected packages: distlib, setuptools, platformdirs, filelock, certifi, virtualenv, pipenv
  WARNING: The script virtualenv.exe is installed in 'C:\Users\creeperpandatrex\AppData\Roaming\Python\Python312\Scripts' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The scripts pipenv-resolver.exe and pipenv.exe are installed in 'C:\Users\creeperpandatrex\AppData\Roaming\Python\Python312\Scripts' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed certifi-2024.2.2 distlib-0.3.8 filelock-3.14.0 pipenv-2023.12.1 platformdirs-4.2.2 setuptools-69.5.1 virtualenv-20.26.2
```

### Jupyter notebook

Now try jupyter notebook from VS Code