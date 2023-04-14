# lab notebook -Connor Edgerly- R@tt

### Day 1
# ls ; this lists all the files in my current working directory
# pwd ; print working directory
## tab button auto completes
# cd ; Changes you into a new directory
# PS1='$ ' ; Sets thing to get rid of the text on the directory?
# Ctrl-C ; Cancel current command line
# rm ; removes directory

## command line, Batch, same thing?
# ssh cme1029@ron.sr.unh.edu ; connects terminal to the cluster
# cme1029zfG1 ; base password
## if: Brokey - Then: open new teminal


### Day 2
# Login
# ssh cme1029@ron.sr.unh.edu
# password
# dumbrat1 (Its dumb rat, not dum brat. i wanted to just have it rat but it wouldnt allow it)

# pwd ; view current directory
# cp ; copy file
# ls ; lists files in file
# cd ; change directory
# tar -zxf shell_data.tar
# -zxf options
# ls -F ; shows folders that are enter-able
# head ; uh, opens a file?
# mkdir ; make a directory
# head -n10 ; shows the first 10 lines
# grep ; show all in file
# | ; pipe to
# wc ; word count
# wc -l ; line count
# Ex. grep '@SRR' SRR...fastq | wc -l
#     grep (find) {thing to find} {file name} | (send to) wc (word count) -l (counts lines)
# cd ../ ; go backwards a folder
# cd ~ ; goes to the root directory


### Day 3
# cd / ; needed to get to absolute path
# cd /home/users/cme1029/gen711/shell_data/ 'Example path'

## Exercise - 3 ways to return to home directory
#   1. cd ~
#   2. cd ../ (multiple times)
#   3. cd /home/users/cme1029/gen711/

# ls -a ; show hidden files
# cat ; opens whole file. concatinate, sticks two files together.
# ls *(.fastq) ; lists all files with variable * (wildcard)
# > ; sends the data to a new file

## Exercise - List all applications of the bin directory of the titles C and A
#   cd /home
#   ls c*
#   ls c* | wc -l   = 90 files
#   ls a*
#   ls a* | wc -l   = 45 files
#   ls o*
#   ls o* | wc -l   = 22 files

# echo ; reads statement
# echo *fastnothing > newfile ; creates file
# echo *fastnothing >> newfile ; adds line to a file
# history | show previous imputs
# grep -A# takes # lines after
# grep -B# Takes # lines before


### Day 4
# realpath (); shows absolute path into a folder
# >> ; append adds to a file
# clear ; clears terminal
# mkdir -p ; makes path from current directory
# gunzip ; unzip files
# conda activate genomics ; loads up a new environment with all programs installed
# fastqc -h ; help directory for fastq command
# mv ; 
# mkdir ; Make directory
# less ; 
# sftp ;

# shift z ; pauses current thing
# bg ; runs program in background
# top ; looks at all the programs running
# q ; returns to command line
# less -S ; shows in a run-on format

# tail ; shows the last lines of a file

## Exercise
# ls -sh ; find size of files 

# --outdir ; outputs
# fastqc () ; runs command
# mkdir -p ~/dc_workshop/results/fastqc_untrimmed_reads
# rmdir ; removes directory
# kill ; Command word: kill
# unzip ; another way to unzip


### Day 5 - Trimming and Filtering
# Hidden Markov Models

# cd ~/desktop
# sftp cme1029@ron.sr.unh.edu
# sftp ; logs into the downloader to this pc
# get ; downloads from file path

## this is a thing
trimmomatic PE -threads 4 SRR_1056_1.fastq SRR_1056_2.fastq \
    SRR_1056_1.trimmed.fastq.gz SRR_1056_1un.trimmed.fastq.gz \
    SRR_1056_2.trimmed.fastq.gz SRR_1056_2un.trimmed.fastq.gz \
    ILLUMINACLIP:SRR_adapters.fa SLIDINGWINDOW:4:20

for infile in *_1.fastq.gz do
    base=$(basename ${infile} _1.fastq.gz)
    trimmomatic PE ${infile} ${base}_2.fastq.gz \
    ${base}_1.trim.fastq.gz ${base}_1un.trim.fastq.gz \
    ${base}_2.trim.fastq.gz ${base}_2un.trim.fastq.gz \
    SLIDINGWINDOW:4:20 MINLEN:25 ILLUMINACLIP:NexteraPE-PE.fa:2:40:15
done

## This is also a thing
# cp /opt/anaconda/anaconda/pkgs/trimmomatic-0.39-1/share/trimmomatic-0.39-1/adapters/NexteraPE-PE.fa .

## Exercise (when trimmomatic is done)
# 1. make a folder called ‘trimmed_fastq’ in data
# get to the data file then type
# mkdir -p trimmed_fastq


# 2. move all files that we made (hint: .trim and the move command, and the destination directory will work)
# cp /tmp/trimmed/*fastq.gz . ; while in the trimmed foleder

# 3. Re-run fastqc on the trimmed fastqs in the trimmed_fastq folder.
# fastqc *fastq.gz


### Day 6

# curl ; copy url to folder
# tar (untars) xvf (something)
# conda env list ; lists all conda environments
# bwa ; help page for bwa
# bwa mem ; alligns reads to ref
# mv ; move stuff
# grep -v ; search for inverse
# ^ ; searches for at the start of a line
# samtools ; another set of program that have something to do with sam and bam
# -o ; determmines where the output will save


### Day 7

## PRACTICE QUESTIONS

## Practice practical
### Change your working directory to your gen711 folder with an absolute path
cd /home/users/cme1029/gen711

### Change your working directory to the 'shell data' folder
cd ~/gen711/shelldata/

### Use grep to search for a bad read ( any read with 7 uncalled bases in a row )
grep "NNNNNNN" SRR098026.fastq

### Use the 'B' option to get line above each match
grep -B1  "NNNNNNN" SRR098026.fastq

### How many lines below each grep line belong to a read?
2

### Use the 'A' and 'B' options with grep to return the read and info lines for each match
grep -B1 -A2  "NNNNNNN" SRR098026.fastq 
# 

### Redirect the bad reads in SRR098026.fastq to a file called bad_reads.fastq
echo 'temp' > bad_reads.fastq
grep -B1 -A2  "NNNNNNN" SRR098026.fastq > bad_reads.fastq

### How many lines are in this file? Paste the command below
cat badreads.fastq | wc -l

### Redirect the bad reads for both fastqs into bad_reads.txt using grep and pipes
grep -B1 -A2  "NNNNNNN" *.fastq > bad_reads.txt

### Determine how many bad read lines are in each of the fastq lines, and compare that with the number of lines in bad_reads.fastq
This Q is confusing... ;-;
400 in bad reads
249 in file

### Examine the file to find if there are any extra lines that might be throwing off your count. What did you use to look at the file?
used head, saw -- lines

### Add your name to the bottom of the bad_reads.fastq
echo Ratt >> badreads.fastq

### Add your name to the top of the bad_reads.fastq
sed '1i Ratt' badreads.fastq
# sed ; script editor

### Make a script that makes a file of bad reads and then puts your name at the end of new bad reads file
#!/bin/sh

### Change the permissions of the file and run the script


### Run md5sum on scripted_bad_reads.txt and write the output to my_md5sum.txt


### Day 8
# git clone https://github.com/cedgerly/lab-notebook.git ; moves the file onto your computer

# https://github.com/jthmiller/gen711-811-example

Project Title
Metabarcoding of cyanobacteria communities from New England Lakes over a summer.

# trio of commands to output your project
git add 
git commit
git push

# repositories ; used as like a time capsule folder thing