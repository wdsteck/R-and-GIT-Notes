# Git-References
Listing of sources of information for living and thriving in the Git Environment

## Git and Github
_Git_ is software that runs on your local computer that lets you manage the configurations of your files using standard practices.

_Github_ is a web service that lets you create repositories of your files for web storage and for sharing.

Whereas you do not need to use both tools, they are most often used together to provide a powerful environment for multi-user, change management.

## Git Resources

* [Pro Git book](https://git-scm.com/book/en/v2)
* [Git Reference](gitref.org)
* [Data Science School Blog](http://www.dataschool.io/tag/git/)
* [Git Guides](https://guides.github.com/)
* [Git SCM Help](https://git-scm.com/about)
* [Introduction to Git and GitHub on YouTube](https://youtu.be/h1e8oC7g0Ps?list=PL5-da3qGB5IBLMp7LtN8Nc3Efd4hJq0kD)
* [BioConductor Web Site](http://www.bioconductor.org) - Open source software for bioinformatics.

## Github Notes
* [Github Help](https://help.github.com/)
* [Create a gh_pages branch for viewing HTML in a repo](https://github.com/lgreski/datasciencectacontent/blob/master/markdown/pml-ghPagesSetup.md)
* [Github Pages](https://pages.github.com/)

## Markdown Resources

* [Markdown Tutorials](http://www.markdowntutorial.com/)
* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [What is Markdown?](http://whatismarkdown.com/)
* [Markdown Official Documentation](http://daringfireball.net/projects/markdown/basics)
* [Markdown by RStudio](http://rmarkdown.rstudio.com)
* [Equations in Markdown](http://www.introductoryr.co.uk/Reproducibility/Chap_6_Maths.html)

The Rmd to md to html workflow can be accomplished with the following:
```
library(knitr)
library(markdown)

#transform the .Rmd to a markdown (.md) file.
knit('r-knitr-markdown.Rmd')

#transform the .md to HTML format
markdownToHTML("r-knitr-markdown.md", "r-knitr-markdown.html",fragment.only = TRUE)
```

The `fragment.only = TRUE`
argument tells the HTML generator to not generated a complete HTML file, only
generate HTML code to represent what is in the md code.

## R Programming Resources

* [Data Science Bootcamp](https://www.datacamp.com) is a good source of R tutorials.
* [Vanderbuilt University Biostat Department R Information Page](http://biostat.mc.vanderbilt.edu/wiki/Main/RS)
* [R Data Merging Page](http://www.statmethods.net/management/merging.html)
* [Working with Dates](http://www.r-statistics.com/2012/03/do-more-with-dates-and-times-in-r-with-lubridate-1-1-0/)
* [R Cookbook](http://www.cookbook-r.com)
* [R Tutorials](http://www.r-bloggers.com/how-to-learn-r-2/)
* [RPubs](http://rpubs.com/thoughtfulbloke/subset) tutorial on subsetting vectors.
* [`ggplot2` Tutorial](http://tutorials.iq.harvard.edu/R/Rgraphics/Rgraphics.html)

###Useful Packages
  In general, there is probably an R package for whatever data storage mechanism we could run into. The best way to find the package and information on how to use the package is to Google "<data storage mechanism> R package".

####Common Connections:
  * file - open a connection to a file on the local computer
  * url - open a connection to a url
  * gzfile - open a connection to a .gz file
  * bzfile - open a connection to a .bz2 file
  * _?connections_ for more information
  * **Remember** to close all connections when finished with them

  Some useful packages:
  ```
  install.packages("ggplot2")
  install.packages("gridExtra")
  
  require("ggplot2")
  require("gridExtra")
  ```
  
  `require()` and `library()` do the same thing, except `require()` returns a bool to indicate if the package is loaded whereas `library()` stops on an exception. `require()` is useful in code as in this example:

For if you need a package in a piece of code, make sure it is installed and loaded:
  ```
  if(require("lme4")){
    print("lme4 is loaded correctly")
  } else {
    print("trying to install lme4")
    install.packages("lme4")
    if(require(lme4)){
      print("lme4 installed and loaded")
    } else {
      stop("could not install lme4")
    }
  }
  ```
### XML Information
  [XML Presentation](http://www.stat.berkeley.edu/~statcur/Workshop2/Presentations/XML.pdf) is a good tutorial on extracting data out of XML in R.
  ```
  install.packages("XML")
  require("XML")
  ```

### JSON Information
  * [R-Bloggers](http://www.r-bloggers.com/new-package-jsonlite-a-smarter-json-encoderdecoder/) - A good jsonlite tutorial.
  * [CRAN](https://cran.r-project.org/web/packages/jsonlite/vignettes/json-aaquickstart.html) - Quick start guide from CRAN

  ```
  require("jsonlite")
  install.packages("jsonlite")
  ```

### tidyr Package Information
  * [Tidy Data](http://vita.had.co.nz/papers/tidy-data.pdf)

  ```
  install.packages("plyr")
  install.packages("dplyr")
  install.packages("tidyr")

  require("plyr")
  require("dplyr")
  require("tidyr")
  ```

  * [Split-Apply-Combine tutorial](http://www.r-bloggers.com/a-quick-primer-on-split-apply-combine-problems/)
  * [plyr tutorial](http://plyr.had.co.nz/09-user/) - Hadley Wickham plyr tutorial
  * [reshape tutorial](http://www.slideshare.net/jeffreybreen/reshaping-data-in-r)

###[MySQL Notes](https://github.com/wdsteck/R-and-GIT-Notes/blob/master/mysqlnotes.md)

###[Swirl Notes](https://github.com/wdsteck/R-and-GIT-Notes/blob/master/swirlnotes.md)

###[HDF5 Notes](https://github.com/wdsteck/R-and-GIT-Notes/blob/master/hdf5notes.md)

###Reading Data from the Web - Web Scraping
  Read lines directly from the site. It comes unformatted and is not very easy to parse:
  ```
  url_site = "https://scholar.google.com/citations?user=HI-I6C0AAAAJ&hl=en"
  con = url(url_site)
  htmlCode = readLines(con)
  close(con)
  htmlCode
  ```
  This can be ugly since it comes unformatted. Reading it with XML may be better:
  ```
  library(XML)
  url = "https://scholar.google.com/citations?user=HI-I6C0AAAAJ&hl=en"
  html <- htmlTreeParse(url, useInternalNodes=T)
  xpathSApply(html, "//title", xmlValue)
  xpathSApply(html, "//df[@id='col-citedby']", xmlValue)
  ```
  This did not work for me. It could not recognize the url as XML. Another way
  to do it is to use the `httr` package.

  * [CRAN HTTR Package](http://cran.r-project.org/web/packages/httr/httr.pdf)
  * [R-Bloggers](http://www.r-bloggers.com/?s=Web+Scraping) - Search R-Bloggers
  for a lot of examples of Web Scraping

  ```
  library(httr)
  html2 = GET(url)
  content2 = content(html2, as = "text")
  parsedHtml = htmlParse(content2, asText = T)
  xpathSApply(parsedHtml, "//title", xmlValue)
  ```
  Some sites require authentication. With HTTR, this can be handled:
  ```
  handle = GET("http://httpbin.org/basic-auth/user/passwd", authenticate("user", "passwd"))
  handle
  names(handle)
  ```
  Using handles preserves the authentication so that subsequent gets
  do not have to be authenticated. Cookies will retain the credentials.

###Caret Package

Caret tutorials:  
[UCLM Tutorial](http://www.edii.uclm.es/~useR-2013/Tutorials/kuhn/user_caret_2up.pdf)  
[R-Project Tutorial](http://cran.r-project.org/web/packages/caret/vignettes/caret.pdf)  

A paper introducing the caret package  
[iStat Software Caret Intro](http://www.jstatsoft.org/v28/i05/paper)
