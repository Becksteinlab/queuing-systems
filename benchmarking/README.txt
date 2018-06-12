From here we can benchmark using an interactive node:

$ interactive -N 1 -n 24 -p physicsgpu1 -q wildfire --gres=gpu:1080GTX:4

Once you are allocated resources, create a directory in scratch space
and copy over your tpr file:

$ WORK="/scratch/${USER}/benchmark/"
$ mkdir -p $WORK
$ cp 2018.tpr $WORK
$ cd $WORK

From here import necessary modules:

$ module load gromacs/2018.1

To run the simulation:

$ ncores=8
$ ngpus=1
$ gmx mdrun -s 2018.tpr -ntmpi $ngpus -nt $ncores -pin on

In the case of gromacs, you would let the simulation run for a about a
minute before killing the process with Control-c since gromacs has
internal optimizations that it will apply at the beginning of the
simulation. Once you do that, you collect the performance and write
that in a file somewhere. Alter the values of $ncores and $ngpus and
collect the performance of your simulation. Do this until you have
identified a sweet spot for performance over resource cost. Request
that configuration for future simulations.
