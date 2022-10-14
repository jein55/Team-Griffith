# Team-Griffith

This contains all the code for the quantum espresso challenge. Due to the amount of coding that was undertaken not all of the code and outputs used were able to be downloaded and collected. However we tried our best to make sure to download as many as possible.

The general format of code followed:

```

#!/bin/bash

#PBS -P xr60 

#PBS -l walltime=00:10:00 

#PBS -l ncpus=48 

#PBS -l mem=190gb 

#PBS -l software=qe 

#PBS -l wd 
 

module load openmpi/4.1.2 
  
module load qe/7.0 

  
export OMP_NUM_THREADS=1 
mpirun pw.x -npool 12 -ndiag 1 -inp CeO2.in > CeO2.out
#this is the code for the MPI run with 1 thread, 12 pools and -ndiag set to 1

export OMP_NUM_THREADS=2 
mpirun -map-by ppr:6:numa:PE=2 -x OMP_NUM_THREADS=2 -display-map pw.x -npool 16 -ndiag 16 -inp CeO2.in > CeO2.out 
#this is the code for the OpenMPI run with 2 threads, 16 pools and -ndiag set to 16 

export OMP_NUM_THREADS=4
mpirun -map-by ppr:3:numa:PE=4 -x OMP_NUM_THREADS=4 -display-map pw.x -npool 32 -ndiag 16 -inp CeO2.in > CeO2.out 
#this is the code for the OpenMPI run with 4 threads, 32 pools and -ndiag set to 16 
  
export OMP_NUM_THREADS=6 
mpirun -map-by ppr:2:numa:PE=6 -x OMP_NUM_THREADS=6 -display-map pw.x -npool 8 -ndiag 16 -inp CeO2.in > CeO2.out 
#this is the code for the OpenMPI run with 6 threads, 8 pools and -ndiag set to 16
  


```

