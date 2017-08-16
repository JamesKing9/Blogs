# Glossary

cosmid ..... 粘粒

restriction enzyme cleavage site ..... 限制性酶切位点

Strain ..... 菌株

Alternative Protocol ..... 替代方案

Additional Protocol ..... 附加方案

traditional ..... 经典的



---







# Choosing an Appropriate Strain of E. coli

Most investigators want to use strains of E. coli that are easy to transform with plasmid DNA (e.g., DH1 or MM294; for a full list of useful strains, please see Appendix 3). The vast majority of 
colEl-type plasmids introduced into these strains replicate to high copy number and can be isolated in high yield. However, a significant minority of recombinant plasmids transform strains of 
E. colt such as DH1 and MM294 with low efficiency, generate transformed colonies that are smaller than usual, and produce low yields of plasmid DNA. Most of these "difficult" plasmids can be 
shown to encode a protein that is toxic to E. coli or to contain inverted or repeated DNA 
sequences. 



# Chapter 4:  Working with High-capacity Vectors

sdfasdf

<img src=".\img\1.jpg" height="660px">    







# Chapter 11:  Preparation of cDNA Libraries and Gene Identification



## INTRODUCTION



## PROTOCOLS



### 1  Construction of cDNA Libraries

This traditional protocol is based on the Gubler-Hoffman method(1983) and is divided into six stages:

*   Stage 1: Synthesis of First-strand cDNA Catalyzed by Reverse Transcriptase
*   Stage 2: Second-strand Synthesis
*   Stage 3: Methylation of cDNA
*   Stage 4: Attachment of Linkers or Adaptors
*   Stage 5: Fractionation of cDNA by Gel Filtration through Sepharose CL-4B
*   Stage 6: Ligation of cDNA to Bacteriophage λ Arms
*   Alternative Protocol: Ligation of cDNA into a Plasmid Vector
*   Additional Protocol: Amplification of cDNA Libraries

### 2  Construction and Screening of Eukaryotic Expression Libraries



Stage 1: Construction of cDNA Libraries in Eukaryotic Expression Vectors 11.68 
Stage 2: Screening cDNA Libraries Constructed in Eukaryotic Expression Vectors 11.74 





### 3  Exon Trapping and Amplification



Stage 1: Construction of the Library 11.81 
Stage 2: Electroporation of the Library into COS-7 Cells 11.85 
Stage 3: Harvesting the mRNA 11.87 
Stage 4: Reverse Transcriptase-PCR 11.89 
Stage 5: Analysis of Clones 11.95 





### 4  Direct Selection of cDNAs with Large Genomic DNA Clones







## INFORMATION PANELS



Commercial Kits for cDNA Synthesis and Library Construction 11.107 
Mo-MLV Reverse Transcriptase 11.109 
Homopolymeric Tailing 11.110 
?gt10and ?gt11 11.111 
Constructing cDNA Libraries from Small Numbers of Cells 11.112 
In Vitro Packaging 11.113 
COS Cells 11.114 
Biotin 11.115 
Magnetic Beads 11.118 
Ligation-independent Cloning 11.121 







# Geneious Manual





### 14.1  Find Restriction Sites

