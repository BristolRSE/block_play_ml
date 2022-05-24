# block_play_ml
ask-rse: supporting files and documentation for machine-learning-augmented block play application

## Installing dependencies
Instructions written for development version of block play application (for live inference and reaction to block arrangements) provided in zip archive `ZIP-2021-05-13-for-testing.zip` (SHA256 hash: 16b6c3f5f6c1f0ed104b6ff84d25856a9396e7355bc54a1dceba42d87f016409).

### Windows 10
To run the block play application  on Windows 10, a suitable environment containing a number of software packages must be created.
The packages can be installed directly using Python's [pip](https://pip.pypa.io/en/stable/) package manager using the provided [requirements.txt](./requirements.txt) file. 
However, it is recommended to use [conda](https://docs.conda.io/en/latest/) with the provided [environment.yml](./environment.yml) file (which includes the packages in [requirements.txt](./requirements.txt) to ensure that the correct version of Python is used).

The following instructions use the conda package manager and PowerShell to install the required packages.

#### Install Microsoft Visual C++ compiler
The block play application depends on the [Python API for the COCO dataset](https://github.com/cocodataset/cocoapi), distributed as the [pycocotools](https://pypi.org/project/pycocotools/) package. Installation of this package requires a C/C++ compiler, which on Windows can be installed with [Visual Studio](https://visualstudio.microsoft.com/) or [Build Tools for Visual Studio](https://visualstudio.microsoft.com/downloads/).


##### Install with Build Tools for Visual Studio
If you do not have a recent version of Visual Studio installed, installation of Build Tools for Visual Studio is recommended, since this only installs the required command line tools.

* Download "Build Tools for Visual Studio 2019" from the [Visual Studio Downloads page](https://visualstudio.microsoft.com/downloads)
  - Under "All Downloads", select "Tools for Visual Studio 2019"
  - Select the "Download" option for "Build Tools for Visual Studio 2019"
* Open the downloaded file (you may need administrative privileges on your machine to do this) and follow instructions
  - When you are given the opportunity to select components to install, **tick the box next to "Desktop development with C++" workload**
  - Proceed with installation (this may take some time to complete)

##### Modify existing Visual Studio installation
**Skip this section if you installed Build Tools for Visual Studio as described above.**

If you already have a recent version of Visual Studio installed, you may be able to modify the existing installation to add the required command line tools.

* Open "Visual Studio Installer" from the Start menu
* Select the "Modify" button in the Visual Studio 2019 box
* **Tick the box next to "Desktop development with C++" under "Workloads"**
* Select "Install" in the bottom right of the window

#### Install Miniconda3
The block play application depends on a number of packages (see [requirements.txt](./requirements.txt)). It requires specific versions of packages which place constraints on the version of the Python language which can be used. In particular, Python 3.7 is the latest version of Python supported by [TensorFlow 1](https://www.tensorflow.org/versions). 

The [conda](https://docs.conda.io/en/latest/) package manager enables us to easily install the correct Python version to satisfy the block play application's dependencies in an isolated environment without impacting other versions of Python which may be present on the system.

If conda is already installed (e.g. through an [Anaconda](https://www.anaconda.com/) distribution or an existing [Miniconda](https://docs.conda.io/en/latest/miniconda.html) installation), you may be able to skip this step and proceed straight to installing packages (below).

* Download Miniconda (Miniconda3 Windows 64-bit) from the [Miniconda downloads page](https://docs.conda.io/en/latest/miniconda.html)
  - Select the download for the latest Python version, 3.9 (this does not affect the version we will use, since conda will automatically install the correct version)
* Run the installer
  - Accept the license
  - Select "Just Me" option for installation
  - **Do not** select the option to modify the PATH variable (unnecessary)

After installation, you can test the conda installation by selecting "Anaconda Powershell Prompt (miniconda3)" from the Start Menu. This should open a command prompt that looks like
```PowerShell
(base) PS C:\Users\User>
```

At the command prompt, type `python` and press enter to run the Python interpreter. 
An Anaconda-branded Python interpreter prompt should open. This should look something like the following:
```
Python 3.9.1 (default, Dec 11 2020, 09:29:25) [MSC v.1916 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
Now type `quit()` and press enter to exit Python.

#### Install packages using conda
> **NOTE** In the following, lines to be typed at a PowerShell prompt ("Anaconda Powershell Prompt (miniconda3)" from the Start menu) will be shown starting with `>` and lines to be typed in a Python interpreter prompt (started in the PowerShell session) will start with `>>>`.

We will install the dependencies of the block play application (including Python 3.7.x) in a [conda environment](https://conda.io/projects/conda/en/latest/user-guide/concepts/environments.html).
This will allow the specific required versions to be installed in an isolated environment, separate from other versions of the packages that might be installed on the system. 

Download the [environment.yml](./environment.yml) and [requirements.txt](./requirements.txt) files (either clone the repository with [Git](https://git-scm.com/), or directly download the files).
The files must be placed in the same directory (this is automatic if cloning with Git).

In the Anaconda PowerShell Prompt, set the current directory to the location of the `environment.yml` and `requirements.txt` files, e.g.
```PowerShell
> Set-Location -Path C:\Users\User\block_play_app\
```
Then, create the conda environment using the following command
```PowerShell
> conda env create --file environment.yml
```
This will create a new conda environment called `block_play_env` and may take a few minutes to complete.

To check that the environment has been successfully created, activate it
```PowerShell
> conda activate block_play_env
```
The PowerShell prompt should now be prefixed by the environment name, e.g.
```PowerShell
(block_play_env) PS C:\Users\User>
```

With `block_play_env` activated, start the Python interpreter
```PowerShell
> python
```
This time, a Python 3.7.x interpreter should open, looking something like this
```
Python 3.7.10 | packaged by conda-forge | (default, Feb 19 2021, 15:37:01) [MSC v.1916 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
To check that the key dependency TensorFlow can be imported, type the following commands at the Python prompt
```python
>>> import tensorflow
>>> tensorflow.__version__
```
which should return
```python
'1.15.0'
```
You can ignore any warning messages about being unable to load a cudart dynamic library (this happens if your machine lacks a GPU).
Exit the Python interpreter
```python
>>> quit()
```

#### Run application
To use the block play application, create a directory in which to store the application files and then extract the zip archive containing the application (`ZIP-2021-05-13-for-testing.zip`) into this directory.
This can be done using Windows File Explorer, or using the following PowerShell commands
```PowerShell
> New-Item -Path C:\Users\<username>\block_play_app -ItemType Directory
> Expand-Archive -Path ZIP-2021-05-13-for-testing.zip -DestinationPath C:\Users\<username>\block_play_app
```
where `C:\Users\<username>\block_play_app` is the directory in which the application will be installed (you may want to change this) and `<username>` is your Windows username.

Change the current working directory to the location of the block play app, e.g.
```PowerShell
> Set-Location -Path C:\Users\User\ask-rse\block_play_app\ZIP-2021-05-13-for-testing\
```
Activate the conda environment previously created (if not already active)
```PowerShell
> conda activate block_play_env
```
then start the block play application
```PowerShell
> python main.py
```
If the previous setup steps have been successful, the application should output text to the terminal for a short while and then open a GUI window displaying webcam input which can be used to control the application.

> **NOTE** You may need to modify the value of `camera_idx` in the block play application's `main.py` file to avoid an error occurring immediately after the GUI appears.
> For example, while testing with a single webcam connected, it was necessary to change this from 1 to 0.
