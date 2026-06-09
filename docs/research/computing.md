# Computing

# Computation at Stanford

Stanford has several places for computation! All students (undergrad and grad)
have access to [Farmshare][1], a small cluster with a queue and with very
limited resources. Additionally, our group has access to [Sherlock][2], the main
computing cluster and a very cool and powerful tool when used responsibly. 

We do not own any nodes at Sherlock, that means that we have to use a queue
system and stay in line until computing resources are free to run our jobs.
Sherlock's line is shared with all the university users, but as part of the
School of Sustainability we have one of the largest partitions in Sherlock that
is only used by researchers within the school. This allows our jobs to stay less
time in the queue as the number of users is just a subset of all of Sherlock's
users. 

## What is a cluster? 

A computer cluster is in rough terms a set of _shared_ computers that are
connected to each other while sharing memory and processing power. Thus, we can
run jobs a (_jobs_ is the name we give to running a script on the cluster)
across nodes or within each of the nodes (nodes are BIG computers). All nodes
are coordinated by a scheduler, in Sherlock case, we use [SLURM][3], a very flexible
scheduler used by most of the big clusters around the world, including the
beautiful [Cheyenne][4], the NCAR super-computer. 


!!! warning annotate "Sherlock is a _*shared*_ resource"
    Every time you use Sherlock, SLURM will penalize you and the whole lab!
    SLURM relies on the FairShare, an algorithm that decides what's the _fair_
    use of computation resources for each user and group. Therefore, everytime
    you run a job be sure of asking the resources you really need (i.e. number
    of hours, cores, and memory).


In general, clusters have three types of nodes: 

 - **Login**: Nodes meant to welcome the user and meant for anything but
   computation. They're named usually: `sh02-lnx`, where `x` is the login node
   identity number. 
 - **Computing**: This nodes will run jobs. Any code _**always**_ runs in these
   nodes. These nodes are named usually: `sh03-09n59`, where `09n59` is
   a specific node in the whole cluster. 
 - **Storage**: Rarely used, but you can access to nodes that are meant just
   for data transmission. This can be either moving a lot of data out or to
   Sherlock. 

In this document we will focus on the [SERC partition][5]. You can check the
partition characteristics by using the `sh_part` command. If you have access to
other partitions or your PI (in case you have a second PI) has nodes, you will
see the information for those nodes there too. 

## Modules 

Having all the software binaries loaded into the `$PATH`[^1] can lead to chaos.
For this reason, Sherlock uses the [Modules system][7]. Loading modules is part
of the life in the cluster and is essential not only for running code, but also to
compile packages (i.e. installing R's `sf` needs you to load several modules.
Same is true for many Python libraries). 

Sherlock has some amazing documentation on Modules, so we won't cover that
here. Just some basics for our lab:  

=== "Python"
    ```bash
    module load python/3.9.0
    ```

=== "R"
    ```bash
    module load R/4.2.0
    ```

=== "Other stuff"
     ```bash
     module spider <other stuff to look for>
     ```

[^1]: This is the environment that contains the path to the executables we want
to run. Go ahead and run `echo $PATH` to see where is the computer looking for
executable binaries.

## Storage 

We have plenty of storage space in Sherlock! For job running, is good to use
fast file systems, like the `$SCRATCH` space. For permanent data storage and
files that will be concurrently used, the `$OAK` and `$GROUP_HOME` are good
alternatives. As all good things in the cluster, remember that `$OAK` is
a shared space within the SDSS, so think of other users before wanting to store those
100 Tb of CMIP data you probably do not need. 


| Storage         | Path                               | Total space         | Time Limit |
|-----------------|------------------------------------|---------------------|------------|
| `$OAK`          | `/oak/stanford/schools/ees/mburke` | 1 Pb [100 Tb/group] | $\infty$   |
| `$GROUP_HOME`   | `/home/groups/mburke`              | 100 Tb              | $\infty$   |
| `$GROUP_SCRATCH`| `/scratch/groups/mburke`           | 100 Tb              | 90 days    |


!!! danger  annotate "`SCRATCH` is deleted every 90 days!"
    Be careful with the scratch space! Be sure to remove all the files you need
    after you run a job. Files in this storage are not backed-up, so there will
    be no way to recover.

### Oak 

