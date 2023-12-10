*The following work was done November 11th, 2023. As the title suggests, the main goal of this ticket is to introduce [[Natural Language Processing]] to the project.*
### Design
Suppose a patient has the following objectives:

1) Lose weight,
2) Sleep better, and
3) Lift more weight.

This program will loop through each of the *significances* from the genes, rank the similarity between each objective, determine which are relevant (probably by a similarity percent cutoff point), and then keep only those.

#### Text Similarity

First, establish which genes' *significance* are relevant, then the rest is data representation ... therefore focus on text similarity first then the document generation after.

```json
{
    "Objective 1" :
        "Gene Category 1" : [
            "gene1",
            "gene2"
        ],
        "Gene Category 2"
}       ...
```

```json
{
    "Objective 1" : {
        "Gene 1" : {"Percent Similiarity", "Significance", "Category"},
        ... ,
        "Gene 10" : {"Percent Similiarity", "Significance", "Category"}
    },
    "Objective 2" : {
        "Gene 1" : {"Percent Similiarity", "Significance", "Category"},
        ... ,
        "Gene 10" : {"Percent Similiarity", "Significance", "Category"}
    }
}
```


https://stackoverflow.com/questions/65852710/text-similarity-using-word2vec

https://stackoverflow.com/questions/1035183/how-can-i-create-a-word-document-using-python

https://github.com/python-openxml/python-docx

https://python-docx.readthedocs.io/en/latest/

#### Bottomline
There are quite a few Python libraries to use and each have a few models at their disposal. [See this Stack Overflow post for a few more libraries.](https://stackoverflow.com/questions/65199011/is-there-a-way-to-check-similarity-between-two-full-sentences-in-python)

Ultimately, the one I will be going with is the one from [*Gensim*](https://pypi.org/project/gensim/).

However, it does not work perfectly so I will make the document generation process more customizable.