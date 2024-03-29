# VSRBiodiversity
This is the official repository for the GECCO (Genetic and Evolutionary Computation Conference, 2021) paper "Biodiversity in Evolved Voxel-based Soft Robots", **best paper award at complex systems track**, hosting all the code necessary to replicate the experiments. This work is partially based on Marco Rochelli's master's thesis (https://github.com/MarcoRochelli/Co-evolution) and was carried out at the Evolutionary Robotics and Artificial Life Laboratory (ERALLab) at the Department of Engineering and Architecture, University of Trieste (Italy).

## Scope
By running
```
java -cp libs:JGEA.jar:libs/TwoDimHighlyModularSoftRobots.jar:target/VSRBiodiversity.jar Main {args}
```
where `{args}` is a placeholder for the arguments you must provide (see below), you will launch an evolutionary optimization for evolving jointly the body (number and arrangement of the voxels) and brain (the controller, an Artificial Neural Network (ANN)) of Voxel-based Soft Robots (VSRs). At the same time, a number of evolution metadata and interesting features will be saved inside the `output` folder. Features include descriptors of VSRs that we devised as a way of characterizing their shape and behaviour. We employed them (in a supervised learning pipeline) to assign each robot to a species, measure biodiversity in VSRs and study how it mutates as the evolutionary algorithm and the controller representation vary. The project has been tested with Java `14.0.2`.

## Structure
* `src` contains all the source code for the project;
* `libs` contains the .jar files for the dependencies (see below);
* `Data_Analysis_Notebook.ipynb` is a Jupyter Notebook (Python) with some routines and starter code to perform analysis on the evolution output files.

## Dependencies
It relies on:
* [JGEA](https://github.com/ericmedvet/jgea), for the evolutionary optimization;
* [2D-VSR-Sim](https://github.com/ericmedvet/2dhmsr), for the simulation of VSRs.

The relative jars have already been included in the directory `libs`. See `pom.xml` for more details on dependencies.

## Usage
This is a table of possible command-line arguments:
Argument       | Type                                         | Optional (yes/no) | Default
---------------|----------------------------------------------|-------------------|-------------------------
evolver        | {cmaes, ga, se-geno, se-shape, se-behaviour} | no                | -
representation | {homogeneous, heterogeneous}                 | no                | -
seed           | integer                                      | no                | -
threads        | integer                                      | yes               | # available cores on CPU

where {...} denotes a finite and discrete set of possible choices for the corresponding argument. The description for each argument is as follows:
* evolver: the evolutionary algorithm to perform optimization with.
* representation: the representation for the robotic controller. For this work, we use a distributed model (one ANN for each voxel), of which we devised two alternatives, _homogeneous_ and _heterogeneous_. In the former, all the ANNs share the same weights; in the latter, different voxels have different weights.
* seed: the random seed for the experiment.
* threads: the number of threads to perform evolution with. Defaults to the number of available cores on the current CPU. Parallelization is taken care by JGEA and implements a distributed fitness assessment.

## Bibliography
Medvet, Pigozzi, Bartoli, Rochelli. "Biodiversity in Evolved Voxel-based Soft Robots", ACM Genetic and Evolutionary Computation Conference (GECCO), 2021
```
@inproceedings{medvet2021biodiversity,
    author = {Medvet, Eric and Bartoli, Alberto and Pigozzi, Federico and Rochelli, Marco},
    title = {Biodiversity in Evolved Voxel-Based Soft Robots}, 
    year = {2021}, isbn = {9781450383509},
    booktitle = {Proceedings of the Genetic and Evolutionary Computation Conference},
    pages = {129–137},
    series = {GECCO '21}
}
```
