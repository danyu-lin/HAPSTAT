# **HAPSTAT**

# **HAPSTAT: Software for the statistical analysis of haplotype-disease association**

-   [Examples](https://dlin.web.unc.edu/software/hapstat/#examples)

-   [Effects](https://dlin.web.unc.edu/software/hapstat/#effects)

-   [Frequency](https://dlin.web.unc.edu/software/hapstat/#frequency)

-   [Input Data](https://dlin.web.unc.edu/software/hapstat/#data)

-   [Download](https://dlin.web.unc.edu/software/hapstat/#to_download)

HAPSTAT is a user-friendly software interface for the statistical analysis of haplotype-disease association. HAPSTAT allows the user to estimate or test haplotype effects and haplotype-environment interactions by maximizing the (observed-data) likelihood that properly accounts for phase uncertainty and study design. Cross-sectional, longitudinal, case-control and cohort studies are considered. The underlying methodology and a subset of the numerical algorithms used in HAPSTAT are found in [Lin and Zeng](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/LinZeng06.pdf) ([JASA](http://www.amstat.org/publications/jasa), 2006), [Lin, Zeng and Millikan](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/LinZengMillikan05.pdf) ([Genetic Epidemiology](https://onlinelibrary.wiley.com/journal/10982272), 2005), [Zeng, Lin, Avery, North and Bray](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/ZengEA06.pdf) ([Biostatistics](http://biostatistics.oxfordjournals.org/), 2006) and [Lin, Hu and Huang](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/LinHuHuang08.pdf) ([American Journal of Human Genetics, 2008](http://www.ajhg.org/)). The current version allows haplotype analysis of multiple genes as well as single- and multi-SNP analysis with missing genotypes, as as described in [Lin, Hu and Huang](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/LinHuHuang08.pdf).

The latest software release is HAPSTAT 3.0. The current and previous versions of the HAPSTAT software are available from the [download page](https://dlin.web.unc.edu/software/hapstat/#to_download). As this software and related materials are still under development, please check back frequently for updates.

## **General information**

The program is written in C++ language. Executable files are available for Windows and i386-based Linux in the download section below.

## **Usage**

On Windows systems:

> `maos.exe --pheno phenotype_file --geno genotype_file --out output_file`

On Linux systems:

> `maos --pheno phenotype_file --geno genotype_file --out output_file`

## **Input**

This software requires two input files: a phenotype file and a genotype file. The phenotype file contains information about the case-control status, subject identification number (ID), and covariates. The genotype file contains the SNP genotype information. Both files are plain text files in a matrix-like layout. The name of the phenotype file is specified with the `--pheno` command-line option; the name of the genotype file is specified with the `--geno` command-line option.

### **Phenotype file**

The phenotype file is a plain text file with *n* rows and *m* columns. The rows represent subjects. Each subject contributes as many rows as the number of times he/she appeared in the studies. The columns are separated by one or more white spaces (the space character or the TAB character). The columns have fixed meanings, as described below:

> **Column 1**: Subject ID. This column is required and is alpha-numerical. No missing values are allowed. Each study subject is attached with a unique ID. Any subject who appears in multiple studies must have the same ID for the multiple records.

> **Column 2**: Case-control status. This column is required and indicates by the values 1 versus 0 whether the subject is a case or a control. All values other than 0 and 1 are treated as missing.

> **Column 3  column *m***: Covariates. These columns are optional and contain covariate values. Covariates include study indicators and environmental variables. All covariate values are numerical. Missing values are indicated by -999. All covariates are entered into the model as they are. Any categorical covariate with more than two levels needed to be transformed to appropriate dummy variables by the user.

### **Genotype file**

The genotype file is a plain text file with *s* rows and *n*+1 columns, where *n* is the number of rows of the corresponding phenotype file. The *s* rows represent *s* SNPs with one SNP in each row. The columns are separated by one or more white spaces (the space character or the TAB character). The columns must have the following format:

> **Column 1**: SNP ID. This column is required and is alpha-numerical. No missing values are allowed.

> **Column 2  column (*n*+1)**: Genotype values. The *j*-th column of the *i*-th row pertains to the value of the *i*-th SNP for the (*j*-1)-th subject in the phenotype file. Accepted genotype values are 0, 1, and 2. Missing values are indicated by 9.

## **Output**

This software writes computational results to the output file named by the user with the `--out` command-line option. This software reports the results for all SNPs in the same order as they appear in the genotype file. For each SNP, the output file shows the parameter estimates, standard errors, standard-normal test statistics, and p-values for the SNP effect (labeled by `SNP effect`), as well as the covariate effects (labeled by `Covariate1`, `Covariate2`, …) if there are covariates in the phenotype file.

## **Examples**

### **Cohort data**

The file [cohort.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/cohort.zip), shown below, contains simulated data from a cohort study of 5000 individuals genotyped at five SNPs. The observation time and event indicator are specified in the columns titled Time and Status, respectively. The Smoking column contains environmental covariate data, and the columns SNP1-SNP5 represent the five SNP sites. Missing SNP values are indicated by 9.

+---------------------------------------------------------------------------------------------------------------------------------------+
| [cohort.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/cohort.zip):   Example cohort data file for HAPSTAT input. |
+---------------------------------------------------------------------------------------------------------------------------------------+
|                                                                                                                                       |
+---------------------------------------------------------------------------------------------------------------------------------------+

Select the tab labeled *Frequencies* in the left panel. In the right panel, select *Hardy-Weinberg disequilibrium*, check both the *Cohort* and *Subcohort* samples and click on *Calculate*. Your results will display on the left; see [Figure 4.1](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.1.png).

\<!–[–\>\<!– Figure 4.1](https://dlin.web.unc.edu/software/hapstat/).–\>

Select the tab labeled *Additive effects*. To estimate dominant effects under Hardy-Weinberg disequilibrium, change the *Assumptions* settings by highlighting the *Dominant* model and *Hardy-Weinberg disequilibrium* from the dropdowns. Click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ to activate the *Select effects* dialog. Change *Threshold* to 0.01 and the sample to *Cohort*. Click on *Calculate* to obtain the display in [Figure 4.2](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.2.png).

The results for the cohort data using the options shown in Figures 4.1 and 4.2 are given in [cohort.out](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/cohort.zip).

### **Cross-sectional data**

The file [cross-sectional.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/cross-sectional.zip), shown below, contains simulated data from a cross-sectional study of 5000 individuals genotyped at six SNPs. Approximately 5% of SNP values are missing. The column titled Trait contains disease-related trait data. The columns Age, Gender and Exposure contain environmental data and the columns SNP1-SNP6 represent the six SNP sites. Missing SNP values are denoted by \*.

+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| [cross-sectional.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/cross-sectional.zip):   Example cross-sectional data file for HAPSTAT input. |
+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                                                                                                                                                                  |
+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Click the ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/gene.png)~ icon to create two genes, with SNP1-SNP3 as Gene 1 and SNP4-SNP6 as Gene 2. Select the trait data and the three environmental variables and click *Continue*.

Select the tab labeled *Additive effects* in the left panel. Click the toolbar icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ to activate the *Select effects* dialog and add the interactions 001×101, 001×101×Age, 001×101×Gender and 001×101×Exposure. Click on *Calculate* to obtain the display shown in [Figure 4.3](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.3.png).

Results are provided in the file [cross-sectional.out](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/cross-sectional.zip).

### **Longitudinal data**

The file [longitudinal.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/longitudinal.zip) contains simulated data from a longitudinal study of 1000 individuals with a quantitative trait measured at five regular time points and with five SNPs. The column titled Subject provides the identifier of the individual. The trait is specified in the column titled Weight. The Time covariate specifies the time point at which the measurement was taken. Columns SNP1-SNP5 represent the five SNP sites.

+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| [longitudinal.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/longitudinal.zip):   Example longitudinal data file for HAPSTAT input. |
+---------------------------------------------------------------------------------------------------------------------------------------------------------+
|                                                                                                                                                         |
+---------------------------------------------------------------------------------------------------------------------------------------------------------+

Select the tab labeled *Additive effects* and click on *Calculate* to obtain the result shown in [Figure 4.4](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.4.png). Click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ to activate the *Select effects* dialog and select the tab labeled *Random effects*. Add the Time covariate to the random effects selection as shown in [Figure 4.5](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.5.png). Click on *Calculate* to obtain the display in [Figure 4.6](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.6.png).

Results are provided in the file [longitudinal.out](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/longitudinal.zip).

### **Analysis of untyped SNPs with external trio data**

The file [case-control.2.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip) contains the same data as in [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip) with the exception of SNP3, which we will consider as untyped. Select the menu option *File*»*Open*»*Case-control data file* to open the file [case-control.2.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip). Next, select the menu option *File*»*Open*»*External data file*»*Trio data file* to open the file [trio.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip). Select SNP1-SNP5 as *Gene* variables from [trio.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip) as shown in [Figure 1.4](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-1.4.png).

Click the tab labeled *case-control.2.dat*. Select the column titled Status as the disease status and the columns Age and Gender as environmental variables. Click the ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/gene.png)~ icon twice to create three genes. Select columns SNP1 and SNP2 as *Gene 1* variables. As SNP3 is present in the external file but not in the study file, we type SNP3 in the variable box for *Gene 2*. Select columns SNP4 and SNP5 as *Gene 3* variables. See [Figure 4.7](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.7.png). for illustration. Click *Continue* to proceed.

Click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ to activate the *Select effects* dialog. When external data is present, HAPSTAT will determine frequencies based on all trios or unrelated individuals by default. The default sample may be changed via the dropdown menu adjacent to the *Threshold* box. To exclude external data from analysis, uncheck the box labeled *Use external data*.

In the *Select effects* dialog, remove the environmental effects by clicking on the *Environment* heading followed by the *Remove* button. Remove all effects and interactions for Gene 1 and Gene 3 by clicking on the *Gene 1* and *Gene 3* headings followed by the *Remove* button, respectively. Remove the interactions 0\*Age and 0\*Gender from Gene 2. See [Figure 4.8](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.8.png). Click *OK* on the *Select effects* dialog. Click on *Calculate* to obtain the display in [Figure 4.9](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.9.png). Results are provided in [trio.out](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip).

We can compare the result of the untyped SNP analysis to the typed SNP analysis of the data in [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip). Select the tab *trio.dat* and close the file via the menu option *File*»*Close* or the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/close.png)~ on the toolbar. Select the menu option *File*»*Open*»*Case-control data file* to open the file [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip). Select the column titled Status as the disease status and the columns Age and Gender as environmental variables. Click the ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/gene.png)~ icon twice to create three genes. Select columns SNP1 and SNP2 as *Gene 1* variables, column SNP3 as the *Gene 2* variable and columns SNP4 and SNP5 as *Gene 3* variables. Click *Continue* to proceed. Click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ to activate the *Select effects* dialog and remove effects as in [Figure 4.8](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.8.png). Click *OK* on the *Select effects* dialog followed by *Calculate*. The result is shown in [Figure 4.10](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.10.png).

### **Analysis of untyped SNPs with external data of unrelated individuals**

The file [unrelated.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/unrelated.zip), shown below, contains simulated data for 1000 unrelated individuals genotyped at five SNPs. Select the menu option *File*»*Open*»*External data file*»*Unrelated data file* to open the file [unrelated.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/unrelated.zip). Select the columns SNP1-SNP5 as *Gene* variables. Select the menu option *File*»*Open*»*Case-control data file* to open the file [case-control.2.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/unrelated.zip) and select variables from the file as shown in [Figure 4.7](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.7.png). Click *Continue* to proceed. Click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ to activate the *Select effects* dialog and remove variables from the selection as shown in [Figure 4.8](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.8.png). Click *Calculate* to obtain the result in [Figure 4.11](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-4.11.png). and [unrelated.out](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/unrelated.zip).

+---------------------------------------------------------------------------------------------------------------------------------------------+
| [unrelated.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/unrelated.zip):  External data file of unrelated individuals. |
+---------------------------------------------------------------------------------------------------------------------------------------------+
|                                                                                                                                             |
+---------------------------------------------------------------------------------------------------------------------------------------------+

## **Effects estimation**

HAPSTAT estimates the effects of haplotypes and environmental covariates and haplotype-environment interactions through regression modeling. For quantitative traits, the linear regression model is employed. For binary traits, the logistic regression model is employed, and the regression parameters pertain to the log odds ratios. For age-at-onset data, the Cox proportional hazards model is employed, and the regression parameters pertain to the log hazard ratios. The mode of inheritance can be additive, dominant, recessive or codominant. Under the additive model, having two copies of a causal haplotype has twice the effect on the trait as compared to having a single copy. Under the dominant model, having one or two copies has the same effect. Under the recessive model, only having two copies of the causal haplotype will affect the trait. Under the codominant model, the effect of having two copies can be arbitrarily different from that of having a single copy. In HAPSTAT, the codominant effects are decomposed into additive and recessive components.

### **Navigation**

Estimate haplotype effects by selecting the tab in the left panel labeled *Additive effects*. The options available to the user display in the right panel. The additive genetic model is set by default; changing this setting in the options panel will change the selected tab label accordingly. After you click on *Calculate*, your results will display on the left; see [Figure 3.1](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.1.png)

### **Convergence criteria**

HAPSTAT uses the EM and Newton-Raphson algorithms to estimate haplotype effects. The convergence criteria are the same as those used for the estimation of haplotype frequencies described in the previous section. The maximization is taken over all parameters in the likelihood. The default tolerance is 10^−4^ and the number of iterations is 500.

### **Assumptions**

Select the additive, recessive, dominant or codominant mode of inheritance from the left dropdown. Use the right dropdown to estimate haplotype effects under Hardy-Weinberg equilibrium (default) or disequilibrium. For Hardy-Weinberg disequilibrium, HAPSTAT will return an estimate for the inbreeding coefficient (ρ).

### **Effects**

The box labeled *Effects* is a static display of the main effects and interactions selected for estimation. By default, HAPSTAT selects the haplotype with the highest frequency in the default sample and all covariates, as well as the interactions between them. The selected haplotypes are compared to a reference group, which includes all unselected haplotypes.

### **Select effects**

To change the default selection, click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ on the toolbar to activate the *Select effects* dialog, shown in [Figure 3.2](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.2.png). The panel labeled *Effects* shows the current selection.

The haplotypes whose frequencies are no greater than the value specified by *Threshold* are removed from calculation. The default threshold is given by

max ( 2/n , 0.001 ),

where n is the total sample size. For case-control and cohort studies, frequencies are determined by the sample chosen from the adjacent dropdown. For case-control studies, the control sample is chosen by default; for cohort studies, the subcohort is the default. The default values of the *Select effects* dialog when using external data are discussed in the *External data* section under *Examples*.

The haplotypes above the threshold along with their frequencies are listed in the *Gene* panel. The *Reference* dropdown lists haplotypes whose frequencies are below the threshold along with those haplotypes that are above the threshold but are not selected for effects estimation. Covariates are listed in the *Environment* panel.

To add a main effect, click on the desired variable in the *Gene* or *Environment* list followed by the *Add* button. The selected variable now appears in the *Effects* panel under the heading *Gene* or *Environment*, respectively. To add an interaction, select the appropriate variables from the *Gene* and *Environment* lists and click the *Add* button. You can select multiple variables from the *Environment* list by using the Shift/Ctrl key. To remove a specific effect from the selection, click on that effect on the *Effects* panel followed by the *Remove* button. Clicking on a heading on the *Effects* panel will remove all associated effects.

In [Figure 3.3](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.3.png), we remove the haplotype effect 10011 and the interactions 10011×Age and 10011×Gender by clicking on the *Gene* heading followed by the *Remove* button. Next, we add haplotype effects 01011, 01100 and 11011 and the interactions 01011×Age, 01100×Age, 11011×Age, 01011×Gender, 01100×Gender, 11011×Gender, and 01011×Age×Gender. [Figure 3.4](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.4.png) illustrates the addition of interaction 01011×Age×Gender. The results are shown in [Figure 3.5](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.5.png).

For longitudinal studies, the user can specify both fixed and random effects through the *Select effects* dialog. See the *Longitudinal data* section under *Examples* for further detail.

### **Multiple genes**

Consider the multiple gene selection illustrated in [Figure 1.3](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-1.3.png). Click *Continue* and then click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/select.png)~ to activate the *Select effects* dialog. Frequencies are estimated over all genes and haplotypes with frequencies no greater than the *Threshold* in the joint distribution are excluded from computation. For each gene, haplotypes and their frequencies from the marginal distribution are listed in the corresponding *Gene* panel. In the *Select effects* dialog, select haplotype 100 from Gene A and haplotype 11 from Gene B to add the gene-gene interaction 100×11 to the *Effects* selection. Clicking *Calculate* gives the result in\
[Figure 3.6](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.6.png).

### **SNP Analysis**

HAPSTAT can be used to analyze the effects of individual SNPs by treating each SNP as a separate gene. By using the linkage disequilibrium information of multiple SNPs to infer the missing SNP values, HAPSTAT provides efficient estimation of SNP effects in the presence of missing data. [Figure 3.7](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.7.png) and [Figure 3.8](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.8.png) show the estimation results from two models, one including all the five SNPs and one including only SNP4. In [Figure 3.7](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-3.7.png), the model includes the main effects of SNP1-SNP5 and their interactions with Age and Gender, as well as the interactions between SNP1 and SNP2-SNP5.

### **Summary**

In the left panel, HAPSTAT displays the estimates of regression parameters and their standard errors, together with the Wald statistics and two-sided p-values. The lower panel displays the log-likelihood value(s). You can calculate the likelihood ratio statistic to test a set of parameters by fitting the models with and without the set of parameters of interest.

### **Precision**

You may change the decimal precision of the displayed results via the menu option *Settings*»*Precision* or the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/precision.png)~ on the toolbar. To change the decimal precision for an individual column, right-click on the column header and select *Precision* from the drop-down menu. In the *Precision* dialog box, enter the number of digits to follow the decimal point for fixed notation (default) or the maximum number of significant digits for scientific notation. The default precision is 4.

### **Saving**

Select the menu option *File*»*Save* to save the effects estimates. To save both frequency and effect estimates, select the menu option *File*»*Save All* or click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/saveall.png)~ on the toolbar. The results for the case-control data using the options shown in Figures 3.1-3.8 are given in [case-control.out](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip).

## **Frequency estimation**

### **Navigation**

HAPSTAT estimates the joint haplotype frequencies of all the SNPs included in the analysis. Select the tab labeled *Frequencies* in the left panel; see [Figure 2.1](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-2.1.png). The options available to the user are located in the right panel. After you click on *Calculate*, your results will display on the left.

### **Convergence criteria**

HAPSTAT uses an EM algorithm to estimate haplotype frequencies. The algorithm terminates when the number of EM iterations exceeds the value specified by *Iterations* or when the change in parameter values between successive iterations satisfies the following inequality:

max~k~ \| δ~k,i~ \|   \<   ε ,

where ε denotes the specified value of *Tolerance*,

+--------------+-------------------------------------------------------------------------------+-----------+---+----------------------+
| δ~k,i~   =   | ![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/lbrace.jpg) | θ~k,i~ −\ |   | if   \| θ~k,i-1~ \|\ |
|              |                                                                               | θ~k,i-1~  |   |   \<   0.01          |
+--------------+-------------------------------------------------------------------------------+-----------+---+----------------------+
| θ~k,i~ −\    | otherwise                                                                     |           |   |                      |
| θ~k,i-1~     |                                                                               |           |   |                      |
+--------------+-------------------------------------------------------------------------------+-----------+---+----------------------+
| θ~k,i-1~     |                                                                               |           |   |                      |
+--------------+-------------------------------------------------------------------------------+-----------+---+----------------------+

and θ~k,i~ is the estimate of parameter k at iteration i. By default, ε = 10^−6^ and the number of iterations is 2000.

### **Assumptions**

Use the dropdown to estimate frequencies assuming the population is in Hardy-Weinberg equilibrium (default) or disequilibrium. For Hardy-Weinberg disequilibrium, HAPSTAT returns an estimate for the inbreeding coefficient (ρ).

### **Samples**

For cross-sectional and longitudinal studies, HAPSTAT will automatically estimate frequencies based on all individuals. For a case-control study, choose to estimate haplotype frequencies of the combined case-control sample or consider cases and controls separately. The default is the control sample. For a cohort study, check *Cohort* to estimate haplotype frequencies based on all genotyped cohort members. Under case-cohort or nested case-control designs, the genotyped individuals are not representative of the entire cohort. Thus HAPSTAT also estimates haplotype frequencies based on all genotyped controls and a random sample of cases such that the proportion of cases used for estimation is the same as the proportion of controls that are genotyped. This option is referred to as *Subcohort*.

When incorporating external data, additional options are available. The option to estimate frequencies based on all families or unrelated individuals is referred to as *Trio* or *Unrelated*, respectively. You may also choose to estimate haplotype frequencies of the samples available for a particular study in combination with the external data. Multiple selections are permitted. The HAPSTAT frequency panel when including external file [trio.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip) is shown in [Figure 2.2](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-2.2.png).

### **Summary**

The results of the frequency estimation are summarized in the lower panel of the HAPSTAT display. In the rare event that the computation fails, an error status message is shown. It may then be necessary to increase the maximum iterations or decrease the error tolerance.

### **Sorting**

Right click on the header of the column you wish to sort by and select *Sort ascending* or *Sort descending*. All columns are sorted accordingly.

### **Filtering**

To display frequencies above a certain threshold, right click on the column header and select *Filter*. In the dialog box, specify the desired threshold and frequency sample. Select *Show all* to disable the filter.

### **Precision**

You may change the decimal precision of the displayed frequency values via the menu option *Settings*»*Precision* or the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/precision.png)~ on the toolbar. In the *Precision* dialog box, enter the number of digits to follow the decimal point for fixed notation (default) or the maximum number of significant digits for scientific notation. The default precision is 4.

### **Saving**

To save frequency estimates, select the menu option *File*»*Save* or click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/save.png)~ on the toolbar. Navigate to the desired directory and enter a file name or choose an existing one. Overwrite and append options are supported for existing files. Selecting the menu option *File*»*Save All* or the toolbar icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/saveall.png)~ will save results of all open tabs. HAPSTAT result files are in text format and open with common word processing software.

