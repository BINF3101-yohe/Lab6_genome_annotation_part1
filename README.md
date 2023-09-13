# Lab4_Genome_Annotation

## Outline

[Introduction](#introduction)

[Step 1](#step-1-set-up-your-lab-4-folder)

[Step 2](#step-2-mask-our-genome)

[Lab Question 1](#lq-1)

[Lab Question 2](#lq-2)

[Step 3](#step-3---setup-for-braker)

[Step 4](#step-4---setup-braker-and-run)

[Lab Quesiton 3](#lq-3)

[Step 5](#step-5---preparing-for-the-next-lab)

[Lab Quesiton 4](#lq-4)

[Lab Quesiton 5](#lq-5)

[Lab Quesiton 6](#lq-6)


## Introduction

In the lab today we will be annotating our genomes. Annotation is the process of finding the genes. The software we will run, called BRAKER, attempts to identify the beginning and end of genes. It will also identify exons and introns within the gene. 

![image](https://github.com/BINF-3101/Lab4_Genome_Annotation/assets/47755288/77b896a0-47e3-470a-a507-b74b94a66093)

Genes within genomes can be distributed in very different ways. Some genomes have lots of genes that are closely packed. The human genome, conversely, has long stretches of DNA that do not contain genes. 

Yeast genomes are typically compact and the genes contain few introns. We need to **train our model** to know what type of genome we have. We will use a database of known yeast proteins to train our mdeol



## Step 1: Set up your Lab 4 Folder

From your home directory (/users/username) create a new folder called lab_4

```bash
mkdir lab_4
```

Now we want to copy our final file from lab_3 into the lab_4 folder 

```bash
cp lab_3/SRR**123**-contigs.v2.fa lab_4/.
```

As a reminder the ```.``` command means "here". So ```lab_4/.``` means "here in the lab 4 folder. 



## Step 2: Mask our genome

Our genome likely contains highly repetitive regions. We want to hide or mask those regions. This helps the genome annotation software ignore these repeated regions

### Step 2a: Load repeatmasker

We will be using a software called repeatmasker which is already installed on the cluster. 

```bash
module load repeatmasker
```

### Step 2b: Run repeatmasker

We want to tell repeatmasker what type of species we are using so that it can look for the right type of repeats

```bash
RepeatMasker -species saccharomycotina SRR**NUM**-contigs.v2.fa
```

This will run for a while. Answer the question below while it is running

# LQ 1

**Repeatmasker looks for insertion elements from a common laboratory bacteria. What is this bacteria?**

Our new masked genome from this pipeline will be **SRR1234-contigs.v2.masked**

The results from our masking will be in the file **SRR1234-contigs.v2.fa.out**

Take a look at your output file (SRR1234-contigs.v2.fa.out) using head, cat or less command

# LQ 2

**How many "simple repeats" were identified in your genome?**


## Step 3 - Setup for BRAKER

Now we are going to get set up to run BRAKER. There are several **key steps** you need to complete before running the slurm script. **You will have to do these each time you want to run BRAKER**

### Step 3b - Clear your console and load modules

We want to unload everything we loaded before and load several packages before starting. 

To clear your terminal you can close it and open a new one or use the module purge command

```bash
#clear all loaded modules
module purge

#load braker and other dependencies
module load bamtools/2.5.1 blast/2.11.0+ augustus/3.4.0 diamond braker/2.1.5
```

### Step 3b - Setup GeneMark

BRAKER calls a program called genemark. We need to tell genemark where to look for it's configuration files

```bash
#go to your home directory
cd
#enter this command exactly
cp $GM_HOME/gm_key $HOME/.gm_key
```

### Step 3c - Setup Augustus

BRAKER calls another program called AUGUSTUS that requires an input database. We need to create this database

```bash
#go to your home directory
cd

#enter this command exactly
cp -ar $AUGUSTUS/config $HOME/augustus_config
```


## Step 4 - Setup BRAKER and run 

**THIS STEP WILL TAKE A LONG TIME** Braker is _not_ a quick program. This process will take **AT LEAST 10 HOURS!**. The larger your genome the longer it will take.

### Step 4a - Copy slurm script

Top copy the slurm script into your lab_4 directory. 

```bash
cp /projects/class/binf3101_001/braker.slurm .
```


### Step 4b - Edit the slurm script

There is one section of the script you need to edit

![image](https://github.com/BINF-3101/Lab4_Genome_Annotation/assets/47755288/3479ccde-e16c-47f9-8423-8a47e9f80c44)


In the line where it says SRR="1234556" you should change it to your SRR number. 


### Step 4c - Submit the slurm script

Before submitting your braker script make sure you have the following files in your directory 

- SRR12345-contigs.v2.fa.masked
- braker.slurm

If those two items are in your directory you can submit the script

```bash
sbatch braker.slurm
```

### Step 4d -  Check on your annotation

This will take a long time to run, so let's look at what's happening


**Check to see if the program is running**

```bash
squeue -u username
```

![image](https://github.com/BINF-3101/Lab4_Genome_Annotation/assets/47755288/ea7927d8-c920-4d5e-ab6f-757932cae2f8)

You should see your job running with the amount of time it's been running. 


**Look at the log file**

The braker program will create a new folder called **braker**

**_NOTE!_** If you need to **re-run braker** you will need to delete this folder. Ask our TA our myself if you run into this issue. 

To look at your log file 

```bash
head braker/braker.log
```

This is where braker will report its progress. 

# LQ 3 

After your run is complete, what does the **end of your log file look like?** You can upload a screenshot, copy the end of the file, or send the entire file. 

If your assembly has _not been completed_ by the lab due date, upload the last lines in your file. 


## Step 5 - Preparing for the next lab

Our analyses will run for a long time. To prepare us for next lab let's answer some questions about our output files. 


### Step 5a - Braker output files

The version of braker we are using only outputs gff or gff3 files. We have it set to generate our gff3 files and it will be named **"braker.gff3**

Take a look at this example of gff3 format https://learn.gencore.bio.nyu.edu/ngs-file-formats/gff3-format/ 

# LQ 4 
How many required fields are there in gff3 format?

# LQ 5 
What is the default or blank value used in GFF3 format?

# LQ 6
We will need to extract DNA and amino acid sequences from our genome using our gff3 file. We will be using this program: getfasta
Look at the documentation for getfasta https://bedtools.readthedocs.io/en/latest/content/tools/getfasta.html

Write and report the command you would use to extract all our DNA sequences from the genome. 
















