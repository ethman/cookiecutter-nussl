# Cookiecutter for NUSSL experiments

Cookiecutter for NUSSL
====================

A boilerplate for reproducible and transparent computer audition research that leverages
the NUSSL library, which is primarily used for source separation. This project uses
[cookiecutter](https://cookiecutter.readthedocs.io/en/latest/readme.html).
*A logical, reasonably standardized, but flexible project structure for doing and 
sharing data science work.*

Requirements
------------
Install `cookiecutter` command line: `pip install cookiecutter`    

Usage
-----
To start a new science project:

`cookiecutter gh:pseeth/cookiecutter-nussl`

Project Structure
-----------------

```
.
├── cookiecutter_repo               <- contains package code called by scripts
│   ├── __init__.py                 <- imports from submodules and also sets up the logger format.
│   ├── algorithms                  <- separation algorithms used in experiments
│   │   ├── __init__.py             <- default includes FT2D, DeepClustering, etc.
│   ├── dataset                     <- contains Dataset classes for training and testing
│   │   │                              and scripts for generating data.
│   │   ├── __init__.py             <- imports MixSourceFolder and Scaper from nussl
│   │   └── scaper_mixer.py         <- Uses Scaper to make datasets for train and test.
│   ├── model                       <- Set up model code here. Just imports SeparationModel.
│   │   ├── __init__.py                and shows how custom modules could be used.
│   ├── test                        <- contains code used for evaluation (e.g. SI-SDR).
│   │   ├── __init__.py                
│   ├── train                       <- contains code used for training. just imports Trainer
│   │   └── __init__.py                from nussl
│   └── utils                       <- any util code can go here.
│       ├── __init__.py
│       └── parallel.py             <- util for computing a function in parallel across
│                                      multiple threads for each set of arguments in a list.
├── data_prep                       <- contains .yml files that are used to generate and 
│   │                                  prepare data.
│   ├── incoherent.yml              <- creates an incoherently mixed Scaper dataset when
│   │                                  passed to scripts/data.py.
│   └── resample.yml                <- resamples a folder of audio files (can be nested)
│                                      outputs a folder with same structure with resampled audio
├── Dockerfile                      <- Dockerfile used to build the Docker image.
├── experiments                     <- contains .yml files that are used to run experiments.
│   │                                  can also contain .py files that are used to generate
│   │                                  .yml files.
│   └── train.yml                   <- example .yml file for training deep clustering on
│                                      example data.
├── Makefile                        <- Makefile with a set of useful commands. use this
│                                      to run commands on host or container, create the
│                                      development environment, etc. See file for details.
├── notebooks                       <- any notebooks used for analysis go here.
│   └── example.ipynb               <- an example notebook that loads a Scaper dataset
│                                      and visualizes it
├── poetry.lock                     <- generated by Poetry.
├── pyproject.toml                  <- project requirements file. managed via Poetry.
├── requirements.txt                <- frozen requirements file. do not edit directly, 
│                                      only generate via 'make freeze_requirements'.                                                    
├── runners                         <- contains classes that run experiments in containers.
│   ├── config.py                   <- uses environment variables to set up container mounts
│   ├── docker_runner.py            <- sets up a class that runs commands in a container
│   ├── experiment_runner_pool.py   <- runs multiple experiments in a job pool
│   ├── experiment_runner.py        <- sets up and runs a single experiment
│   ├── __init__.py                 
│   └── utils.py
├── scripts
│   ├── data.py                     <- creates a dataset using Scaper, using a .yml file 
│   │                                  with specifications (see above).
│   ├── prepare_urbansound.py
│   ├── resample.py                 <- resamples a folder of audio files. 
│   │                                  takes in a .yml file with specifications (see above)
│   └── run_in_docker.py            <- runs a command in the container
├── setup
│   ├── build_docker_image.sh       <- builds the docker image (use 'make docker').
│   ├── environment                 <- contains scripts for setting up environment variables
│   │   ├── default.sh              <- default. copy to *_local.sh (untracked) and fill in
│   ├── install_docker.sh           <- installs Docker and nvidia-docker on an Ubuntu machine
│   └── melodia                     <- Melodia plug-in files. works only on Linux machines
│       ├── MELODIA - License.txt      but is copied and used in the container. Depends on
│       ├── mtg-melodia.cat            vamp.
│       ├── mtg-melodia.n3
│       ├── mtg-melodia.so
│       └── README_linux64.txt
└── tests                           <- any test cases can go in here 'make test' will run
    │                                  them on the host and then in the container.
    ├── __init__.py
    └── test_yaml.py                <- contains a test case that makes sure all your yaml 
                                       is valid.
```

License
-------
This project is licensed under the terms of the [MIT License](/LICENSE)