## **Input data**

HAPSTAT supports data from cross-sectional, longitudinal, case-control, and cohort (including case-cohort and nested case-control) association studies. The cross-sectional and longitudinal designs collect data on a random sample of individuals. In a cross-sectional study, the response variable is measured only once on all study subjects; in a longitudinal study, the response variable is measured repeatedly through time. In the case-control design, data is collected on a sample of diseased individuals or cases and a sample of disease-free individuals or controls. The cohort design follows a sample of at-risk individuals over time and records their times of disease occurrence. The individuals who are withdrawn prematurely or who are disease-free at the end of the cohort study have censored observations, in that their ages at onset are only known to be beyond their durations of follow-up. HAPSTAT also supports the inclusion of external genotype data collected on family trios or unrelated individuals, allowing for analysis on untyped SNPs.

### **File format**

HAPSTAT accepts ANSI-encoded text files containing data in a tabular (row-column) format. Each row contains space or tab delimited data specific to an individual. Column titles may be specified in the first line of the file and must also be space or tab delimited. If using external data, column titles must be specified in both the study file and the external file. File may contain columns of extraneous data. There are no requirements on the ordering of the columns.

The study file must contain one or more columns representing the multi-SNP genotype. Optionally, the file may include one or more columns of environmental covariates. Study-dependent data requirements are as follows:

