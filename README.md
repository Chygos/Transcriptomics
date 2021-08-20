# Visualization of Differential gene expression

1. After adjusting p values and annotation of genes, the most differentially expressed genes were selected. They were joined by using “Join two datasets” which used the input as normalized counts generated by DESeq2. The cut tool is used to extract the columns with the gene IDs and normalized counts. The differentially expressed genes are represented in terms of log 2 FC(fold-change) by DESeq2.(how many times the change in expression has occurred). Then, heatmap was generated using heatmap2.

## To plot the heatmap:
*a. param-file* 
*b. “Input should have column headers”: Normalized counts for the most differentially expressed genes* 
*c. “Advanced - log transformation”/“Data transformation”: Log2(value) transform my data* 
*d. “Enable data clustering”: Yes* 
*e. “Labeling columns and rows”: Label columns and not rows* 
*f. “Coloring groups”: Blue to white to red* 


2) Another statistical measure is to calculate the z score and represent expression in terms of deviation from mean. This is done using table compute function for normalized counts; which says how far from mean values our actual readings are (in terms of standard deviations). Note that +-3SD has around 99.6% of data. Lower expressed (downregulated) genes will have negative SD, and upregulated will have positive SD. Our samples will show a plus or minus representation. Another heatmap is plotted to see how individual samples fare.

## Table Compute 
### with the following parameters to first subtract the mean values per row
“Input Single or Multiple Tables”: Single Table
param-file
“Table”: Normalized counts for the most differentially expressed genes
“Type of table operation”: Perform a full table operation
Custom expression on ‘table’, along ‘axis’ (0 or 1)”: table.sub(table.mean(1), 0)
The table.mean(1) expression computes the mean for each row (here the genes) and table.sub(table.mean(1), 0) subtracts each value by the mean of the row (computed with table.mean(1))
 
### “Input Single or Multiple Tables”: Multiple Table
param-file
“Table1”: Normalized counts for the most differentially expressed genes
Click on: “Insert Tables”
“Table2”: Table compute output
Custom expression on ‘table2.div(table1.std(1),0)‘
The table1.std(1) expression computes the standard deviations of each row on the 1st table (normalized counts) and table2.div divides the values of 2nd table (previously computed) by these standard deviations.
Rename the output to Z-scores for the most differentially expressed genes
 
## To plot the heatmap:
“Input should have column headers”: Z-scores for the most differentially expressed genes
“Advanced - log transformation”/“Data transformation”: Plot the data as it is
“Enable data clustering”: Yes
“Labeling columns and rows”: Label columns and not rows
“Coloring groups”: Blue to white to red
 





