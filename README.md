# block_play_ml
ask-rse: supporting files and documentation for machine-learning-augmented block play application

## Installing dependencies
Instructions written for development version of block play application (for live inference and reaction to block arrangements) provided in zip archive `ZIP-2021-05-13-for-testing.zip` (SHA256 hash: 16b6c3f5f6c1f0ed104b6ff84d25856a9396e7355bc54a1dceba42d87f016409).

### Windows 10
To run the block play application  on Windows 10, a suitable environment containing a number of software packages must be created.
The packages can be installed directly using Python's [pip](https://pip.pypa.io/en/stable/) package manager using the provided [requirements.txt](./requirements.txt) file. 
However, it is recommened to use [conda](https://docs.conda.io/en/latest/) with the provided [environment.yml](./environment.yml) file (which includes the packages in [requirements.txt](./requirements.txt) to ensure that the correct version of Python is used.