**Cross-sectional**

:   The file must contain one column describing the trait value of the individual.

**Longitudinal**

:   File data must be tab delimited. The file must contain two columns of data per individual providing an identifier unique to that individual and the observed trait value. For each individual, each observation is recorded on a separate row. At least some individuals have more than one observation. Data that is constant over all observations, such as the multi-SNP genotype, need only be specified for one observation. An identifier must be specified for each row of observed data. There are no requirements on the ordering of the rows.

**Case-control**

:   The file must contain one column describing the disease status of the individual.

**Cohort**

:   The file must contain two columns of data per individual providing the observation time and event indicator.

The external file contains data collected on either trios or unrelated individuals. The file must contain one or more columns representing each of the SNP sites intended for analysis in the study file and all untyped SNPs of interest. For trio data, HAPSTAT requires three rows of data per family, where data for mothers and fathers is in the first two rows and the child’s data is in the third. The correspondence between SNP sites in the study data and external data is determined by the column title. For both the study file and the external file, column titles must be specified in the first row of the file and the corresponding SNP sites must be titled the same in both files.

### **Data specification**

The multi-SNP genotype is represented by a sequence of the values 0, 1 and 2, corresponding to the number of occurrences of a specific allele at each SNP site. Any value other than 0, 1 or 2 is assumed to indicate missing SNP data. Individuals are allowed to have missing data at all SNP sites. Environmental covariates are represented by decimal values and may not contain missing values. The representation of data not intended for analysis is unimportant.

