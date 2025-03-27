# Getting Started: Log Into NCAR HPC Systems

[Helpful Link - Logging In](https://ncar-hpc-docs.readthedocs.io/en/latest/getting-started/#about-this-page)

Open a terminal and type in the command:
<ul>
    <li>**ssh -X slarsen@derecho.hpc.ucar.edu** for derecho</li>
    <li>**ssh -X slarsen@casper.hpc.ucar.edu** for casper</li>
</ul>

Make sure you have your password ready

There will be Duo two-factor authentication, so make sure you have your phone on you as well

[Helpful Link - Activating Conda Environments](https://ncar-hpc-docs.readthedocs.io/en/latest/environment-and-software/user-environment/conda/)

TO ACTIVATE CONDA: **module load conda**

Other Conda commands:
<ul>
    <li>**conda env list**</li>
    <li>You can use either conda or mamba for activating/deactivating your environment </li>
    <li>**conda activate my-env** or **mamba activate my-env**</li>
    <li>**conda deactivate** or **mamba deactivate** (just be consistent)</li>
</ul>

Making your own environment (example):

**mamba create -n my-env python=3.10 numpy scipy matplotlib pandas**

**geocat-comp wrf-python**



# Submitting Simple Jobs to Derecho or Casper

[Helpful Link - Submitting Jobs](https://ncar-hpc-docs.readthedocs.io/en/latest/pbs/#job-scripts)
[Helpful Link - Job Scripts](https://ncar-hpc-docs.readthedocs.io/en/latest/pbs/job-scripts/)

Type **vi** to make a new file with the following format (example below):

~~~~~~~

#!/glade/u/apps/opt/conda/envs/npl/bin/python
#PBS -N hello_pbs                         # Job Name
#PBS -A <project_code>                    # Project Code
#PBS -j oe                                # Combine any standard text output (o) and error (e) into one output file
#PBS -k eod                               # not sure what this is tbh
#PBS -q main                              # Specifies the desired PBS queue for this job
#PBS -l walltime=00:05:00                 # Maximum amount of time to be spent on the project HH:MM:SS, Minimum is 5min
#PBS -l select=1:ncpus=1:mpiprocs=1       # Number of nodes and cpus requested (try to keep it light)

import sys
print("Hello, world!!\n\n")

print("Python version:")
print(sys.version)
print("Version info:")
print(sys.version_info)

~~~~~~~

Your projcect code is ***UCOR0090***

You can change the #!/glade/u/apps/opt/conda/envs/npl/bin/python to npl -> my-env to specify your environment

To Submit your job: **qsub your_script_name**

To monitor your ongoing jobs: **qstat -u slarsen**

To retrieve list of finished jobs: **qhist -u slarsen**

To Kill an ongoing job: **qdel jobID**

# Using NCAR HPC Jupyter Hub

Login to the [Jupyter Hub](https://jupyterhub.hpc.ucar.edu/)

If you're logging in on Firefox your credentials should fill in for you. You'll need Duo authentication, so make sure you have your phone on you.

Start the server (press the 'start' button) to activate tools

# Uploading and Downloading Files

To upload a file, you can't be in the supercomputer: you need to open a new terminal and be in your own mac computer's base environment. Once you do that, run the following command:

To upload files: **scp your_local_file_pathname slarsen@casper.hpc.ucar.edu:/path/to/hpc/folder/**

(replace casper with derecho if working with derecho)

Upload command example: **scp /Users/skylarlarsen/Desktop/Cornell/Year_Two/EAS_DeepLearning/CASPER_Doc/HOWTO.md slarsen@casper.hpc.ucar.edu:/glade/u/home/slarsen/**

To download files: **scp slarsen@derecho.hpc.ucar.edu:/path/to/hpc/folder/ local_file_pathname**

Download command example: **scp slarsen@casper.hpc.ucar.edu:/glade/u/home/slarsen/hello_world /Users/skylarlarsen/Desktop/Cornell/Year_Two/EAS_DeepLearning/CASPER_Doc/**

REMEMBER, these commands must be typed into your HOME COMPUTER, NOT THE SUPERCOMPUTER.

You can also transfer files between clusters (casper to derecho and vice versa)

# Monitoring Resource Usage

Check current jobs: **qstat -u your_username**

View core hours: **ncar_accounting_report**


# Clone Your Repository

In the supercomputer terminal: **git clone https://github.com/your_username/your_repo.git**

Example: **git clone https://github.com/SkylarLarsen/EAS_6995.git**
