# Lab4_Genome_Annotation

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

**THIS STEP WILL TAKE A LONG TIME** Braker is _not_ a quick program. We will discuss why this is in class. 