In cross-sectional studies, disease-related traits are represented by decimal values. In longitudinal studies, the identifier is represented as a string value and disease-related traits are represented by decimal values. HAPSTAT allows both quantitative and binary traits in cross-sectional studies and only quantitative traits in longitudinal studies. In case-control studies, the disease status is specified by 1 for cases or 0 for controls. In cohort studies, decimal values represent the observation times and a binary event indicator distinguishes between uncensored and censored individuals by the values 1 and 0, respectively.

The file [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip), shown below, contains simulated data for a case-control study of 2000 individuals genotyped at five SNPs, where some SNP values are missing.

|                                                                                                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip):  Format of case-control data for HAPSTAT input. |
|                                                                                                                                                     |

The disease status is specified in the first column, titled Status. The columns Age and Gender contain environmental covariate data, and the columns SNP1-SNP5 represent the five SNP sites. The · character indicates a missing SNP value.

For external data, the sequence of values representing the genotype must have the same allele correspondence as in the study data. The file [trio.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip), shown below, contains simulated data for 50 families genotyped at five SNPs. Columns SNP1-SNP5 correspond to the five identically titled SNP sites in [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip).

|                                                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------|
| [trio.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip):  External data file of family trios. |
|                                                                                                                                  |

### **Study data import**

