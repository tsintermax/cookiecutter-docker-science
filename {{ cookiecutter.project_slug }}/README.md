# {{ cookiecutter.project_name }}

{{ cookiecutter.description }}

## Requirements

* [Docker version 17 or later](https://docs.docker.com/install/#support)

## Setup development environment

We setup the development environment in a Docker container with the following command.

- `make init`

This command gets the resources for training and testing, and then prepares the Docker image for the experiments.
After creating the Docker image, you run the following command.

- `make create-container`

The above command creates a Docker container from the Docker image which we create with `make init`, and then
login to the Docker container. Now we made the development environment. For create and evaluate the model,
you run the following command.

## Development with Docker container

This section shows how we develop with the created Docker container.

### Edit source code

Most of the source codes of this project, `{{ cookiecutter.project_name }}` are stored in the `{{ cookiecutter.project_slug }}` directory.
Generated Docker container mounts the project directory to ``/work`` of the container and therefore
when you can edit the files in the host environment with your favorite editor
such as Vim, Emacs, Atom or PyCharm. The changes in host environment are reflected in the Docker container environment.

### Update dependencies

When we need to add libraries in `Dockerfile` or `requirements.txt`
which are added to working environment in the Docker container, we need to drop the current Docker container and
image, and then create them again with the latest setting. To remove the Docker the container and image, run `make clean-docker`
and then `make init-docker` command to create the Docker container with the latest setting.

### Login Docker container

Only the first time you need to create a Docker container, from the image created in `make init` command.
`make create-container` creates and launch the {{ cookiecutter.project_slug }} container.
After creating the container, you just need run `make start-container`.

### Logout from Docker container

When you logout from shell in Docker container, please run `exit` in the console.

### Run linter

When you check the code quality, please run `make lint`

### Run test

When you run test in `tests` directory, please run `make test`

### Sync data source to local data directory

When you want to download data in remote data sources such as Amazon S3 or NFS, `sync-from-remote` target downloads them.

### Sync local data to remote source

When you modify the data in local environment, `sync-to-remote` target uploads the local files stored in `data` to specified data sources such as S3 or NFS directories.

### Show profile of Docker container

When you see the status of Docker container, please run `make profile` in host machine.

### Use Jupyter Notebook

To launch Jupyter Notebook, please run `make jupyter` in the Docker container. After launch the Jupyter Notebook, you can
access the Jupyter Notebook service in http://localhost:{{ cookiecutter.jupyter_host_port }}.

## Directory Map

├── Makefile
├── README.md
├── config
├── data
│   ├── external								 <- Data from third party sources.
│   ├── interim								   <- Intermediate data that has been transformed.
│   ├── processed							 <- The final, canonical data sets for modeling.
│   └── raw										<- The original, immutable data dump.
├── docker
│   └── Dockerfile
├── model											<- Trained and serialized models, model predictions, or model summaries
├── notebook									  <- Jupyter notebooks. Naming convention is a number (for ordering), │                         the creator's initials, and a short `-` delimited description, e.g.  `1.0-jqp-initial-data-exploration`.
├── references									<- Data dictionaries, manuals, and all other explanatory materials.
├── reports							  		 	<- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures									 <- Generated graphics and figures to be used in reporting
├── requirements.txt						   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
├── scripts											 <- Other scripts
├── tests
│     ├── \__init\__.py
│     └── test_sample.py
└── {{ cookiecutter.project_slug }}
    ├──\__init\__.py										 <- Makes src a Python module
    ├── data_cleansing
    ├── data_gens								<- Scripts to download or generate data	
    ├── feature_engineering
    ├── models
    ├── utils
    └── visualization

#Credits

This package was created with [Cookiecutter](https://github.com/audreyr/cookiecutter) and the [cookiecutter-docker-science](https://docker-science.github.io/) project template.
Modified by @tsintermax for JDSC exclusively.