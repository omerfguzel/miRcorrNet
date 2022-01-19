## miRcorrNet
miRcorrNet is a novel tool that performs machine learning-based integration to analyse miRNA and mRNA gene expression profiles. This tool groups mRNAs based on their correlation to miRNA expression levels and hence it generates groups of target genes associated with each miRNA. Then, these groups are subject to a rank function for classification [1]. In this repository, the pre-processed data is supplied with several different types of cancers. This data is downloaded and pre-processed from downloaded from The Cancer Genome Atlas (TCGA). The flow diagram of workflow is like this:
 ![alt text](https://github.com/omerfguzel/miRcorrNet/blob/main/Data%20Graphics/ReadMe/miRcorrNet_v2.jpg)
The KNIME implementation of workflow above looks like this: 
 ![alt text](https://github.com/omerfguzel/miRcorrNet/blob/main/Data%20Graphics/ReadMe/miRcorrNet_v11.png)
## mRNA and miRNA Data Types
The image below shows one of the mRNA data. It is a .table file which contains samples in the rows and gene names in the columns, class column represents if the sample is control or case.
 ![alt text](https://github.com/omerfguzel/miRcorrNet/blob/main/Data%20Graphics/ReadMe/mRNA_Data.jfif)
The image below shows one of the miRNA data. It is also a .table file which contains samples in the rows and gene names in the columns, class column represents if the sample is control or case. 
 ![alt text](https://github.com/omerfguzel/miRcorrNet/blob/main/Data%20Graphics/ReadMe/miRNA_Data.jfif)
 
## Setting Up the Environment
These workflows are implemented on KNIME. It can be downloaded and simply installed from ***[here](https://www.knime.com/downloads)***. There is also R/RStudio in computer which is used for implementation. Rserve package of RStudio is a major dependency for this tool so it should be installed as well. If there is any problem caused by dependency or lack of package, it can be obtained from RStudio website. For example, if there is an error with message “ranked_miRNA_RobustRankaggreg”, this means a package is lacked and this package is available in ***[here](https://cran.r-project.org/web/packages/RobustRankAggreg/index.html)***.

## KNIME Implementation
Before executing any node, there are some settings to be done in KNIME software. The Python version in your computer and the version in the workflow must be compatible (Python2 or Python3). This workflow uses Python2, but the majority of Python users work with Python3. Python environment with desirable version can be created easily with following:
- ***File -> Preferences -> KNIME(left side of the pop-up) -> Python***\
In this window, there are several options but the option selected should also selected in the workflow’s Python based nodes. The nodes **0:460:459:458:456** and **0:459:458:456** are Python related nodes. If you change Python version from 2 to 3, you must also change the Python version in these nodes with following after double-clicking node:
- ***Executable Selection -> Python2/Python3 -> Apply***\
In RStudio, these commands should be called before execution to activate R server:
- *library(Rserve);*
- *Rserve(args = "--vanilla")*

After setting Python version and activating R server, there is a final operation before executing workflow which is setting parameters. In this workflow, parameters like **Negative Correlation Value, Positive Correlation Value** and **Number of Iterations** are changeable by user. They are set -0.6, +1.0 and 100 as default. These parameters basically can be changed from **SetParamers(0:471)** node.

Finally, in the first node which is List Files(0:223) the data is selected by browsing the folder that includes both mRNA and miRNA data with .table extensions.

Then the workflow is executed by pressing double play button or via Shift+F7. After execution is done, output files is generated in the folder where the original data is placed with comparison results.