To open a study file in HAPSTAT, select the menu option *File*»*Open* and choose the study type corresponding to your data from the submenu. Browse to the directory where your data file resides, select your file and click the *Open* button. The HAPSTAT display after importing [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip) is shown in [Figure 1.1](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-1.1.png)

You may only have one file open in HAPSTAT at any time. To open a new file, select the menu option *File*»*Open* or click the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/open.png)~ on the toolbar. HAPSTAT will prompt you to save your results before closing the current file. You may also close a file via the menu option *File*»*Close* or the icon ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/close.png)~ on the toolbar.

### **Transpose**

Use the *Settings*»*Transpose* menu option to transpose rows and columns.

### **Variable selection**

To specify the columns that correspond to the variables HAPSTAT should use for analysis, first click inside the text area of the variable you wish to set in the *Variables* box on the right panel. Then select the columns of data corresponding to that variable by clicking on the column labels on the left panel. Use the toolbar icons ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/show.png)~ and ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/hide.png)~ to show or hide unselected columns. The selection of variables for the single-gene analysis of [case-control.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip) is shown in [Figure 1.2](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-1.2.png). After completing your selection, click *Continue* to proceed.

### **Multiple genes**

Click the ~![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/gene.png)~ icon on the toolbar to create multiple genes. [Figure 1.3](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-1.3.png) shows the choices of SNP1-SNP3 and SNP4-SNP5 as Gene 1 and Gene 2, respectively.

