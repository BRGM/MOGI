# Geological Interpretor Proof of Concept

## Overview
This repository contains an algorithm designed for **automatic interpretation** based on a novel interpretation formalism. 
The algorithm is developed in Python and is conveniently encapsulated in a single [**notebook script**](notebooks/00_demo_mogi.ipynb).

The algorithm utilizes a unique interpretation formalism and incorporates 
a knowledge model encapsulated in the [mogi.owl](ontologies/mogi.owl) file (**Minimal Ontology for Geological Interpretation**). 
This ontology serves as a foundation for **geological interpretation**,
providing a structured and comprehensive framework for the algorithm's decision-making process.
This repository is associated with a publication submitted to CaGeo journal under the title **knowledge driven modeling formalism to automatically interpret and construct geological models**. 
The publication details the theory and the formalism behind the algorithm presented in this repository. 
In the publication we use a simplified scenario to show how generally modelers construct geological surfaces using interpolation [**interpolation_based_scenario**](human_based_scenario/interpolation_based_scenario.ipynb).

## Getting Started

Follow these steps to start using the algorithm:

### Clone the Repository:
Clone this repository from GitHub or download the ZIP master of the repository on your machine:
    git clone https://github.com/BRGM/MOGI.git

### Create Environment:
This project uses special Python packages, including [owlready2](https://owlready2.readthedocs.io).

For the code to work properly, your python environment needs the packages listed in the environment file in [installation/mogi.yml](installation/mogi.yml).

We recommend creating a new environment to avoid conflicts. The following command should create an appropriate environment and call it **mogi** 
Navigate to the repository directory and create a virtual environment by using the [mogi.yml](installation/mogi.yml) file:
    conda env create -f installation/mogi.yml

Alternatively, make sure all the necessary packages are installed by checking the [mogi.yml](installation/mogi.yml) file.

### Activate Environment:
Each time you want to use this code you need to activate the **mogi** environement (including just after creating it the first time).
    conda activate mogi

### Launch Demo Notebook:

Open the provided [demo jupyter notebook](notebooks/00_demo_mogi.ipynb) to start working with the algorithm.
    jupyter notebook demo.ipynb

To avoid packaging complexity for this first proof of concept, all the working code is included in the notebook.
It means you'll need to run all the cells of the notebook from the start up to the demonstration section to initiate the notebook.
If you are not familiar with Jupyter notebooks, know that there is a *Run All* option that should be available in the commands depending on your jupyter notebook tool.
Cells of the notebook can be run individually with *Ctrl+Enter*. 

## Contents

The repository includes the following files:
* README.md: the current  instruction file.
* notebooks/demo.ipynb: A demonstration notebook to help users get started quickly.
* ontologies/mogi.owl: Minimal Ontology for Geological Interpretation, serving as the knowledge model.
* installation/mogi.yml: YML file specifying the required dependencies.
* licence/Licence_CeCILL-B_V1.txt: The license file governing the usage and distribution of the algorithm.
* licence/copyright.txt: The file containing copyrights of the developpers and institutions.
* human_based_scenario/interpolation_based_scenario.ipynb: A notebook containing a script for building a geological surface using interpolation and expert interpretations.
* inputs/sparse_data: a csv file containing intial inputs used in the demonstration of the proposed algorithm and in the human_based_scenario application.
* inputs/sparse_data1 and  inputs/sparse_data2: two csv files containing additional inputs used in the human_based_scenario application to constrain interpolation.

## License

This algorithm is released under the [cecil-b](licence/Licence_CeCILL-B_V1.txt) license. See the LICENSE file for more details.

## Contributing

If you would like to contribute to the development of this algorithm, please follow our [contribution guidelines](contribution_guidelines.md).

## Issues

If you encounter any issues or have suggestions, please open an issue in the repository.

## Development advices

Please refer to the [contribution guidelines](contribution_guidelines.md).

### Notebook management
If you intend to commit changes to the notebooks versionned in this project,
please edit your environnement in the following way beforehand to avoid versionning
local information and execution count.

1. Install **jq** if needed (from https://stedolan.github.io/jq/) making it accessible into your *path*
2. Edit the *config* file in the *.git* folder in the repository directory
3. Add the following piece of code:

        [filter "nbstrip_full"]
        clean = "jq --indent 1 \
            '(.cells[] | select(has(\"outputs\")) | .outputs) = []  \
            | (.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
            | .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
            | .cells[].metadata = {} \
            '"
        smudge = cat
        required = true

4. Create a *.gitattributes* file in the main folder of the repository (if not already there) and add in

        *.ipynb filter=nbstrip_full

