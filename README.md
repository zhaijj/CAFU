## CAFU
CAFU is a Galaxy-based bioinformatics framework for comprehensive assembly and functional annotation of unmapped RNA-seq data from single- and mixed-species samples which integrates plenty of existing NGS analytical tools and our developed programs, and features an easy-to-use interface to manage, manipulate and most importantly, explore large-scale unmapped reads. Besides the common process of reads cleansing, reads mapping, unmapped reads generation and novel transcription assembly, CAFU optionally offers the multiple-level evidence analysis of assembled transcripts, the sequence and expression characteristics of assembled transcripts, and the functional exploration of assembled transcripts through gene co-expression analysis and genome-wide association analysis. Taking the advantages of machine learning (ML) technologies, CAFU also effectively addresses the challenge of classifying species-specific transcript assembled using unmapped reads from mixed-species samples. The CAFU project is hosted on GitHub (https://github.com/cma2015/CAFU), publically available via an Amazon Elastic Cloud disk image and a standardized Docker container.

## Overview of functional modules in CAFU
<style type="text/css">
	table.tableizer-table {
		font-size: 12px;
		border: 1px solid #CCC; 
		font-family: Arial, Helvetica, sans-serif;
	} 
	.tableizer-table td {
		padding: 4px;
		margin: 3px;
		border: 1px solid #CCC;
	}
	.tableizer-table th {
		background-color: #104E8B; 
		color: #FFF;
		font-weight: bold;
	}
</style>
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th>Functional modules</th><th>Functions</th><th>Applications</th><th>Input files</th><th>Main output files</th><th>Programs</th><th>References</th></tr></thead><tbody>
 <tr><td>Extraction of unmapped reads</td><td>Quality Control</td><td>Examine the quality of RNA-Seq data</td><td>Raw RNA-seq data</td><td>Quality examination reports (html)</td><td>FastQC (https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)</td><td>[1]</td></tr>
 <tr><td>&nbsp;</td><td>Trim Raw Reads</td><td>Trim poly-A/T and low-quality reads</td><td>Raw RNA-seq data</td><td>High-quality RNA-seq data (Fastq)</td><td>Fqtrim (version 0.9.7; https://ccb.jhu.edu/software/fqtrim/)</td><td>[2]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>Trimmomatic (version 0.36; http://www.usadellab.org/cms/?page=trimmomatic)</td><td>[3]</td></tr>
 <tr><td>&nbsp;</td><td>Generate Unmapped Reads</td><td>Align trimmed reads and obtain unmapped reads</td><td>High-quality RNA-seq data; Reference sequences of corresponding species</td><td>Alignment results (BAM); Unmapped reads (Fastq)</td><td>HISAT2 (version 2.1.0; https://ccb.jhu.edu/software/hisat2/index.shtml)</td><td>[4]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>SAMTools (version 1.8; http://samtools.sourceforge.net/)</td><td>[5]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>BEDTools (version 2.27.0; http://bedtools.readthedocs.io/en/latest/)</td><td>[6]</td></tr>
 <tr><td>De novo transcript assembly of unmapped reads</td><td>Assemble Unmapped Reads</td><td>De novo assemble unmapped reads, remove redundancy of transcript fragments and re-assemble transcript fragments</td><td>Unmapped reads</td><td>Assembled transcript sequences (Fasta)</td><td>Trinity (version 2.2.0; https://github.com/trinityrnaseq/trinityrnaseq/wiki)</td><td>[7]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>CD-HIT-EST (version 4.6.8; http://weizhongli-lab.org/cd-hit/)</td><td>[8]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>CAP3 (version 12/21/07; http://seq.cs.iastate.edu/cap3.html)</td><td>[9]</td></tr>
 <tr><td>Evidence support of assembled transcripts</td><td>Expression-level Evidence</td><td>Obtain confident transcripts according to read coverage and expression abundance</td><td>All transcripts (combine reference transcript and assembled transcripts); High-quality RNA-seq data </td><td>Expression matrix; Confident transcript ID</td><td>RSEM (version 1.3.0; https://deweylab.github.io/RSEM/) ; Bowtie2 (version 2.3.4.1; http://bowtie-bio.sourceforge.net/index.shtml)</td><td>[10, 11]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>BEDTools (version 2.27.0; http://bedtools.readthedocs.io/en/latest/)</td><td>[6]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>&nbsp;</td><td>Genome-level Evidence</td><td>Obtain confident transcripts according to transcript-genome alignments</td><td>Assembled transcripts; Reference sequences of corresonding and closely related speces</td><td>Alignment results (PSL); Confident transcript ID</td><td>GMAP (version 2015-09-29; https://github.com/juliangehring/GMAP-GSNAP)</td><td>[12]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>&nbsp;</td><td>Transcript-level Evidence</td><td>Obtain confident transcripts according to transcript-transcript alignments</td><td>Assembled transcripts; Reference transcripts of corresonding and closely related speces</td><td>Alignment results (PSL); Confident transcript ID</td><td>GMAP (version 2015-09-29; https://github.com/juliangehring/GMAP-GSNAP)</td><td>[12]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>&nbsp;</td><td>Protein-level Evidence</td><td>Obtain confident transcripts according to the protein potential</td><td>Assembled transcripts</td><td>Confident transcripts ID; Protein potential assessment results; Domain/family results</td><td>CPC2 (version 0.1; http://cpc2.cbi.pku.edu.cn/);</td><td>[13]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>Pfam (version 31.0; https://pfam.xfam.org/)</td><td>[14]</td></tr>
 <tr><td>Species assignment of assembled transcripts</td><td>SAT</td><td>Machine learning-based prediction of the original species of assembled transcripts</td><td>CDSs of two species; Assembled transcripts</td><td>SAT score</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>Sequence characterization of assembled transcripts</td><td>Characterize Nucleic-acid Feature</td><td>Explore the similarity between assembled and annotated transcripts in terms of the distribution of transcript length, exon length, G+C content</td><td>Confident transcripts; Reference transcripts</td><td>Diagnostic plots (barplot/density)</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>&nbsp;</td><td>Characterize Amino-acid Feature</td><td>Explore the similarity between assembled and annotated transcripts in terms of the distribution of amino acid-based features used in SAT</td><td>Confident transcripts; Reference transcripts</td><td>Diagnostic plots (barplot/density)</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>Expression profiles of assembled transcripts</td><td>Analysis Condition Specificity</td><td>Identify condition-specifically expressed transcripts</td><td>All transcripts; High-quality RNA-seq data; Sample information</td><td>Condition-specific table; Diagnostic plots(heatmap)</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>&nbsp;</td><td>Analysis Heterogeneous</td><td>Identify stablely expressed transcripts</td><td>Expression matrix; Sample information</td><td>Gini coefficient table; Diagnostic plot (dotplot)</td><td>In-house scripts</td><td>Our study</td></tr>
 <tr><td>&nbsp;</td><td>Analysis Differential Expression</td><td>Identify differentially expressed transcripts</td><td>All transcripts; High-quality RNA-seq data; Sample information</td><td>DE analysis table; Diagnostic plot (Volcano plot; Venn-daragram )</td><td>RSEM (version 1.3.0; https://deweylab.github.io/RSEM/) ; Bowtie2 (version 2.3.4.1; http://bowtie-bio.sourceforge.net/index.shtml)</td><td>[10, 11]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>EBSeq (version 3.7; https://bioconductor.org/packages/release/bioc/html/EBSeq.html)</td><td>[15]</td></tr>
 <tr><td>Function annotation of assembled transcripts</td><td>Co-expression and GO</td><td>Invesitgate the putative function of assembled transcripts through co-expression network and GO enrichment analysis</td><td>Expression matrix</td><td>Co-expression result tables; Diagnostic plot (Dendrogram); GO analysis table</td><td>WGCNA (version 1.63; https://cran.r-project.org/web/packages/WGCNA/index.html)</td><td>[16]</td></tr>
 <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>topGO (version 3.7; https://bioconductor.org/packages/release/bioc/html/topGO.html)</td><td>[17]</td></tr>
</tbody></table>
