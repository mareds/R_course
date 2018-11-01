---
title       : Data Analysis with R
subtitle    : 11 - R Markdown for communication
author      : Saskia A. Otto
job         : Postdoctoral Researcher
framework   : io2012        
highlighter : highlight.js 
hitheme     : sao_theme     
widgets     : [mathjax, quiz, bootstrap, interactive] 
mode        : selfcontained 
knit        : slidify::knit2slides
logo        : uham_logo.png
biglogo     : BigLogo_MDS.png
assets      : {assets: ../../assets}
--- &slide_no_footer .segue bg:#1874CD





# R Markdown
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

--- 
## How to go from R to any output format for sharing your results?

<div class="img-with-text" style="position: absolute; left: 325px; top: 150px">
    <img src="img/Rmarkdown_output_formats.png" alt="" height=500px/>
 <p><span class="source-img" style = "float:right">source: 
    <a href='https://rmarkdown.rstudio.com/authoring_quick_tour.html' title=''>rmarkdown.rstudio.com</a></span></p>
</div>

---
## By using R Markdown

<img src="img/Logo_rmarkdown.png" style="height:75px;border:0;position: absolute; left: 400px; top: 25px" </img> 

- R Markdown is an easy-to-write **plain text formatter** designed to make web content, reports or presentations easy to create,
- can **weave** the outputs of your R code, like **figures and tables**, with **text** to create a report,
- supports not only the **reproducibility** of your analysis but also the **entire report**,
- supports various different **static** as well as **dynamic output formats**.
- How does it work? R Markdown encapsulates various processs into a single render function:

<div class="img-with-text" style="position: absolute; left: 250px; top: 420px">
    <img src="img/Rmarkdown_flow_mod.png" alt="" width=600px/>
 <p><span class="source-img" style = "float:right">modified from the <a href='https://github.com/rstudio/cheatsheets/raw/master/rmarkdown-2.0.pdf' title=''>R Markdown</a> cheat sheet (under CC-BY-SA license)</span></p>
</div>


---
## A quick introduction

<iframe src="https://player.vimeo.com/video/178485416" width="640" height="360" frameborder="0" style="margin-bottom: 2em;" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen="">
</iframe>

<p><span class="source-img" style="position: absolute; left: 400px; top: 650px">source:
    <a href='https://rmarkdown.rstudio.com/authoring_quick_tour.html' title='R Markdown video'>rmarkdown.rstudio.com</a> (RStudio is a trademark of Rstudio, Inc.)</span></p>

   
--- &vcenter
## How to create an .Rmd file

<img src="img/Rmarkdown_step_1.png" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" width="800px" style="display: block; margin: auto;" />

--- &vcenter
## How to create an .Rmd file

<img src="img/Rmarkdown_step_2.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" width="500px" style="display: block; margin: auto;" />

--- &vcenter
## Structure of an .Rmd file

<img src="img/Rmarkdown_step_3.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" width="700px" style="display: block; margin: auto;" />

--- &vcenter
## Structure of an .Rmd file

<img src="img/Rmarkdown_step_4.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" width="800px" style="display: block; margin: auto;" />

--- &vcenter
## Rendering Output

<img src="img/Rmarkdown_step_5.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" width="800px" style="display: block; margin: auto;" />

---
## (Markdown) Syntax

<div class="img-with-text" style="position: absolute; left: 200px; top: 125px">
    <img src="img/Rmarkdown_syntax_1.png" alt="" width=700px/>
 <p><span class="source-img" style = "float:right">source: 
    <a href='https://rmarkdown.rstudio.com/authoring_quick_tour.html' title=''>rmarkdown.rstudio.com</a></span></p>
</div>

---
## HTML vs Markdown vs R Markdown Syntax

<div class="img-with-text" style="position: absolute; left: 200px; top: 150px">
    <img src="img/Rmarkdown_syntax_2.png" alt="" width=700px/>
 <p><span class="source-img" style = "float:right; line-height:1.5">source: Donovan, T., Brown, M., & Katz, J. (2015). Vermont Cooperative Fish and Wildlife Research Unit R Projects: R for Fledglings.<br>Retrieved from  
    <a href='https://www.uvm.edu/rsenr/vtcfwru/R/fledglings/08_Markdown.html' title=''>https://www.uvm.edu/rsenr/vtcfwru/R/fledglings/08_Markdown.html</a><br>(under <a href='https://creativecommons.org/licenses/by-nc-nd/4.0/' title=''>CC-BY-NC-ND 4.0</a> license) </span></p>
