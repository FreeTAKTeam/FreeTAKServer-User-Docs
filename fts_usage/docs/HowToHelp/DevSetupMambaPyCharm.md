# Setup a development environment for FTS
## introduction
this tutorial assumes that you are working under windows (tested under 11)

# Tools Installation

## Get the IDE: PyCharm
As an integrated Development Environment (IDE) some people use PyCharm.

[Download PyCharm from here](https://www.jetbrains.com/pycharm/)

## Clone the Project Repositories

Clone from the [FreeTAKTeam/repositories](https://github.com/orgs/FreeTAKTeam/repositories) group
`FreeTakServer` and `DigitalPy` repositories locally.
This can be done from within `PyCharm`. 

It can also be done from the command line.

```shell
git clone https://github.com/FreeTAKTeam/FreeTakServer.git fts
git clone https://github.com/FreeTAKTeam/DigitalPy dipy
```

Some other optional repositories:
```shell
git clone https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs fts-docs
git clone https://github.com/FreeTAKTeam/UI.git fts-ui
```

# Create a virtual Environment

Here we [use a `conda` variant, `micromamba`](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html).

Detailed installation instructions can be found [here](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html).

With `micromamba` installed we can set up a virtual environment:

```shell
mamba env create -y -f fts_user/docs/HowToHelp/fts-dev-env.yml
```

This environment definition is not seminal.
The dependencies used here are copied from the following sources:

FreeTakServer

* [FreeTakServer/pyproject.toml](https://github.com/FreeTAKTeam/FreeTakServer/pyproject.toml)
* [FreeTakServer/setup.py](https://github.com/FreeTAKTeam/FreeTakServer/setup.py)
* [FreeTAKServer/.../mission/test-requirements.txt](https://github.com/FreeTAKTeam/FreeTakServer/FreeTAKServer/components/extended/mission/test-requirements.txt)
* [FreeTAKServer/.../mission/requirements.txt](https://github.com/FreeTAKTeam/FreeTakServer/FreeTAKServer/components/extended/mission/requirements.txt)
* [FreeTakServer/requirements.txt](https://github.com/FreeTAKTeam/FreeTakServer/requirements.txt)

DigitalPy

* [DigitalPy/pyproject.toml](https://github.com/FreeTAKTeam/DigitalPy/pyproject.toml)

```yaml
{!HowToHelp/fts-dev-env.yml!}
```

Activate the virtual environment
```
mamba activate fts-dev
```
# Install FTS Locally

Install dependencies and DigitalPy as package
```
pushd dipy
pip install -e .
popd
```

# Configure PyCharm

### FTS YAML File
In the  folder containing the FreeTakServer working repository create a file. 
  
Populate that file, `FTSConfig.yaml`, with the following:
```yaml
{!HowToHelp/FTSConfig.yaml!}
```

1. Adjust paths to point to point to dir structure
2. Create a certs folder at the same level
3. Adjust FTS_CERTS_PATH to point to the newly created dir
4. Create new directory for the FreeTakServerLogs
5. Adjust FTS_LOGFILE_PATH to point to the newly created dir

# you're Ready to Help!


