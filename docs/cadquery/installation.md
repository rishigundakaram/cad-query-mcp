<a id="installation"></a>

# Installing CadQuery

To install both Cadquery and CQ-Editor together with a single installer see the instructions below [Adding a Nicer GUI via CQ-editor]().

CadQuery may be installed with either conda or pip.  The conda installation method is the better tested and more mature option.

## Install via conda

Begin by installing the conda package manager.  If conda is already installed skip to [conda]().

### Install the Conda Package Manager

In principle, any Conda distribution will work, but it is probably best to install [Miniforge](https://github.com/conda-forge/miniforge) to a local directory and to avoid running conda init.  After performing a local directory installation, Miniforge can be activated via the [scripts,bin]/activate scripts. This will help avoid polluting and breaking the local Python installation.

Miniforge is a minimal installer that sets *conda-forge* as the default channel for package installation and provides [mamba](https://mamba.readthedocs.io/en/latest/user_guide/mamba.html).  You can swap almost all commands between conda & mamba.

In Linux/MacOS, the local directory installation method looks something like this:

```default
# Install to ~/miniforge
curl -L -o miniforge.sh "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
bash miniforge.sh -b -p $HOME/miniforge

# Activate
source $HOME/miniforge/bin/activate
```

On Windows, download the installer and double click it on the file browser or install non-interactively as follows:

```default
:: Install to %USERPROFILE%\Miniforge
curl -L -o miniforge.exe https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe
start "" /wait miniforge.exe /InstallationType=JustMe /RegisterPython=0 /NoRegistry=1 /NoScripts=1 /S /D=%USERPROFILE%\Miniforge

:: Activate
cmd /K ""%USERPROFILE%/Miniforge/Scripts/activate.bat" "%USERPROFILE%/Miniforge""
```

```default
# Install to $env:USERPROFILE\Miniforge
curl.exe -L -o miniforge.exe https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe
Start-Process -Wait -FilePath miniforge.exe -ArgumentList @("/InstallationType=JustMe", "/RegisterPython=0", "/NoRegistry=1", "/NoScripts=1", "/S", "/D=$env:USERPROFILE\Miniforge")

# Activate
. $env:USERPROFILE\Miniforge\shell\condabin\conda-hook.ps1
conda activate
```

It might be worthwhile to consider using `/NoScripts=0` to have an activation shortcut added to the start menu.

After conda installation, create and activate a new [conda environment](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) to prepare for cadquery installation.

### conda

`mamba install` is recommended over `conda install` for faster and less memory intensive cadquery installation.

Install the latest released version of cadquery:

```default
conda create -n cq
conda activate cq
mamba install cadquery
```

or install a given version of cadquery <sup>[1](#f1)</sup>:

```default
conda create -n cq231
conda activate cq231
mamba install cadquery=2.3.1
```

or install the latest dev version:

```default
conda create -n cqdev
conda activate cqdev
mamba install -c cadquery cadquery=master
```

Add the *conda-forge* channel explicitly to the install command if needed (not using a miniforge based conda distribution).

## Install via pip

CadQuery can be installed via pip on Linux, MacOS and Windows. Python versions 3.9 and newer are supported by CadQuery, however a bleeding-edge Python installation may be broken due to lagging support in CadQuery’s complex set of dependencies. If the pip installation method does not work for your system, you can try the conda installation method above.

It is highly recommended that a virtual environment is used when installing CadQuery, although it is not strictly required. Installing CadQuery via pip requires an up-to-date version of pip, which can be obtained with the following command line (or a slight variation thereof).:

```default
python3 -m pip install --upgrade pip
```

Once a current version of pip is installed, CadQuery can be installed using the following command line.:

```default
pip install cadquery
```

It is also possible to install the very latest changes directly from CadQuery’s GitHub repository, with the understanding that sometimes breaking changes can occur. To install from the git repository, run the following command line.:

```default
pip install git+https://github.com/CadQuery/cadquery.git
```

You should now have a working CadQuery installation, but developers or users who want to use CadQuery with IPython/Jupyter or to set up a developer environment can read the rest of this section.

If you are installing CadQuery to use with IPython/Jupyter, you may want to run the following command line to install the extra dependencies.:

```default
pip install cadquery[ipython]
```

If you want to create a developer setup to contribute to CadQuery, the following command line will install all the development dependencies that are needed.:

```default
pip install cadquery[dev]
```

## Adding a Nicer GUI via CQ-editor

If you prefer to have a GUI available, your best option is to use
[CQ-editor](https://github.com/CadQuery/CQ-editor).

You can download the newest build [here](https://github.com/CadQuery/CQ-editor/releases/tag/nightly). Install and run the *run.sh* (Linux/MacOS) or *run.bat* (Windows) script in the root CQ-editor directory. The CQ-editor window should launch.

### Linux/MacOS

1. Download the installer (.sh script matching OS and platform).
2. Select the script in the file browser and make executable.  Choose **Properties** from the context menu and select **Permissions**, **Allow executing file as a program** (or similar, this step varies depending on OS and window manager).
3. Select the script in the file browser and choose **Run as Program** (or similar).

   Follow the prompts to accept the license and optionally change the installation location.

   The default installation location is `/home/<username>/cq-editor`.
4. Launch the **run.sh** script from the file brower (again make executable first and then run as program).

To install from command line, download the installer using curl or wget or your favorite program and run the script.:

```default
curl -LO https://github.com/CadQuery/CQ-editor/releases/download/nightly/CQ-editor-master-Linux-x86_64.sh
sh CQ-editor-master-Linux-x86_64.sh
```

To run from command.:

```default
$HOME/cq-editor/run.sh
```

### Windows

1. Download the installer (.exe) and double click it on the file browser.

   Follow the prompts to accept the license and optionally change the installation location.

   The default installation location is `C:\Users\<username>\cq-editor`.
2. Launch the **run.bat** script from the file brower (select **Open**).

To run from command line, activate the environment, then run cq-editor:

```default
C:\Users\<username>\cq-editor\run.bat
```

### Installing extra packages

*mamba*, and *pip* are bundled with the CQ-editor installer and available for package installation.

First activate the environment, then call mamba or pip to install additional packages.

On windows.:

```default
C:\Users\<username>\cq-editor\Scripts\activate
mamba install <packagename>
```

On Linux/MacOS.:

```default
source $HOME/cq-editor/bin/activate
mamba install <packagename>
```

## Adding CQ-editor to an Existing Environment

You can install CQ-editor into a conda environment or Python virtual environment using conda (mamba) or pip.

Example cq-editor installation with conda (this installs both cadquery and cq-editor):

```default
conda create -n cqdev
conda activate cqdev
mamba install -c cadquery cq-editor=master
```

Example cq-editor installation with pip:

```default
pip install PyQt5 spyder pyqtgraph logbook
pip install git+https://github.com/CadQuery/CQ-editor.git
```

## Jupyter

Viewing models in Jupyter is another good option for a GUI.  Models are rendered in the browser.

The cadquery library works out-of-the-box with Jupyter.
First install cadquery, then install [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html) in the same conda or Python venv.:

conda

> ```default
> mamba install jupyterlab
> ```

pip

> ```default
> pip install jupyterlab
> ```

Start JupyterLab:

```default
jupyter lab
```

JupyterLab will open automatically in your browser.  Create a Notebook to interactively edit/view CadQuery models.

Call `display` to show the model.:

```default
display(<Workplane, Shape, or Assembly object>)
```

## Test Your Installation

If all has gone well, you can open a command line/prompt, and type:

```default
$ python
>>> import cadquery
>>> cadquery.Workplane('XY').box(1,2,3).toSvg()
```

You should see raw SVG output displayed on the command line if the CadQuery installation was successful.

#### NOTE
* <a id='f1'>**[1]**</a> Older releases may not be compatible with the latest OCP/OCCT version.  In that case, specify the version of the dependency explicitly.  ```default mamba install cadquery=2.2.0 ocp=7.7.0.* ```
