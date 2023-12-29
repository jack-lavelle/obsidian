This ticket is slightly more complicated than previous and may involve sub-tasks. Motivated by developments in research of Python NLP libraries for the purpose of this project, this ticket is to implement them and overhaul the report generation in the process.

### Preliminary Design
#### Report Design
The library used for report generation has been changed and is now [python-docx](https://python-docx.readthedocs.io/en/latest/). Instead of the report being a `.pdf`, it will now be a word document so that it can be more easily modified.

The new report will have the following look:

```
Objective 1
	Category of Gene
		* Set of Advice
		(gene)
		* Set of Advice
		(gene)
	Category of Gene
		* Set of Advice
		(gene)
Objective 2
	Category of Gene
		* Set of Advice
		(gene)
		* Set of Advice
		(gene)
	Category of Gene
		* Set of Advice
		(gene)
....
```

- [ ] #nutrition-genome How compatible is *Significance* with the *Advice* section? For example, if a significance is "Increased Anxiety" then will advice geared towards lessening stress *necessarily* be included?
	Assume the answer is *yes*.

Here is brainstorming of the data format to generate the report.
```
{
    "Objective 1" : {
        "Category 1" : [
            "Gene 1", <-- call get_gene_info(...) here
            "Gene 2"
        ],
        "Category 2" : [
            "Gene 1",
            "Gene 2"
        ]
    },
    "Objective 2" : {
        "Category 1" : [
            "Gene 1", 
            "Gene 2",
            "Gene 3"
        ]
    }
}
```

#### UI Design
The report generation process will now allow the user to select which genes to automatically include in the report. It will have the following interface:

![[Pasted image 20231112150559.png]]
The *Select Specific Gene* will contain the next 10 genes from the similarity report and then allow for custom search of gene.

### Implementation Log

*This serves as a working log to catalog what it was I was thinking / things I felt I needed to write down at certain parts of implementation.*

#### Implementation of `Report.generate(...)`

Unfortunately I did not log during the refactoring of `Patient` or the creation of `Report`. I will move on. 

Currently I am at a standstill since I need a working set of data in order to generate a report ... which I currently do not have. Therefore, I will overhaul the UI process that selects the genes through a combination of manual and automatic gene selection.

##### Gene Selection UI Design

Current Patient View
![[Pasted image 20231119210927.png]]

- [ ] Needs their objectives readily available / editable. #nutrition-genome #add-tags

Upon pressing `Create Report`:
```
Objective 1
    Automatic Gene Selection
        | Gene Name | Significance | Similarity |
        | Gene Name | Significance | Similarity |
    Manual Gene Selection
        | Select Genes |
        (* then list them here *)

Objective 2
    Automatic Gene Selection
        | Gene Name | Significance | Similarity |
        | Gene Name | Significance | Similarity |
    Manual Gene Selection
        | Select Genes |
        (* then list them here *)

Objective 3
    Automatic Gene Selection
        | Gene Name | Significance | Similarity |
        | Gene Name | Significance | Similarity |
    Manual Gene Selection
        | Select Genes |
        (* then list them here *)
```

![[Pasted image 20231119211544.png]]
##### Gene Selection UI Implementation

*November 22nd, 2023*
The end goal for this part is to provide a set of genes that have been selected through the means of automatic and manual methods. This will form the basis for `Report.generate(...)`.

*November 24th, 2023*
- [ ] #nutrition-genome #refactoring`application.py` shouldn't contain any implementation of `Windows`, instead I should follow the example set by `ReportGeneSelectionWindow` where the window class contains the implementation.
- [ ] #nutrition-genome You should be able to click the gene name which does the equivalent of a `get_gene_info()` call.


This page is being deprecated since it is in an old / confusing / unscalable format.