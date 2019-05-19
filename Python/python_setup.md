# Python3 and makefile install

## Python3 Install

This project uses python3 so you will want to make sure that is installed and added to your path. The easiest way to install python3 is through a software manager. For windows use [chocolatey](https://chocolatey.org/docs/installation) and for mac I use [Homebrew](https://brew.sh/). For mac you also need to have [xcode](https://developer.apple.com/xcode/) installed to use brew, so make sure to install that as well if you don't have it. Once you have a software manager you can run the install commands in terminal or powershell.

``` bash
# mac
brew install python3

# windows
choco install python3 -y
```

once it is installed `close and open` your terminal and run

``` bash
python3 --version
```

and you should get the vesrion of python. You have to close the terminal because when python is installed it gets added to your path, which is basically an alias for `usr/bin/python3.exe` or `c:\program files\python3\python.exe` or wherever you installed it, so you don't have to type in the full path to the executable and the extension, you just type in `python3` and it does the same thing. Your terminal may not update the path until you restart it, so best to restart the terminal any time you install something you plan to use in the terminal.

### Mac Users note

Macs come with python 2.7 installed by default, so if you run just `python` it will use python 2.7 and not python 3.x so make extra sure to use python3 when trying to run files or commands using python.

## Makefile install

Next you will want to install makefile so the make commands will work. If you don't want to install makefile you can just copy paste the commands from the file to terminal and they will work just fine.

``` bash
# mac
xcode-select --install

# windows
choco install make -y
```

