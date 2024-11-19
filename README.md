# Parallel Heat Equation Solver

This repository contains a parallel implementation of a 2D [heat equation](https://en.wikipedia.org/wiki/Heat_equation) solver using the [Jacobi method](https://en.wikipedia.org/wiki/Jacobi_method). The solver supports various parallelization strategies involving MPI and OpenMP. It is designed to be flexible, allowing both blocking and non-blocking communication approaches for improved performance across different architectures.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Dependencies](#dependencies)
- [Compilation](#compilation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Performance Considerations](#performance-considerations)

## Introduction
The heat equation solver uses the Jacobi iterative method, a popular numerical algorithm for solving partial differential equations. To accelerate the computation, we have implemented parallelization techniques using MPI (Message Passing Interface) and hybrid MPI+OpenMP approaches. This allows efficient utilization of multi-core and distributed computing environments.

## Features
The implementation supports four parallelization strategies:
1. **MPI with Blocking Communication**: Uses only MPI for domain decomposition with blocking message-passing.
2. **MPI with Non-Blocking Communication**: Uses MPI with non-blocking communication to overlap computation with communication.
3. **Hybrid MPI + OpenMP with Blocking Communication**: Combines MPI for inter-node communication and OpenMP for intra-node parallelism using blocking communication.
4. **Hybrid MPI + OpenMP with Non-Blocking Communication**: Combines MPI and OpenMP, employing non-blocking communication to reduce synchronization overhead.

## Dependencies
- **MPI Library**: e.g., OpenMPI or MPICH
- **OpenMP**: Included with most modern C compilers
- **Make**: For building the project

Ensure you have these installed on your system before compiling the solver.

## Compilation
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
2. Build the project using Make:
   ```bash
   cd src
   make
   ```
   This will generate the executable `heat` for the solver in `/src`.

## Configuration
You can adjust the domain resolution, number of iterations, parallelization strategy, and other parameters by modifying `/src/test.dat`. Details on the configuration options are also provided there.

## Usage
The solver can be executed as follows:
```bash
export OMP_NUM_THREADS=<number_of_threads>
mpiexec -n <number_of_processes> ./heat test.dat <number_of_processes_in_ydirection> <number_of_processes_in_xdirection>
```
An example SLURM script `/src/job.scp` we use on the [SuperMUC-NG](https://doku.lrz.de/supermuc-ng-10745965.html) system at LRZ is also provided for running the solver on a cluster. 

## Documentation
The development process and experimental analysis of this solver are provided in the form of a lab report `/report/Heat_Report.pdf` from a course at the Technical University of Munich.