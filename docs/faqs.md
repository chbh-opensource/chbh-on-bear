# Frequently Asked Questions

Is something incorrect, out-of-date or missing from this page? Open an issue on github and let us know.

## Where can I ask for help?

You can ask for informal help via the CHBH Code, Computing and Open Science teams page. More formal support is availabl by raising a support ticket with IT.

---

## General

### ‘CPU’ terminologically distinct from ‘core’?

For our purposes we can think of them as the same.

### What does 4 cores actually mean?

4 different things can happen at once. And say 50 cores means 50 jobs in parallel.

### Is castles the same as rds space?

[CaStLeS](https://intranet.birmingham.ac.uk/it/teams/infrastructure/research/bear/castles/castles.aspx) (Compute and Storage for Life Sciences) resources (both compute and storage) are a constituent part of BEAR Cloud, BlueBEAR and the wider BEAR infrastructure. They are reserved exclusively for the use of research groups carrying out research in the life sciences.

In CHBH, 'Castles' has often referred to Virtual Machine environments used for analyses. These are been phased out in favour of the BEAR GUI.

### What about code sharing? Not everybody has a Bluebear. Will people be able to run my code if I’ve written it for use on this platform?

Couple of points
- Think in terms of ‘develop’ vs ‘rationalise’. The second part is where parallelising becomes a bi advantage. It’s also the place you think about code sharing.
- There are clever ways to make things very shareable agnostic to infrastructure. E.g., putting everything into a docker container and running ‘container jobs’. This has the disadvantage that you lose bear’s optimisation (all modules have been optimised so may run a lot faster). But you gain control. Tradeoff

---

## BEAR Portal

### What is included in the 'Number of hours' when starting a service on BEAR portal?

The ‘number of hours’ means that the GUI is required for N hours, not that the whole analysis needs to last N hours.  The 8 hour limit is for interactive jobs or apps started from the BEAR portal. The time limit on the main cluster is 10 days.

### What does ‘working directory’ mean when starting VS Code?

This changes root dir that VScode opens in, though it can only operate within your RDS home space, not a group space. If you want to edit files in a group space using VS Code, you'll need to create a 'Symbolic Link' that provides a path to the group from within your home space. For example, to link a project to a home space you can run

```shell
ln -s /rds/groups/q/quinna-example-project /rds/homes/q/quinna/
```

There will now be a link directory in `/rds/homes/q/quinna/quinna-example-project` that you can use to see the files in the group space. Note that this is a 'link' not a copy.

### Do I NEED to run a VScode interactive session - couldn’t I use my own local code editor?

If you’ve mounted your RDS drive, you could also use a local text editor, any one that you like. But, if you’re running things locally on BEAR, an advantage is that you don’t need to copy files back and forth which adds a step and can be cumbersome.

### Does VScode track changes to code?

VScode doesn’t track changes itself but VScode should be able to show you which files have been modified if you are reading files within an existing git repository. Git should be used to handle version tracking.

### What situations would it make sense to use parfor in matlab?

The most common neuroimaging use-case for `parfor` is looping over participants for first-level analyses. For example, when you want to run an identical set of steps on every file in a datasets.

Other examples might include computing something from every voxel/channel/frequency in a single dataset, or running non-parametric permutatation stats.

---

## Matlab

### What if you asked for 50 CPUs and DIDN’T use a parfor? Would it still be faster?

Not necessarily. It depends on how the person wrote the code, occasionally a toolbox might know how to parallelise a process internally but this is unlikely by default. It is possible to ask for 50 cores and then accidentally run an analysis on only one of them.w

### Can I write a startup.m script to do things like adding paths to tools I use all the time, so MATLAB will automatically execute this when it starts up?

Yes. A matlab `startup.m` script in your local home directory will run as normal when opening matlab.

### For people who are already using matlab/rdesktop on their own computer, what are the key steps to get the best optimisation as you’ve described when they switch to the cluster?

Don’t optimise too early. Look at your data first - lots of visualisation etc which is more interactive. But when you’ve got your pipeline hardened, that’s when you want to do all this stuff. Or when you’ve got a pipeline but want to change something and re-run.