### **Header data**

HAPSTAT will attempt to detect if the first line of your file contains column titles or actual data. You can toggle what HAPSTAT decides by checking/unchecking the menu option *Settings*»*Include header*.

### **Edit/clear selection**

To change your variable selections after the *Continue* button is clicked, return to the file tab and click the *Edit* button. The *Settings*»*Clear* menu option will clear the current selection.

### **Sorting**

Right click on the title of the column you wish to sort by and select *Sort ascending* or *Sort descending*. All columns are sorted accordingly.

### **Excluding rows**

All rows are included by default. To exclude a particular row from your analysis, right click on the row number and select *Exclude*.

### **External data import**

You may import external data at any time. To open an external file, select the menu option *File*»*Open*»*External data file* and choose the external type corresponding to your data from the submenu. Browse to the directory where your data file resides, select your file and click the *Open* button. The HAPSTAT display after importing [trio.dat](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/case-control.zip) is shown in [Figure 1.4](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/figure-1.4.png).

If a study file is already open in HAPSTAT, all gene variables selected from the study file will be pre-selected from the external file (if present). You may add or remove SNP variables from the gene selection as described above. SNPs selected from the study file must be a subset of those selected from the external file. SNPs selected from the external file that are not selected or not present in the study file are considered to be untyped.