</div>



--- &twocol
## Get more infos

<img src="img/Cartoon_info.png" style="height:100px;border:0;position: absolute; left: 375px; top: 25px" </img> 

*** =left
- The [cheatsheet](https://github.com/rstudio/cheatsheets/raw/master/rmarkdown-2.0.pdf) gives you a good overview.
- R Studio provides also a useful [reference guide](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf).
- Look at the [R Markdown Webside](https://rmarkdown.rstudio.com) from R Studio for a first start.
- To dig deeper you will find many youtube videos and online tutorials.
  - A good one is, for instance: [R for fledglings](https://www.uvm.edu/rsenr/vtcfwru/R/fledglings/08_Markdown.html)

<img src="img/Rmarkdown_cheatsheet_1.png" style="width:350px;border:0;position: absolute; left: 650px; top: 50px" </img> 

<div class="img-with-text" style="position: absolute; left: 650px; top: 330px">
    <img src="img/Rmarkdown_cheatsheet_2.png" alt="" width=350px/>
 <p><span class="source-img" style = "float:left; line-height:1.5"> Cheat sheet is freely available at <br>
 <a href='https://www.rstudio.com/resources/cheatsheets/' title=''>https://www.rstudio.com/resources/cheatsheets/</a></span></p>
</div>


--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- &exercise
# Task: Convert an R script into a Markdown file 

Start your first R Markdown file that should render a html document and save it under any name.
In lecture 8 on visualizations you were asked to answer the following questions using the `hydro` dataset (file "data/1111473b.csv"):

1. What happens if you make a scatterplot of station (x) vs temp (y)? Why is the plot not useful? What would be a better plot?
2. What happens if you make a boxplot of cruise (x) vs psal (y)? Why is this plot less suitable? What could be an alternative?

If you have done this exercise you can simply use your code and copy and paste it into the code chunks of your .Rmd file. If you haven't done the exercise you have now the opportunity to make up leeway.


--- &exercise
# Implement the following in your .Rmd file

1. Start with R code chunks for loading the data and required libraries 
2. Add code chunks for 
    i) any data modifications
    ii) any plot
3. Think about which code chunks should be evaluated (eval=TRUE) or not displayed (echo=FALSE)
4. Think about the dimensions of the figure and add the required specifications in the chunk options
5. Include different headers and subheaders
6. Add your answers and think about whether you want to use
    i) any ordered or unordered lists
    ii) text in **bold** or *italic*
7. Add a webside link that fits to the topic
8. Add an image   

<div class="alert alert-green" style="position: absolute; left: 600px; top: 525px">
  <h4>Note:</h4> Try to <strong>knit</strong> your .Rmd file <strong>frequently</strong> (after any major addition)!! It is highly likely that you will run into an error message and that way you can identify the cause much faster.</div>


--- &slide_no_footer .segue bg:url(img/Darst.jpg);background-size:cover

# Now its time for your FIRST CASE STUDY!!!

<p><span class="source-img" style="position: absolute; left: 50px; top: 650px; color:white">Photo by NASA (ID ISS040-E-12110), accessed 
    <a href='https://earthobservatory.nasa.gov/images/84047/coastlines-of-the-southern-baltic-sea' title=''>here</a></span></p>


--- &slide_no_footer .segue bg:#CD2626

# How do you feel now.....?

--- &vcenter
## Totally confused?
                
<img src="img/Comic_confused.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" width="400px" style="display: block; margin: auto;" />

Practice on the exercise data and go through the suggested info material.

--- &vcenter
## Totally bored?
                
<img src="img/Comic_bored.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" width="800px" style="display: block; margin: auto auto auto 0;" />

Once your done, change in the YAML header the output format to e.g. PDF and knit your .Rmd file again. How do you like that output? Play around with all the options and output formats that R Markdown provides. Convert any of your R scripts you wrote so far into an .Rmd file

---
## Totally content?
Then go grab a coffee, lean back and enjoy the rest of the day...!

<img src="img/Comic_hammock.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" width="600px" style="display: block; margin: auto;" />


--- &thankyou