Oak is shared with all the SDSS. You can create folders in the root of the
server (the path in the table above) if you need to share files with people
across the school (i.e. ESS, EPS, or rarely, E-IPER). For lab-wide data, we use
the `mburke` directory. We do not have any particular nomenclature for our
filesystem, but try to be use sensible and informative names: 

 - 🚫 `$OAK/mburke/results`
 - ✅ `$OAK/mburke/<project_name>`
 - ✅ `$OAK/mburke/ERA_5_1979_2023`

To avoid permission and possible file corruption avoid cloning repos directly
into `$OAK`, use your `$HOME` for that and store your data in any of the
storages described above

## Running jobs 

There are different ways of running jobs in Sherlock. Compared with other clusters, Sherlock
does not have any computing quotas, rather you can run as many jobs you want until the scheduler 
stop giving giving you jobs. In general, we have two ways of running jobs: 

### In-line

SLURM allow us to request nodes and run jobs directly into them! We have several use cases for this request: 

 - Testing a pipeline: I have built a Python script `hello.py` and want to test
   it before submitting a larger job.
 - Running small tests: I have a GPU job and I want to test my Python
   environment is correctly compiling the right CUDA version. I cannot test
   this is a login node. 
 - Running a Jupyter Notebook: I want to run a quick jupyter notebook without
   having to deal with a job submission.

In-line jobs are very useful, especially for testing and debugging, but remember that is always better to have pipelines that are less interactive and that can run unsupervised. To run in-line jobs, you have to use the `sdev` command: 

!!! example
    `sdev` commands:
        ```sh
        $ sdev -h
        sdev: start an interactive shell on a compute node.
        
        Usage: sdev [OPTIONS]
            Optional arguments:
                -c      number of CPU cores to request (OpenMP/pthreads, default: 1)
                -g      number of GPUs to request (default: none)
                -n      number of tasks to request (MPI ranks, default: 1)
                -N      number of nodes to request (default: 1)
                -m      memory amount to request (default: 4GB)
                -p      partition to run the job in (default: dev)
                -t      time limit (default: 01:00:00)
                -r      allocate resources from the named reservation (default: none)
                -J      job name (default: sdev)
                -q      quality of service to request for the job (default: normal)
        
            Note: the default partition only allows for limited amount of resources.
            If you need more, your job will be rejected unless you specify an
            alternative partition with -p.
        ```


You can request a job with 1 node, 16 cores and 32 Gb of RAM in the SERC partition (just like the
average MacBookPro) for 30 minutes using the following:

```
sdev -n 1 -c 16 -m 16G -p serc -t 00:30:00 --pty bash
```

Once you run this job, you will get assigned a job number and when the
resources are allocated you will have access to that computing node terminal.
Inside the computing node you have access to any folder or file stored in
Sherlock and you can run any binary using the `module` command. 

### Batch job

Compared to the in-line job, we won't have any access to the computing node
terminal. The job will run completely unsupervised and if it fails then the job
will stop executing and will be cancelled and two files will be written: an
output file (usually with an `.out` extension), and an error file with all the
error contents (with an `.err` extension)

=== "Job example"

    ```bash
    #!/usr/bin/bash
    #SBATCH --job-name=test_job
    #SBATCH --output=test_job.out
    #SBATCH --error=test_job.err
    #SBATCH --time=00:30:00
    #SBATCH -p serc
    #SBATCH --nodes 1
    #SBATCH --mem 16GB
    #SBATCH -c 4
    #SBATCH --mail-user=ihigueme@stanford.edu
    #SBATCH --mail-type=ALL
    
    sleep 10
    echo "Hello from the ${HOST}"
    ```

=== "Another example"

    ```bash
    #!/usr/bin/bash
    #SBATCH --job-name=test_job
    #SBATCH --output=test_job.out
    #SBATCH --error=test_job.err
    #SBATCH --time=00:30:00
    #SBATCH -p gpu
    #SBATCH --nodes 1
    #SBATCH --mem 16GB
    #SBATCH --gpu 1
    #SBATCH -c 4
    #SBATCH --mail-user=ihigueme@stanford.edu
    #SBATCH --mail-type=ALL
    
    sleep 10
    echo "Hello from the ${HOST} with a GPU"
    ```
=== "Submit your job"
     ```bash
     $ sbatch test_job.sbatch
     Submitted batch job 22312518 # This is your job id
     ```

