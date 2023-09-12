# Lab4_Genome_Annotation

## Introduction

In the lab today we will be annotating our genomes. Annotation is the process of finding the genes. The software we will run, called MAKER, attempts to identify the beginning and end of genes. It will also identify exons and introns within the gene. 

![image](https://github.com/BINF-3101/Lab4_Genome_Annotation/assets/47755288/77b896a0-47e3-470a-a507-b74b94a66093)

Genes within genomes can be distributed in very different ways. Some genomes have lots of genes that are closely packed. The human genome, conversely, has long stretches of DNA that do not contain genes. 

Yeast genomes are typically compact and the genes contain few introns. We need to **train our model** to know what type of genome we have. 



## Step 1: Set up your Lab 4 Folder

## Step 2: Mask our genome

Our genome likely contains highly repetitive regions. We want to hide or mask those regions. This helps the genome annotation software ignore these repeated regions

### Step 2a: Load repeatmasker

We will be using a software called repeatmasker which is already installed on the cluster

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

Repeatmasker looks for insertion elements from a common laboratory bacteria. What is this bacteria?


The output from this pipeline will be **SRR1234-contigs.v2.masked**

## Step 4 