## **Download**

### **Windows**

The HAPSTAT software interface is provided as a self-contained Windows executable. HAPSTAT should run on 32-bit X86 systems operating under Windows XP/2000/NT/98. The required system memory is dependent on the input data; we recommend 512MB or higher.

To use HAPSTAT, download hapstat-3.0.zip to your computer, extract the ZIP archive to the desired location and run the executable file HAPSTAT-3.0.exe.

Current release » updated 06/25/2008 » [**hapstat-3.0.zip**](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/hapstat-3.0.zip)

Previous versions of the software are available for download below. The ZIP archives include the HAPSTAT executable, documentation and example files.

HAPSTAT 2.0 » released 02/29/2008 » [**hapstat-2.0.zip**](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/hapstat-2.0.zip)\
HAPSTAT 1.0 » released 03/09/2007 » [**hapstat-1.0.zip**](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/hapstat-1.0.zip)

### **Linux**

We provide a command-line version of HAPSTAT for Linux. It automates the analysis of multiple data sets for case-control studies. The majority of options available in the HAPSTAT 2.0 software interface are supported. Download hapstat-3.0.linux.tar.gz to your computer and extract the gzipped tarfile to the desired location. Documentation and example files are included.

Current release » updated 10/14/2008 » [**hapstat-3.0-linux.zip**](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/hapstat-3.0-linux.zip)

