# DL_MESO installation instructions

Dependencies:
 - MPI
 - GNU compiler

## Obtain a license

`DL_MESO` requires a license from STFC. This can be requested here: https://www.scd.stfc.ac.uk/Pages/DL_MESO-register.aspx

Once the registration process is complete, STFC will send an email with a download link and a password to unzip the files.

## Download and unzip the files

Download the file to your user-space in ARCHER2.

```bash
cd ${HOME/home/work}
# use wget do download the zip file
wget <link to download>
# or sftp/scp/rsync file to this folder
# unzip files -- you'll be asked for the password provided in the email
unzip dl_meso_2.7.zip
```

## Compile files

The following uses GNU compilers and MPICH:

```bash
# go to the WORK folder inside `dl_meso`
cd ${HOME/home/work}/dl_meso/WORK
# load the GNU compilers
module load PrgEnv-gnu
# Compile LBE
CC -o lbe.exe ../LBE/plbe.cpp

# compile DPD
cp ../DPD/makefiles/Makefile-MPI ./Makefile
make FC=ftn FFLAGS="-O3 -fallow-argument-mismatch" all

# compile extra utilities
make CC=CC FC=ftn FFLAGS="-O3 -fallow-argument-mismatch" -f Makefile-utils
```

executables are now in `${HOME/home/work}/dl_meso/WORK` and can be accessed in the usual way (or added to `$PATH`)
