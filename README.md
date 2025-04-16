# Flow-over-cylinder

# Flow Around a Cylinder (OpenFOAM v10, pisoFoam)

This repository contains an OpenFOAM case simulating the unsteady, incompressible flow around a circular cylinder. The simulation utilizes the `pisoFoam` solver for transient pressure-velocity coupling.

## Case Description

The simulation investigates the flow at a Reynolds number of 100, leading to the formation of a von Kármán vortex street. The computational domain is a rectangular channel with a centrally placed cylinder. No-slip boundary conditions are applied to the cylinder surface, inlet velocity is uniform, outlet has a zero gradient for pressure and velocity, and slip conditions are used for the top and bottom walls. The fluid is assumed to be Newtonian with constant density and viscosity. The k-omega SST turbulence model is employed.

## Mesh Generation

The computational mesh for this simulation was generated using GAMBIT version 2.4.6. The mesh file, `34x18.msh`, is included in the `case/` directory (or potentially in a separate `mesh/` directory). This mesh was converted to OpenFOAM format using the `fluentMeshToFoam` utility.

## Setup Instructions

1.  **Prerequisites:** Ensure you have OpenFOAM v10 and ParaView installed on your system.
2.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/x7z9/Flow-over-cylinder.git](https://github.com/x7z9/Flow-over-cylinder.git)
    cd your-project-name
    ```
3.  **Navigate to the Case Directory:**
    ```bash
    cd case
    ```
4.  **Run the Simulation:**
    ```bash
    fluentMeshToFoam 34x18.msh && checkMesh && topoSet && pisoFoam && decomposePar && mpirun -np 8 pisoFoam -parallel && reconstructPar && postProcess -func vorticity && rm -r processor*
    ```
    This script will execute the mesh generation and the `pisoFoam` solver.
5.  **Post-processing:**
    Open the generated `.foam` file in ParaView:
    ```bash
    paraFoam -builtin
    ```
    You can then visualize velocity vectors, pressure fields, and other relevant quantities.

