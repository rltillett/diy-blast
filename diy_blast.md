# DIY Bioinformatics - BLAST & friends

## Some tools suggested:
- PC or mac (assume windows)
- a web browser that can use NCBI web tools (pretty much anything)
- Atom text editor (portable download for classroom PCs)
   - atom windows portable instructions:
   - http://flight-manual.atom.io/getting-started/sections/installing-atom/#platform-windows
   - atom windows portable download: https://github.com/atom/atom/releases/download/v1.13.0/atom-windows.zip
   - atom windows installer (if user can install): https://github.com/atom/atom/releases/download/v1.13.0/AtomSetup.exe

-  Ape (a DNA editing/manipulation tool)
   - http://biologylabs.utah.edu/jorgensen/wayned/ape/
   - Ape download for windows:
   - http://biologylabs.utah.edu/jorgensen/wayned/ape/Download/Windows/ApE_win_current.zip
   - misc ape notes/warning:
      - in-app blast at ncbi may be broken b/c ncbi changed the API syntax / URLs

## Using the Basic Local Alignment Search Tool (BLAST)

### What is BLAST?
BLAST is a set of tools used to identify imperfect matches (similarity) between a query nucleotide/protein sequence with sequences stored in a database. For a given query sequence, BLAST reports the aligned regions of similarity.

### Why use BLAST?
- “What is my sequence and what does it do?”
   - You obtained DNA sequence from an experiment and need to know more about it
   - Comparing the novel sequence to known protein sequences to hypothesize gene function
   - Comparing a partial sequence to whole genome sequences
- Finding homologs to interesting genes in your favorite species
- Specialized BLASTs exist too
   - Make gene-specific primers for PCR (Primer-BLAST)
   - Screen a sequence for vectors (VecScreen)
   - Comparing two sequences (bl2seq)

### BLAST Example: a novel phage sequence

Obtain the appletree2 sequence
- Go to http://phagesdb.org
- In the “search phagesdb” text box type "appletree2" and click search
- click on the 1st search result to bring up the appletree2 record
- Scroll down and click on the link for “Yes: Download fasta file“
- Open the downloaded sequence in a text editor and/or ape

#### Performing BLAST at phagesdb
- starting from the appletree2 page
- click locally blast this genome
- click BLAST button

#### The Results Page (phagesdb)
- Query information
- The Graphic Summary
   - position indicates aligned region
   - color indicates score
- Descriptions
   - Scores
   - Expectation values
   - Identities
- Alignments
   - Two sets of letters: query on top, subject on bottom
   - Identical nucleotides indicated by the vertical line
   - If a gap (caused by mismatches between the query and subject) is large enough, the alignment may get split into two (or more) chunks between the query and subject
- Bit scores and expectation values
   - Bit scores are the “raw” scores for the pairwise alignment
   - e-values are an estimate of how likely such alignment would be (vs. pure chance)


#### Performing BLAST at NCBI
- Go to http://www.ncbi.nlm.nih.gov/
- On the right, under Popular Resources, click BLAST to go to the BLAST home page http://blast.ncbi.nlm.nih.gov/
- Choose the program nucleotide blast http://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&BLAST_PROGRAMS=megaBlast&PAGE_TYPE=BlastSearch&SHOW_DEFAULTS=on&LINK_LOC=blasthome
- Paste in the sequence of the gene of interest and click BLAST button
- Results page: similar to phagesdb? How are they different?

#### The Results Page (ncbi)
- Query information
- The Graphic Summary
   - position indicates aligned region
   - color indicates score
- Descriptions
   - Clickable gene names
   - Scores
   - Expectation values
   - Identities
- Alignments
   - Two sets of letters: query on top, subject on bottom
   - Identical nucleotides indicated by the vertical line
   - If a gap (caused by mismatches between the query and subject) is large enough, the alignment may get split into two (or more) chunks between the query and subject
   - Links (to the subject sequence entry in Genbank, Download links to the aligned sequence, to the whole subject sequence)
- Bit scores and expectation values (sortable at ncbi)
   - Bit scores are the “raw” scores for the pairwise alignment
   - e-values are an estimate of how likely such alignment would be (vs. pure chance)


   ### more on e-values
   - ncbi e-value videos
   	- video 1: e-values https://youtu.be/nO0wJgZRZJs
   	- video 2: 3 FAQs https://youtu.be/Z7ek7UoP7Bg

### Modifying BLAST parameters (at ncbi)
- Scroll back to top of page and click “Edit and Resubmit”
- Changing the database (click the help button for a description)
   - nt/nr (NCBI’s main database of sequences)
   - Refseq RNA
   - RefSeq Genomic
   - NCBI Genomes (chromosome)
- Let’s change the database used
   - In Program selection, change to NCBI Genomes
   - Click BLAST
   - What has changed?
- Restrict by species
- Search genomes only

### Comparing a partly unknown nucleotide sequence to proteins (blastx)
Obtain the gumball phase sequence
- Go to http://phagesdb.org
- In the “search phagesdb” text box type "gumball" and click search
- click on the 1st search result to bring up the gumball record
- Scroll down and click on the link for “Yes: Download fasta file“
- Open the downloaded sequence in a text editor and/or ape


Let's suppose I told you that there is a protein sequence somewhere within this range:
- between 16320 to 21107
- We can select this range using ape, via "select (from-to)" command and blast (at ncbi)
   - select (from-to)
   - copy
   - new blast query at ncbi
   - blastx
   - paste sequence
   - change translation table to Bacterial (11)
   - and go
- view blastx results
   - graphical map
   - hit list
   - pairwise comparisons
      - can we guess where our exact coordinates are?
   - accessing details from individual results
What is our protein, then?
- (this is what it does, biologically)
- http://viralzone.expasy.org/all_by_species/3955.html

### Specialized BLASTs (at phagesdb+NCBI)
#### Comparing two sequences (bl2seq)
- Appletree2 vs. one of its close relatives
   - Return to appletree2 page at phagesdb
   - Click “family relatives”
   - Choose Lebron
- Save Lebron’s sequence
- Return to ncbi blast home page
- “align two sequences”


### Another BLAST Example: “What relatives does a gene have in a model organism?”

Obtain this example sequence
- Go to http://www.ncbi.nlm.nih.gov/
- In the “all databases” text box type “VvCBF4” and click search
- In the Entrez page click “Nucleotide” to get to the 1 record of this sequence
- Click the word FASTA in the upper left
- If something went wrong, go here http://www.ncbi.nlm.nih.gov/nuccore/DQ497624
- Choose the program nucleotide blast
- Paste in the sequence of the gene of interest and click BLAST button
- Results page: anything curious about these results?
Modifying BLAST parameters (by genomes, by species)
- Let’s change the type of nucleotide blast used
   - Click edit and resubmit
   - In Program selection, change to blastn
- Searching genomes only
- Restrict by species (type the word "Arabidopsis")
