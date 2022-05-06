# Bibliometric-Analysis
Please use this for the bibliometric analysis workshop
There are 3 bibtext files. These are exported from the Scopus database. The 3 txt files are exported from the Web of Science database. Here's the code for this :

```
library(bibliometrix)
library(xlsx)
library(bibliometrixData)

#Combining bibtex files
big_bibtex <- c(readLines("kmone.bib"), "\n", readLines("kmtwo.bib"), "\n", readLines("kmthree.bib"))
writeLines(big_bibtex, "big_bibtex.bib")

##Importing Scopus Dataset
scopus_data <- convert2df("big_bibtex.bib", dbsource="scopus", format = "bibtex")

#Combining txt files
big_txt <- c(readLines("kmone.txt"), "\n", readLines("kmtwo.txt"), "\n", readLines("kmthree.txt"))
writeLines(big_txt,"big_txt.txt")

##Importing Web of Science Dataset
web_data <- convert2df("big_txt.txt")

##Combining both datasets
combined_final <- mergeDbSources(web_data, scopus_data, remove.duplicated = T)

##Exporting Files
write.xlsx(combined_final, "combined_final.xlsx")
biblioshiny()
```