As you can see, there is some overlap between the options we used in `sdev` and
the ones we use in our batch job file. Any SLURM command should be prepended by
the `#SBATCH` flag, this is telling the computer that is a command for the
scheduler and not a local variable. Let's go over some of the commands use
above: 

`--job-name`
:   Name for the job. Is useful for traceability when calling `squeue` or just
    to check the history of commands ran in the past.

`--output` and `--error`
:   Name for output and error files. Usually saved in the same directory where
    the batch file is located. You can specify another path. If left empty, the
    default will be `<job-name><job-id>.err`

`--time`
:   Time we are asking the scheduler to keep the job alive. Once the time is
    done, the job will be stopped. Plan accordignly and test before running a long
    job. Sherlock has limits, so jobs shouldn't last more than 7 days.

`-p`
:   Paritition. The default is using the main queue, but there are many
    available (list them using the `sh_part` command). Use `dev` if you want to
    test, and `serc` when you're ready to send jobs.

`--nodes`
:  Number of nodes to request. Usually this is set to 1 because it fits most of
   the vanilla parallelization schemes in Python and R. Use more than 1 node
   if, and only if, you're using OpenMPI powered code (i.e. C++ processes and
   sometimes Python's Dask). If using more than one node, many new options are
   open: `--ntasks-per-node`, and `--cpus-per-task`. Read more on the SLURM
   documentation.  

