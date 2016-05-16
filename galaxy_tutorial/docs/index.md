Introduction to Galaxy
======================

The tutorial is the modified version which was written by [Simon
Gladman](mailto:simon.gladman@unimelb.edu.au) - VLSCI

Background
----------

Galaxy is a web based analysis and workflow platform designed for
biologists to analyse their own data. It comes with most of the popular
bioinformatics tools already installed and ready for use. There are many
Galaxy servers around the world and some are tailored with specific
toolsets and reference data for analysis of human genomics, microbial
genomics, proteomics etc.

There are some introductory slides available
[here](https://docs.google.com/presentation/d/1dzHagGkswjH7MOZ7OACVXGU-riBs33K3J5lWpnCpPhs/pub?start=false&loop=false&slide=id.g537781ff1_2_18).

Basically, the Galaxy interface is separated into 3 parts. The tool list
on the left, the viewing pane in the middle and the analysis and data
history on the right. We will be looking at all 3 parts in this
tutorial.

![Galaxy interface components diagram](./images/Galaxy_components.png)

This workshop/tutorial will familiarize you with the Galaxy interface.
It will cover the following topics:

-   Logging in to the server
-   Getting data into galaxy
-   How to access the tools
-   Using to use some common tools

------------------------------------------------------------------------

Learning Objectives
-------------------

At the end of this tutorial you should:

Be able to upload data to a Galaxy server from:
    -   A file on your local computer
    -   A file on a remote datastore with an accessible URL.
    -   A file UCSC genome browser **missing**

Be able use tools in Galaxy by:
    -   Accessing the tool via the tool menu
    -   Using the tool interface to run the particular tool
    -   Viewing/accessing the tool output.

------------------------------------------------------------------------

Section 1: Preparation.
-----------------------

The purpose of this section is to get you to log in to the server..

1.  Go to [MDC galaxy production sever](https://galaxy.mdc-berlin.net/galaxy/)

2.  Log in:

    -   Enter your MDC user name
    -   Enter your password
    -   Click **OK**

------------------------------------------------------------------------

Section 2: Getting data into Galaxy
-----------------------------------

There are 2 main ways to get your data into Galaxy. We will use each of
these methods for 3 files and then work use those 3 files for the rest
of the workshop.

-   Start a new history for this workshop. To do this:

    -   Click on the history menu button (the
        ![](images/Galaxy-menu.png) icon)
        at the top of the Histories panel.
    -   Select **Create New**

It is important to note that Galaxy has the concept of "File Type" built
in. This means that each file stored needs to have its type described to
Galaxy as it is being made available. Examples of file types are: text,
fasta, fastq, vcf, GFF, Genbank, tabular etc.

We will tell Galaxy what type of file each one is as we upload it.

### Method 1: Upload a file from your own computer

With this method you can get most of the files on your own computer into
Galaxy. (there is a size limit)

-   Download the following file to your computer: **to change**
    *https://swift.rc.nectar.org.au:8888/v1/AUTH\_377/public/galaxy101/Contig\_stats.txt.gz*

    -   From the Galaxy tool panel, click on **Get Data -&gt; Upload
        File**
    -   Click the **Choose File** button
    -   Find and select the *Contig\_stats.txt.gz* file you downloaded
        and click **Open**
    -   Set the "file format" to *tabular*
    -   Click the **Start** button
    -   Once the progress bar reaches 100%, click the **Close** button

The file will now upload to your current history.

### Method 2: Upload a file from a URL

If a file exists on a web resource somewhere and you know its URL
(Unique resource location - a web address) you can directly load it into
Galaxy.

-   From the tool panel, click on **Get Data -&gt; Upload File**

    -   Click on the **Paste/Fetch Data** button
    -   Copy and paste the following web address into the URL/Text box: **to change**
        *https://swift.rc.nectar.org.au:8888/v1/AUTH\_377/public/COMP90014/Assignment1/bacterial\_std\_err\_1.fastq.gz*
    -   Set the file format to *fastqsanger* (not fastqcsanger)
    -   Click **Start**
    -   Once the progress bar has reached 100%, click **Close**

Note that Galaxy is smart enough to recognize that this is a compressed
file and so it will uncompress it as it loads it.

### Method 2 (again): Get data from a public URL

Now we are going to upload another file from the remote data source.

Repeat the above for:
*https://swift.rc.nectar.org.au:8888/v1/AUTH\_377/public/MRSA0252.fna*

Note that this file is a *fasta* file and not a *fastqsanger* file.

The DNA sequence of *Staphlococcus aureus MRSA252* will be loaded into
your history as a fasta file.


### The data

Though we aren't going to focus on the contents of these files and what
they mean from a bioinformatics standpoint, here is a brief description
of each one.

-   *Contigs\_stats.txt*

    -   this file contains a table of summary data from a de novo genome
        assembly (the process of attempting to recover the full genome
        of an organism from the short read sequences produced by most
        DNA sequencing machines. )
    -   The columns contain a lot of information but the ones we will be
        using indicate the amount of data (or coverage) that went into
        making up each piece of the final assembly.

<!-- -->

-   *bacterial\_std\_err\_1.fastq.gz*

    -   This file contains sequence reads as they would come off an
        Illunina sequencing machine. They are in
        [fastq](https://en.wikipedia.org/wiki/FASTQ_format) format.

<!-- -->

-   *MRSA0252.fna*

    -   This file contains the genome sequence of *Staphylococcus aureus
        MRSA252*. It is in
        [fasta](https://en.wikipedia.org/wiki/FASTA_format) format.

------------------------------------------------------------------------

Section 3: Play with the tools
------------------------------

The purpose of this section is to get you used to using the available
tools in Galaxy and point out some of the more basic manipulation tools.

Firstly however, you’ll notice that two of the files have very long and
confusing names. So we might want to change them. To do this we need to
“edit” the file. So:

1.  Click on the
    ![](images/Galaxy-edit.png)
    icon (edit) next to the file in the history called:
    *https://swift.rc.nectar.org.au:8888/v1/AUTH\_377/public/COMP90014/Assignment1/bacterial\_std\_err\_1.fastq*
2.  In the "Name" text box, give it a new name. Call it: *Typical Fastq
    File*
3.  Click the **Save** button.

Repeat the process for the MRSA252 fasta file. Rename it to
*MRSA252.fna*

Now that’s better. There was a lot of other functionality hidden behind
that edit
(![](images/Galaxy-edit.png))
icon. You can change a file’s data type, convert its format and many
other things. Feel free to play around with them.

Ok, back to the tools..

### Example 1: Histogram and summary statistics

The first thing we are going to do is produce a histogram of contig read
coverage depths and calculate the summary statistics from the
Contig\_stats.txt file. To do this we need to cut out a couple of
columns, remove a line and then produce a histogram. This will introduce
some of the text manipulation tools.

Click on the
![](images/Galaxy-view.png)
icon of the *Contig\_stats.txt* file to have a look at it. Note that
there are 18 columns in this file. We want column 1 and column 6. To do
this:

**1. Cut out column 1 and column 6.**

-   From the tool panel, click on **Text Manipulation -&gt; Cut** and
    set the following:
-   Set "Cut Columns" to: *c1,c6*
-   "Delimited by": *Tab*
-   "Cut from": *Contig\_stats.txt*
-   Click **Execute**

Examine the new file by clicking on it’s
![](images/Galaxy-view.png)
icon. We now have 2 columns instead of the 18 in the original file.

**2. Remove the Header lines of the new file.**

-   From the tool panel, click on **Text Manipulation -&gt; Remove
    beginning** and set the following:
-   "Remove First": *1*
-   "from": *Cut on data1*
-   click **Execute**

Note the the new file is the same as the previous one without the header
line.

**3. Make a histogram.**

-   From the tool panel, click on **Graph/Display Data -&gt; Histogram**
    and set the following:
-   "Dataset": *Remove beginning on Data X*
-   "Numerical column for X axis": *c2*
-   "Number of breaks": *25*
-   "Plot title": *Histogram of Contig Coverage*
-   "Label for X axis": *Coverage depth*
-   Click **Execute**

Click on the
![](images/Galaxy-view.png)
icon of the histogram to have a look at it. Note there are a few peaks..
Maybe these correspond to single, double and triple copy number of these
contigs.

**4. Calculate summary statistics for contig coverage depth.**

-   From the tool panel, click on **Statistics -&gt; Summary
    Statisitics** and set the following:
-   "Summary statistics on": *Remove beginning on Data X*
-   "Column or expression": *c2*
-   Click **Execute**

You’ll note that the summary statistics tool failed and is red in the
history. There was an error! If you click on the filename, and then the
bug
![](images/Galaxy-bug.png)
symbol, it will tell you what went wrong. (There is a missing python
library.) At this point, you would normally contact your Galaxy server
administrator.

### Example 2: Convert Fastq to Fasta

This shows how to convert a fastq file to a fasta file. The tool creates
a new file with the converted data.

**Converter tool**

-   From the tool panel, click on **Convert Formats -&gt; FASTQ to
    FASTA** and set the following:
-   "FASTQ file to convert": *Typical Fastq File*
-   Click **Execute**

This will have created a new Fasta file called FASTQ to FASTA on data 2.

### Example 3: Find Ribosomal RNA Features in a DNA Sequence

This example shows how to use a tool called “barrnap” to search for
rRNAs in a DNA sequence.

**1. Find all of the ribosomal RNA's in a sequence**

-   From the tool panel, click on **Annotation -&gt; barrnap** and set
    the following:
-   "Fasta file": MRSA252.fna
-   Click **Execute**

A new file called *barrnap on data 3* will be produced. It is a gff3
file. (This stands for genome feature format - version 3. It is a file
format for describing features contained by a DNA sequence.) Change it’s
name to something more appropriate (click on the
![](images/Galaxy-edit.png)
icon.) There is also a STDERR output file from this tool - just ignore
this one.

Now lets say you only want the lines of the file for the 23S rRNA
annotations. We can do this using a Filter tool.

**2. Filter the annotations to get the 23S RNAs**

-   From the tool panel, click on **Filter and Sort -&gt; Select** and
    set the following:
-   "Select lines from": (whatever you called the barrnap gff3 output)
-   "the pattern": *23S* (this will look for all the lines in the file
    that contain “23S”)
-   Click **Execute**

Now you have a gff3 file with just the 23S annotations!

What now?
---------

Remember how we started a new history at the beginning? If you want to
see any of your old histories, click on the history menu button
![](images/Galaxy-menu.png)
at the top of the histories panel and then select “Saved Histories.”
This will give you a list of all the histories you have worked on in
this Galaxy server.


------------------------------------------------------------------------

Galaxy Workflows
================
------------------------------------------------------------------------

Section 1: Create and run a workflow.
-------------------------------------

This section will show you two different methods to create a workflow
and then how to run one.

### Import the workflow history

This step will show you how to import a history from a remote source
into your own workspace. We will be using this history to build a
workflow.

-   From the histories menu
    ![](images//Galaxy-menu.png),
    click **Import from File**.
-   Enter
    *https://swift.rc.nectar.org.au:8888/v1/AUTH\_377/public/Workflow-finished-history.tar.gz*
    in the URL box.
-   Click **Submit**

You might have to wait for a bit, then:

-   From the history menu
    ![](images//Galaxy-menu.png),
    click **Saved Histories**
-   Select the history: *Imported: Workflow-finished*

### Workflow creation: Method 1

We will create a workflow from an existing history. You can use this
method to make a re-useable analysis from one you’ve already done. i.e.
You can perform the analysis once and then create a workflow out of it
to re-use it on more/new data. We will create a workflow from the
history you imported in step 1 above. The footnote below explains the
steps that created this history. These are the steps we will mimic in
the workflow.

Make sure your current history is the one you imported in Section 2 -
Step 1 above (*imported: Workflow\_finished.*) If not, switch to it.

**Now we will create the workflow.**

-   Click on the histories menu button
    ![](images//Galaxy-menu.png)
    at the top of the history pane.
-   Click **Extract Workflow**

You will now be shown a page which contains the steps used to create the
history you are extracting from. We use this page to say what to include
in the workflow. We want everything here so we’ll just accept the
defaults and:

-   Change the Workflow name to something sensible like “Basic Variant
    Calling Workflow”
-   Click **Create Workflow**

The workflow is now accessible via the bottom of the tool pane by
clicking on All Workflows.

#### Some discussion:

Have a look at your workflow. Click on its button in the workflow list.
It’s tool interface will appear. You can now run this workflow any time
you like with different input datasets. NOTE: The input data sets must
be of the same types as the original ones. i.e. Two fastq reads files
and one fasta reference sequence.

More interesting though is to:

-   Click on the **Workflows** link in the top menu
-   Click on the down arrow on your workflow’s button.
-   Click **Edit**

A visualisation of your workflow will appear. Note the connections and
the steps.

Next we’ll go through how to create this workflow using the editor..

### Workflow Creation: Method 2

We will now create the same read mapping/variant calling workflow using
the editor directly. We need to get some reads and a reference, map the
reads to the reference using BWA, run Freebayes on the BAM to call the
variants, and finally filter the resulting vcf file.

#### Step 1: Create a workflow name and edit space. {#step-1-create-a-workflow-name-and-edit-space}

-   Click on **Workflow** in Galaxy’s menu.
-   Click on the **Create New Workflow** button.
-   In the "Workflow Name" text box type: *Variants from scratch*
-   Click the **Create** button.

You’ll now see a list of workflows. Your’s will be in that list.

#### Step 2: Open the editor and place component tools

-   Click on the down arrow on your workflow’s button.
-   Select **Edit**

You’ll be presented with a blank workflow grid.

**Add three input datafiles.**

-   In the Workflow control section of the tool pane, click on **Inputs
    -&gt; Input dataset** three times.
-   Spread them out towards the left hand side of the workflow grid by
    clicking and dragging them around.
-   For each one, change their name.
    -   Click on each input box in turn
    -   In the right hand pane (where the history usually is), change
        the name to:
        -   Reference data
        -   Reads 1
        -   Reads 2 - respectively.

**Add in the BWA mapping step.**

-   Click on **NGS: Mapping -&gt; Map with BWA** in the tool pane. BWA
    will be added to the workflow grid.
-   In the right hand pane (where the history usually is), change the
    following parameters.
    -   Change “Will you select a reference genome from your history or
        use a built-in index?:” to *Use a genome from history.*
    -   Note that the BWA box on the grid changes to match
        these settings.

**Connect the tools together.**

-   Click and drag on the output of one of the input dataset tools to
    each of the input spots in the BWA tool. (Make connections.)
    -   "Reference data" output to reference to "Use the following
        dataset as the reference sequence"
    -   "Reads 1" output to "Select first set of reads"
    -   "Reads 2" output to "Select second set of reads"

**Add in the Freebayes (Variant Calling step.)**

-   Click on **NGS: Variant Calling -&gt; Freebayes**
-   In the right hand pane, change the following:
    -   "Choose the source for the reference list:" to *History*
    -   Connect "Map with BWA" bam output to "Freebayes’" bam input.
    -   Connect the "Reference data" output to "Freebayes’" *Use the
        following dataset as the reference sequence* input.

If you’re keen - **Note: this is optional.** Also change the following
parameters the right hand pane for freebayes to make it a bit more
sensible for variant calling in bacterial genomes.

-   "Choose parameter selection level": *Complete list of all options*
-   "Set population model": *Yes*
-   "Set ploidy for the analysis": *1*
-   "Set input filters": *Yes*
-   "Exclude alignments from analysis if they have a mapping quality
    less than": *20*
-   "Exclude alleles from analysis if their supporting base quality is
    less than": *20*
-   "Require at least this fraction of observations … to evaluate the
    position": *0.9*
-   "Require at least this count of observations .. to evaluate the
    position": *10*
-   "Set population and mappability priors": *Yes*
-   "Disable incorporation of prior expectations about observations":
    *Yes*

**Add in the Filter step.**

-   Click on **Filter and Sort - &gt; Filter**
-   Connect "Freebayes’" output\_vcf to the "filter" input.
-   In the right hand pane, change the following:
    -   "With the following condition": *c6 &gt; 500*
    -   "Number of header lines to skip": *56*

Phew! We’re nearly done! The only thing left is to select which workflow
outputs we want to keep in our history. Next to each output for every
tool is a star. Clicking on the stars will select those files as
workflow outputs, everything else will be hidden in the history. In this
case we only really want the BAM file and the final variants (vcf file.)
Therefore:

**Select workflow outputs.**

-   Click on the star next to "Map with BWA’s" bam file output.
-   Click on the star next to "Filter’s" output vcf.

#### Step 3: Save it!

Click on the
![](images//Galaxy-menu.png)
at the top of the workflow grid and select **Save**.

Congratulations. You’ve just created a Galaxy workflow.

Now to run it!

### Running the workflow

We will now make a new history called "Test" and run the workflow on
it’s data.

#### Create the new history

-   From the Histories Menu, select **Copy Datasets**
-   Select the 2 x fastq files and the Ecoli .fna file.
-   Under destination history, enter *Test* into "New History Named:"
-   Click **Copy History Items** button
-   Click on the link to the new history in the green bar at the top of
    the screen

#### Run the workflow

-   On the tools pane, click **All Workflows**
-   Select the *Variants from scratch* workflow (or whatever you
    called it.)
-   Give it the correct files.
-   *Ecoli ... .fna* for Reference data
-   *bacterial\_std\_err\_1.fastq* for Reads 1
-   *bacterial\_std\_err\_2.fastq* for Reads 2
-   Click **Run Workflow**

Your workflow will now run. It will send the right files to the right
tools at the right time to the cluster (compute engine on your machine)
and wait for them to finish. Watch as they turn yellow then green in
turn.

What now?
---------

Where to start? There’s so much you can do with Workflows. You can even
run them on multiple file sets from the one setup.

That's it. You now know a bit about the Galaxy interface and how to load
data, run tools and view their outputs. For more tutorials, see
<http://genome.edu.au/learn>

------------------------------------------------------------------------

Documentation built with [MkDocs](http://www.mkdocs.org/).