Previous versions of the software are available for download below.

hapstat 2.0 » released 10/11/2007 » [**hapstat-2.0-linux.zip**](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/hapstat-2.0-linux.zip)

## **Support**

Your comments are welcome! If you encounter problems using HAPSTAT, have questions or suggestions for improvement, please contact us at ![](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/linsoft_email.png "linsoft at bios dot unc dot edu"){alt=""}.

## **Reference**

Lin DY, Hu Y, Huang BE (2008). [Simple and efficient analysis of disease association with missing genotype data.](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/LinHuHuang08.pdf) [*The American Journal of Human Genetics*](https://www.cell.com/ajhg/home), 82:444-452.

Zeng D, Lin DY, Avery CL, North KE, Bray MS (2006). [Efficient semiparametric estimation of haplotype-disease associations in case-cohort and nested case-control studies](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/ZengEA06.pdf). [*Biostatistics*](http://biostatistics.oxfordjournals.org/), 7(3):486-502.

Lin DY and Zeng D (2006). [Likelihood-based inference on haplotype effects in genetic association studies](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/LinZeng06.pdf). [*Journal of the American Statistical Association*](http://www.amstat.org/publications/jasa), 101:89-104.

Lin DY, Zeng D, Millikan R (2005). [Maximum likelihood estimation of haplotype effects and haplotype-environment interactions in association studies](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/LinZengMillikan05.pdf). [*Genetic Epidemiology*](https://onlinelibrary.wiley.com/journal/10982272), 29:299-312.

## **Disclaimer**

The HAPSTAT software and related files are distributed free of charge and without warranty of any kind. The author provides no guarantee as to the suitability or functioning of this software or to the results obtained from its use, nor does the author provide any guarantee as to the correctness, completeness or quality of the information contained within this site.

## **Copyright**

Copyright (c) 2006-2008 Tammy Bailey, Danyu Lin and the University of North Carolina at Chapel Hill, Department of Biostatistics, 3101 McGavran-Greenberg CB#7420, Chapel Hill, North Carolina 27599-7420 USA. All rights reserved.