`--mem` and `--cpu`
:  These two options set how much memory and cores you need. Remember that as
   a thumb of rule, these two go together. The more cores you use in
   parallelization, the more memory you will need since cores are sharing data
   over RAM. `serc` nodes have between 24 and 128 cores, and between  191G and
   1024G of RAM memory. Your job should not exceed any of these limits, and
   usually not be even close to that maximum. Adding more memory and more cores is
   often not a good solution to slow code (check out the piece about the Amdahl's Rule [here][9]). 

`--mail-user` and `--mail-type`
:  This is nice-to-have in your job, especially if you're in a long queue. This
   command will send an email to the email under `mail-user` once the job started
   to run, finished to run, or just failed. Usually has nice data on usage that
   you can use to set your next job. 

## Some tricks and common issues in Sherlock

### Tricks

#### Do `ssh` like a pro

Tired of doing `ssh <user>@sherlock.stanford.edu` and being thrown into whatever login node they want? Want to set up an SSH-tunnel from the get-go with a pre-determined port (v.gr. this is very useful for running Jupyter notebooks in Sherlock nodes)? The [SSH config][10] is what you need. The Sherlock documentation has [some details][11] on this.  

#### `tmux` is your best friend

Back in the day, life in the terminal was the common place. Unix has developed
very good window managers that allow you to have horizontal and vertical
splits, and several windows within a unique `ssh` connection. More importantly,
these managers also allow you to run a process and let it run even if you
disconnect from Sherlock. There are two main programs that serve this
functions: `screen` and `tmux`. The later is better maintained, and is also my
favorite ❤️

Tmux has a good [starter guide][12], and is extremely configurable using its
dotfile: `~/.tmux.conf`. I know, what the heck are dotfiles? Check out more
about them [here][13]. 

#### Building bash scripts

An essential tool of the terminal is to learn how to run basic bash files. These files are very flexible and allow to build command-line interfaces: 

=== "A simple bash file: `hello.sh`"
    ```bash
    #!/bin/bash
    echo "Hello world!"
    ```
=== "A bash file with commands"
    ```bash
    #!/bin/bash
    # Print whatever argument we put on the command
    $ARG=$1
    echo "{$ARG}"
    ```

Bash is incredibly flexible and powerful. These scripts are particularly useful
when creating batch jobs or just simplifying how we run code. More details on how
to write and run these are [here][8].

### FAQs

#### My Windows machine is not compatible with X, Y or Z

Truly unfortunate. You have a 2K one-time grant as a SDSS student. Change
computers, many good Linux Machines are also available with better specs than
a MacBook Pro at a similar price range. If you want to stay with Windows, update
to the Windows 10/11 edition and install the Ubuntu terminal. 

#### I don't have access to `$OAK`, what should I do?

:   Checkout the SERC OAK [documentation][6]

#### My job is stuck in `(Priority)`
:   Life is hard. Just wait

##### I need some help with my code 
:   Getting help for Sherlock is quite easy. You can either ask for help to
people in the lab, or you can also use the `#sherlock-users` channel on Slack
where Kilian Cavalotti or any of the cluster's users are happy to help you with
any problem. You can also check many of the great [resources][17] put together by
the SDSS-CFS

## A few remarks on environment reproducibility

### Python

Sherlock modules do not include any distribution of Anaconda. If you want to
install Conda[^2] or [Mamba][14], you should install it on your `$HOME`
directory. Nonetheless, these Python distributions are very bloated and do not
play well with Sherlock. An alternative to this is to load the `python/3.9.0`
module, and then use `vritualenv`. 

=== "Load modules and install virtualenv"
    ```bash
    module load python/3.9.0
    # pip will install libraries locally in the $HOME
    pip install virtualenv 
    ```
=== "Create environment"
    ```bash
    virtualenv -p python $SCRATCH/test_env
    ```
=== "Activate environment"
    ```bash
    source $SCRATCH/test_env/bin/activate

    # Test that I am using my environment python
    # This should print the path to the environment
    which python

    # Once you check is the right path, you can install some libraries
    pip install -r requirements.txt
    ```

Notice that I am creating my environment in the `$SCRATCH` space, this is due
to space limitations in the `$HOME`. Sherlock only allows 15 Gb in your home
directory, thus you should avoid to put environment or big files on it. Once
you have reached your quota, Sherlock will stop writing files and this can lead
to data corruption. 

You do not need to use `$SCRATCH`, you can use either `$GROUP_HOME` or `$GROUP_SCRATCH`.
Be aware you cannot share environments with people across the group, this
because of permissions. A solution to this is always keeping
a `requirements.txt` updated so people can reproduce your Python environment.
A more advanced alternative is to use [Singularity][16], a containerization 
module created specifically for HPC systems and developed by Stanford. 


#### A note on Conda/Mamba on Sherlock
By default, `conda` will install environments in your `$HOME` directory. Conda
does not only install Python libraries, but also many binaries that it needs 
to compile package installation, this includes its own version of `gcc` and 
its own `C++` libraries. Be aware that many of these are not optimized to 
Sherlock's hardware, and you should avoid these if you are looking for max
performance (i.e. Sherlock has it's own compilation of PyTorch just to play
nice with its GPUs). 

A solution to Conda's storage problem is to change your `~/.condarc` file and
use the following (remember to change your user name in the file below)

=== "`~/.condarc`"
    ```yaml
    always_yes: true
    envs_dirs:
      - /scratch/users/{your user name}/conda_envs
    
    channels:
      - conda-forge
      - defaults
    channel_priority: strict
    ```

More details in how to manage `virtualenv` environments is [here][15].

[^2]: I do recommend to use Mamba over Conda, is not only faster, but also way
more reliable and based on the `conda-forge` channel.


## Some reading material

 * [Ten Simple Rules for Success with HPC - Imperial College](https://arxiv.org/abs/2101.06737)

[1]: https://web.stanford.edu/group/farmshare/cgi-bin/wiki/index.php/Main_Page
[2]: https://www.sherlock.stanford.edu/
[3]: https://slurm.schedmd.com/overview.html
[4]: https://arc.ucar.edu/knowledge_base/70549542
[5]: https://stanford-rc.github.io/docs-earth/
[6]: https://stanford-rc.github.io/docs-earth/docs/getting-started-oak
[7]: https://www.sherlock.stanford.edu/docs/software/modules/
[8]: https://swcarpentry.github.io/shell-novice/06-script.html
[9]: https://hpc.llnl.gov/documentation/tutorials/introduction-parallel-computing-tutorial 
[10]: https://linuxize.com/post/using-the-ssh-config-file/
[11]: https://www.sherlock.stanford.edu/docs/advanced-topics/connection/#ssh-options
[12]: https://github.com/tmux/tmux/wiki/Getting-Started
[13]: https://driesvints.com/blog/getting-started-with-dotfiles/
[14]: https://mamba.readthedocs.io/en/latest/
[15]: https://pythonbasics.org/virtualenv/
[16]: https://www.sherlock.stanford.edu/docs/software/using/singularity/
[17]: https://stanford-rc.github.io/docs-earth/docs/resources_overview#pancakes-resources