**Restriction Enzymes**[1](https://assets.geneious.com/manual/10.2/GeneiousManual218.html#fn1x15) cut a nucleotide sequence at speciﬁc positions relative to the occurrences of the enzyme’s *recognition sequence* in the sequence. For example, the enzyme *EcoRI* has the recognition sequence GAATTC and cuts both the strand and the antistrand sequence after the G inside the recognition sequence[2](https://assets.geneious.com/manual/10.2/GeneiousManual219.html#fn2x15) , leaving a single-stranded overhang (*sticky end (overhang)*): 

​     

![PIC](https://assets.geneious.com/manual/10.2/figures/restriction_ecori.png)

The option **Find Restriction Sites...** from the **Tools** → **Cloning** menu or the context menu allows you to ﬁnd and annotate restriction sites on a nucleotide sequence.    

You can conﬁgure the following options: 

-   **Candidate Enzymes** lets you select a set of restriction enzymes from which you want to draw the ones to use in the analysis. This includes the options to use commonly used, or all known commercially available restriction enzymes. If you have created your own restriction enzyme set from your local database then this will also be listed (see below for how to create such a document). 

-   **Enzymes must match X to Y times:** only returns restriction enzymes which cut the sequence X to Y times. Results for enzymes that cut the sequence more or less than this will be discarded. If you set X to be 0, when this operation is complete, it will report which candidate enzymes do not cut the sequence. 

-   **Specifying cut regions**

    : To specify a region of sequence where you want the enzyme to cut or not cut, choose one of the options below, and use the base counters to specify a sequence range that the options apply to. If you have selected a region of sequence in the sequence viewer, clicking the refresh arrow next to the base number counters will copy the selected region to this setting. The following options are available:     

    -   **Cut Anywhere:** Returns enzymes which cut anywhere in the entire sequence. It is not possible to select a subregion with this setting. 
    -   **Must only cut between:** Returns enzymes which only cut between the speciﬁed bases. 
    -   **Must cut between (may cut outside):** Returns enzymes which cut between the speciﬁed bases, and may also cut outside that region. 
    -   **Must not cut between:** Returns enzymes which only cut outside the speciﬁed bases.

-   **Advanced**: This displays a table of all enzymes in your candidate set, including their recognition site, overhang, and methylation information (Figure [14.1     ](https://assets.geneious.com/manual/10.2/GeneiousManualse67.html#x217-31900014.1)). Only the enzymes selected in this table will be considered in the analysis; initially, all rows are selected. You can click on the column headers to sort the table ascending or descending by that column, and you can Shift+click and Ctrl+click to select a range of rows and to toggle the selection of a row, respectively. 

-   To create custom enzyme set, select the enzymes you want in the Advanced window, then click **Save Selected Enzymes** and give the set a name. This set will then be available in the **Candidate Enzymes** lists.

After conﬁguring your options, click **Apply** to record the restriction enzyme site annotations on the sequence. The annotation shows the enzyme’s recognition site, and the cut site. Once the document is saved, two new tabs will appear above the sequence view: **Enzymes** displays the list of enzymes and their cut positions; **Fragments** displays a list of fragments that would be produced from the restriction digests. These tables can be exported as .csv ﬁles for subsequent processing with other software such as e.g. Microsoft Excel®.    

To select the region between two cut sites on a sequence, Shift+click on the two restriction site annotations in the sequence view.    

------

​      

![PIC](https://assets.geneious.com/manual/10.2/figures/restriction_findSites.png) 

​     Figure 14.1:      **Find Restriction Sites** restriction enzymes table accessible under the **Advanced** option.    

------



##### Restriction Enzyme eﬀective length

Eﬀective length for restriction enzymes is displayed in both the **Advanced** table of enzymes, and in the **Enzymes** tab on the sequence viewer.    

Eﬀective length is a measure of how frequently an enzyme will cut, taking into account both sequence length and ambiguities. In other words, lower eﬀective length means an enzyme is expected to cut more frequently. Because ambiguous bases are more likely to match a sequence by chance, they contribute less than 1 to the eﬀective length.    

Eﬀective length is calculated as the sum of the following formula across all symbols in the recognition sequence, where n is the number of nucleotides each symbol represents.    

1 - log(n) / log(4)    

I.e. 1 for a ACGT, 0.5 for 2-ambiguity (MRWSYK),   .208s for 3-ambiguity (VHDB) and 0 for N.    

Note: The sum displayed in Geneious is rounded down to nearest .0 or .5    

See <http://search.cpan.org/dist/BioPerl/Bio/Restriction/Enzyme.pm#cutter> for a little explanation of why you would use this.    



### 14.6  Gibson Assembly

Gibson Assembly or Gibson Cloning is a method for seamless ligation of multiple sequences in a single reaction, without the need for restriction sites. The Gibson Assembly operation allows you to simulate cloning reactions that use an exonuclease to generate overlapping fragments for ligation, including Gibson Assembly, GeneArt® Seamless Cloning (5’ exonuclease), SLIC and In-Fusion® Cloning (3’ exonuclease). It can also be used to simulate cloning operations that do not use exonuclease such as CPEC and SLiCE. For an overview of the Gibson Assembly interface, see section [14.3    ](https://assets.geneious.com/manual/10.2/GeneiousManualse69.html#x221-32200014.3).    

To run a Gibson Assembly operation, optionally select a **Backbone** sequence, along with one or more **Insert** sequences, and then specify the type of exonuclease you wish to use for the reaction. You can adjust the order in which the sequences will be ligated in the **Construct Layout Panel**. Currently the Gibson Assembly operation can only be run using linear sequences.    

**Batch cloning** with alternate sequences can be performed using sequence lists. Each of the individual nucleotide sequences in a list will be inserted into a separate product at the same insert position.    

**Exonuclease:** The exonuclease activity deﬁnes which strand (if any) gets digested to expose complementary overhangs: 

-   **5’ exonuclease** (Gibson & GeneArt® Seamless Cloning): The enzyme chews back bases from the 5’ end to expose complementary overhangs. GeneArt® Seamless Cloning recommends a 15 bp overhang, while to perform a Gibson assembly a longer overhang of 25 to 40 bp is used in many protocols. 
-   **3’ exonuclease** (SLIC & In-Fusion® Cloning): The enzyme chews back bases from the 3’ end to expose complementary overhangs. A 15 bp overhang is recommended for In-Fusion® Cloning, while for SLIC a 25 bp overhang is recommended. 
-   **None** (CPEC & SLiCE): These two methods don’t use a speciﬁc exonuclease. Instead, CPEC ampliﬁes the whole strand with a polymerase, and SLiCE uses a cell extract to recombine DNA molecules using short-end homologies.

If there are existing, compatible, overhangs annotated on the selected sequences (e.g. those derived from restriction digest), they will be used for the ligation reaction. If existing overhang annotations are not compatible, or do not meet the speciﬁed requirements, the overhangs will be removed or ﬁlled in (depending on the overhang and the exonuclease chosen) prior to primer design.    

**Primer Options:** Here you can adjust parameters that inﬂuence creation of primers and overhangs: 

-   **Min Overhang Length:** The minimum length of the complementary overhangs between two adjacent sequences. Usually half of this length is added via primer extension to each sequence. For sequences ﬂanking the backbone, the full Min **Overhang Length** will be added to the insert sequence. 
-   **Min Overhang Tm:** The minimum melting temperature allowed for the annealing region between two adjacent sequences. The overhang length will be increased until the melting temperature satisﬁes this condition. 
-   **Tm Calculation:** Additional settings required by Primer3 to calculate the melting temperature. These settings are applied to both the overhang Tm calculation as well as to the primer Tm calculation.

##### Extension primers for creation of complementary overlaps

For sequences without existing complementary overlaps on both ends, a pair of primers will be created to generate complementary overlaps via Primer Extension PCR, as required. If both ends are complementary no primers will be generated. Primer design uses non-stringent conditions which may result in poor quality primers - we recommend that you check the generated primers before ordering them.    

Extensions will be added to the primer corresponding to the neighboring sequence, to generate complementary overhangs. Primers are generated only for insert sequences, as it is assumed that the vector should stay unmodiﬁed. For this reason the extension length of primers extending to the vector will be the full speciﬁed minimal overlap length, whereas extensions on primers between two inserts, will each be half of the total overlap length. If you wish to manually add modiﬁcations to primer extensions, these must be annotated onto the insert sequence as type ‘Gibson Primer Extension’, otherwise they will be included within the binding region.    

The melting temperature for the annealing region between the neighbouring sequences is calculated using the Tm characteristics setting in Primer Options. In many cases the Phusion DNA polymerase is used, for which it is recommended to use the Tm formula of [Breslauer et al. 1986](http://www.pnas.org/content/83/11/3746).    

For very short or long extensions, Primer3 might be unable to calculate a Tm. If Primer3 fails, Geneious will calculate the Tm using one of the formulas below - this will be Formula [14.1    ](https://assets.geneious.com/manual/10.2/GeneiousManualse72.html#x225-328001r1) if the sequence is too short (less than 13 bp), or Formula [14.2    ](https://assets.geneious.com/manual/10.2/GeneiousManualse72.html#x225-328002r2) if the length is greater than 13 bp. 

$Tm = 2[AT] + 4[GC]$ 		(14.1)

$Tm = 64.9 + \frac{41[GC]−16.4}{[AT GC ]} $		(14.2)

The primers generated in your Gibson Assembly will be listed in the Report Document, along with the calculated characteristics and any errors that occurred during the primer generation process. Furthermore any modiﬁcations (recession or maintaining overhangs, adding extensions to primers) are shown at the beginning of the document.    



### 14.7  Gateway® Cloning

Geneious contains three operations to assist with Gateway® cloning. Gateway is a registered trademark of Invitrogen Corporation. The **Gateway** option under the **Cloning** menu will perform a BP reaction and/or an LR reaction on the selected documents. If there are a mixture of AttB/AttP and AttL/AttR sites on the input documents, it will perform a BP reaction on all documents with AttB/AttP sites, followed by an LR reaction on the results of the BP reaction and any input documents with AttL/AttR sites.    

For example, to insert a PCR product with attB sites directly into a destination vector, select the PCR product, a donor vector, and a destination vector. Geneious will ﬁrst produce an entry clone from the PCR product and donor vector, then react this entry clone with the destination vector to produce an expression clone.    

##### Annotate att sites...

This operation searches for AttB, AttP, AttL and AttR sites and annotates them on your sequence.    

##### Add AttB Sites to PCR product

This operation allows you to add AttB sites to a PCR product. It will work on the following types of document: 

-   A PCR product. AttB sites will be appended to the PCR product. 
-   A document with primer binding sites annotated. If there is more than one pair, Geneious will ask you which pair to use. The PCR product will be extracted and AttB sites appended.



### 14.10  CRISPR site ﬁnder

The CRISPR/Cas9 system is an RNA-guided endonuclease technology for gene editing. This system requires guide RNA (gRNA) comprised of a 20 bp target sequence next to a PAM (Protospacer Adjacent Motif) to direct the Cas9 enzyme to the cleavage site. The Find CRISPR Sites tool will search for gRNA (“CRISPR”) sites in your selected sequences, and can score them based on on-target activity or potential oﬀ-target interactions.    

To search for CRISPR sites, ﬁrst select the sequence(s) you want to target. This can be any number of sequences and sequence list documents, and supports selections in the documents. For best performance the search region for each sequence should be limited to 1000 bp. Open the **Find CRISPR Sites** tool in the Cloning menu. Check **Anywhere in sequence** or **Selected region** depending on if you are targeting the full sequences or a selection from them. Enter the gRNA sequence you want to search for in the Motif panel. There is a help box in the Motif section of the options panel that explains how to input your motif and gives an example. After selecting your scoring and pairing options, press **OK** to start the operation. Geneious will ﬁnd potential CRISPR targets in your sequences and annotate them onto the documents.    

##### On-target Activity Score

CRISPR sites can be scored two ways. The ﬁrst is by predicting the on-target activity using the method proposed by [Doench et al, 2014](http://www.ncbi.nlm.nih.gov/pubmed/25184501). This scoring algorithm analyses the one- and two-base features of the gRNA, as well as the GC content, and uses an experimentally determined predictive model to score the expected activity level of the CRISPR target. Scores are between 0 and 1, with a higher score denoting higher expected activity. Note that ambiguous bases won’t contribute to this score.    

##### Oﬀ-target interaction analysis

The second scoring method compares a CRISPR site with other similar sites, and assigns a score based on how individual the CRISPR site is and how likely it is to induce oﬀ-target interactions. To enable this scoring check **Score sites through oﬀ-target analysis**. This function uses a scoring system proposed by [Zhang et al, 2013](http://www.nature.com/nbt/journal/v31/n9/full/nbt.2647.html), which takes into consideration the positions of mismatches between the CRISPR site and its oﬀ-target sites. Scores are between 0 and 100, with a higher score denoting less oﬀ-target activity.    

Selecting **Score against an oﬀ-target database** will prompt Geneious to search sequences in the given folder for oﬀ-target interactions of your CRISPR sites. The sequence you are targeting can be inside this folder. This way you can ﬁnd CRISPR sites that target a particular gene but are scored for interactions against the entire genome. The top 5 oﬀ-target sites are kept and annotated onto the CRISPR site even though all oﬀ-target interactions found are incorporated into the score. Scoring against an oﬀ-target database will signiﬁcantly increase the time taken for the operation to complete.    

Before scoring, the oﬀ-target database is searched for full exact matches of the whole target sequence. These exact copies of the target sequence are ignored during oﬀ-target scoring. The intervals that were ignored are reported at the end of the operation in a dialog box if only one target sequence is being searched. They can also be found by mousing over the name of the CRISPR sites annotation track in the sequence viewer.    

If multiple sequences are given as the targets, the option to **Score each sequence against all other selected sequences** is available. This checks for oﬀ-target interactions between the target sequences and incorporates them into the oﬀ-target scores.    

If **Score against an oﬀ-target database** is **not** selected, the CRISPR sites for a sequence will only be scored against any unselected stretches of that single sequence.    	

You can control the number of mismatches and indels allowed between a CRISPR site and its oﬀ-target sites by adjusting **Maximum mismatches allowed against oﬀ-targets**. Then use **Maximum mismatches allowed to be indels** to set the number of these mismatches allowed to be indels. Increasing these numbers will increase the time it takes for the search to complete.    

Geneious also recognises a seed region on CRISPR sites when scoring against oﬀ-targets. This is a region of the CRISPR guide sequence immediately adjacent to the PAM site that can tolerate fewer mismatches and no indels when compared to potential oﬀ-target sites ([Cho et al, 2014](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3875854/)). Geneious uses a 10 bp seed region that can tolerate a maximum of 2 mismatches.    

##### Pair CRISPR sites

To help minimize oﬀ-target interactions, the mutant Cas9 D10A Nickase can be used with a pair of gRNAs on complementary strands of a target sequence. This induces a single-stranded break at each site, simulating a double-stranded break overall. Oﬀ-target interactions of any one gRNA target will then be only a single nick, which is repaired with high ﬁdelity. This process is described by [Zhang et al, 2013.](http://zlab.mit.edu/assets/reprints/Ran_FA_Cell_2013.pdf)    

By selecting **Pair CRISPR sites**, only CRISPR sites that are within range of a complementary pair will be returned. You can specify the maximum overlap of the paired sites and the maximum space allowed between the paired sites. The maximum overlap and maximum space between sites are measured from the 5’, PAM-distal end of the CRISPR sites.    

The optimal CRISPR pairs will be linked when they are annotated onto your target sequence, though any CRISPR site with a potential pair will be returned. Optimal pairs are decided by averaging their oﬀ-target interaction scores.    

 

##### Results output

CRISPR sites are returned as annotations on your original sequences. Hovering the mouse over an annotation will bring up a tooltip showing the information about any scores calculated, plus the 5 highest-scoring oﬀ-target sites (if they are analysed). For each oﬀ-target site the score, location and oﬀ-target sequence are given. Mismatches to the CRISPR site are in red, and insertions in the oﬀ-target site are underlined and red.    

The annotations are colored based on their On-target, Oﬀ-target, or Paired score. If more than one type of score is calculated you can choose which score to color the annotations by using the **Color CRISPR Sites by** option. The annotations will be colored on a gradient starting at green (for good scores), moving through yellow and ending at red (for poor scores).    



---



# ~ End ~