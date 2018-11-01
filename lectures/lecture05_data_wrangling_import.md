---
title       : Data Analysis with R
subtitle    : 5 - Data wrangling - 1.Import
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



# Data wrangling with tidyverse
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

---
## Data wrangling is

- a concept introduced by **Hadley Wickam**
- the art of **getting your data into R in a useful form** for visualisation and modelling
- composed of **three** main parts:

---
## Data wrangling is

- a concept introduced by **Hadley Wickam**
- the art of **getting your data into R in a useful form** for visualisation and modelling
- composed of **three** main parts:

<div class="img-with-text" style="position: absolute; left: 125px; top: 300px">
    <img src="img/Data_wrangling.png" alt="" width=800px/>
 <p><span class="source-img" style = "float:right">source of flowchart: 
    <a href='http://r4ds.had.co.nz/wrangle-intro.html' title=''>R for Data Science</a> by Wickam & Grolemund, 2017 (licensed under <a href='https://creativecommons.org/licenses/by-nc-nd/3.0/us/' title=''>CC-BY-NC-ND 3.0 US</a>)</span></p>
</div>




---
## Tidy (uni)verse
  
Is a collection of **R packages** that share **common philosophies** and are designed to work together:

<img src="img/Tidyverse_packages.png" style="width:1000px;border:0;position: absolute; left: 50px; top: 200px" </img> 


---
## Tidy (uni)verse

You will get to know during the course
  
- **readr**: reads rectangular data (like 'csv', 'tsv', and 'fwf') into R
- **tibble**: modern re-imagining of data frames
- **tidy**: re-arranges data to make it "tidy" 
- **dplyr**: provides functions for data manipulation
- **stringr**: provides wrapper functions for common string operations
- **lubridate**: handles dates/times
- **ggplot2**: a plotting system for R, based on the grammar of graphics
- **purrr**: functional programming toolkit 
- **modelr**: wraps around base R’s modelling functions to make them work naturally in a pipe

---
## Why tidyverse?

- **Consistency**
  - e.g. all *stringr* functions take a string as first argument
  - e.g. most functions take a data frame as first argument (piping)
- Tidy data imposes **good practices**
- **Synergies** between different packages/tools
- Implements **simple solutions** to common problems
- **Smarter default** settings
  - e.g. `utils::write.csv(row.names = FALSE)`, `readr::write_csv()`
- Runs **fast** (most functions implemented with Rcpp)
- More and more packages implement the tidyverse concept 

---

The easiest way to get these packages is to install the whole tidyverse:
> `install.packages("tidyverse")`

--- &slide_no_footer .segue bg:grey

# But wait ... a little detour on packages
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

---
## Packages

- are written by the **R community**
- are a collection of
  - reusable R **functions**, 
  - the **documentation** that describes how to use them, 
  - and often sample **data**
- the official **CRAN package repository** features **11782 (!)**  available packages at the moment (Nov 11, 2017)

---
## Exponential increase

<div class="img-with-text" style="position: absolute; left: 100px; top: 125px">
    <img src="img/R_package_number.png" alt="R_package_number" width=850px/>
 <p><span class="source-img" style = "float:right">The chart was created using  
    <a href='http://blog.revolutionanalytics.com/2016/04/cran-package-growth.html' title=''>this code</a> from Andrie de Vries (on Oct 12th, 2018).</span></p>
</div>


---
## Key packages and dependencies

<img src="img/Package_dependencies.png" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" width="1000px" style="display: block; margin: auto;" />


---
## Package installations (ONCE)

The 'approved' versions can be downloaded from CRAN using the **function**
> `install.packages("package_name")`

or via R Studio:

---

<img src="img/Package_installation.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" width="900px" style="display: block; margin: auto;" />

---
## Package loading (EVERY SESSION)




You load a package using the functions `library()` or `require()`. R checks whether this package has been installed and if it doesn’t exist, you’ll get an error message. The main difference between both functions is what happens if a package is not found. For consistency, simply stick to one function:

```r
library(any_package) # library("any_package") would also work
```

```
## Error in library(any_package): there is no package called 'any_package'
```

```r
require(any_package) # require("any_package")
```

---
## Package loading (cont)

If you load a specific package you add it to the search paths:
<img src="img/Search_paths.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" width="500px" style="display: block; margin: auto;" />

<p><span class="source-img" style="position: absolute; left: 625px; top: 340px">modified from 
    <a href='http://adv-r.had.co.nz/Environments.html' title=''>Advanced R</a> by H. Wickam, 2014</span></p>

- To call a function, R first has to find it. R does this by **first** looking in the **global** environment.
- If R doesn’t find it there, it looks in the **search path**, the list of all the packages you have attached.
- If packages have functions with the same name, R uses the function from the package, which was **loaded last**.


---
## Package loading (cont)

You can see the search path and package list by running `search()`.

```r
search()
```

```no-highlight
##  [1] ".GlobalEnv"        "tools:rstudio"     "package:stats"    
##  [4] "package:graphics"  "package:grDevices" "package:utils"    
##  [7] "package:datasets"  "package:methods"   "Autoloads"        
## [10] "package:base"
```

--- 

After loading


```r
library(tidyverse) 
```
you see that 8 additional tidyverse core packages are loaded.
You also see a **conflict of function names** (`filter()` and `lag()` exist in 2 packages)!

--- 

Lets look at the search path again:

```r
search()
```

```no-highlight
##  [1] ".GlobalEnv"        "package:forcats"   "package:stringr"  
##  [4] "package:dplyr"     "package:purrr"     "package:readr"    
##  [7] "package:tidyr"     "package:tibble"    "package:ggplot2"  
## [10] "package:tidyverse" "tools:rstudio"     "package:stats"    
## [13] "package:graphics"  "package:grDevices" "package:utils"    
## [16] "package:datasets"  "package:methods"   "Autoloads"        
## [19] "package:base"
```
You now see the 9 packages added to the search path (right after the global environment).

--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- &radio bg:#EEC900

# Quiz 1: Function conflicts

From which packages will R use the functions `filter()` and `lag()`?

1. _dplyr_
2. stats

*** .explanation
`dplyr` has been loaded after `stats` (which R automatically loads in every session) so `dplyr` comes before `stats` in the search path (position 2 vs 10). After R didn't find the functions `filter()` and `lag()` in the global environment it will look next in `dplyr`. As R is successfull finding the functions here, it will not continue searching elsewhere.

---
##  How to unload packages?

You remove a package from the search path using the function
> `detach(packagename)`

or by unchecking the box next to the package name in the 'Packages' pane.

<img src="img/Detach_packages.png" title="plot of chunk unnamed-chunk-9" alt="plot of chunk unnamed-chunk-9" width="900px" style="display: block; margin: auto auto auto 0;" />

---
## Information on packages

- If you run `?packagename`  (e.g. `?tidyverse`) you get some more information of what the package does and sometimes lists of functions available in this package or weblinks for further information.
- More recent packages have also so-called "vignettes", which provide even more informations than the help documentation. You can read the vignette by calling `vignette("packagename")`.
- Sometimes, a package provides several vignettes. To get an overview call the function `browseVignettes("packagename")`.


```r
vignettes("dpylr")
browseVignettes("dpylr")
```

--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- &exercise

# Explore some of the tidyverse packages (not 'tidyverse' itself) or any other one installed.

1. Load and unload 3 packages of your choice.
2. Look into the help documentation and vignettes of these 3 packages. 
  - What are they for? 
  - Who is the author?
3. Identify at least 3 functions that each of the 3 packages provides.


--- &slide_no_footer .segue bg:#1874CD

# Back to data wrangling: 1. Import
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 
<img src="img/Data_wrangling_a.png" style="width:450px;border:0;position: absolute; left: 125px; top: 200px" </img> 

---
## Data sources

- Excel files (.xls / .xlsx)
- Comma seperated values (.csv) --> most common files
- Text files (.txt)
- NetCDF (Network Common Data Form)
- Relational data bases (MySQL, PostgreSQL, etc.)
- URLs
- and many more ...

<div class="alert alert-green" style="margin-left: auto; margin-right: auto;">
  Mostly you will have flat files (with no <strong>internal hierarchy</strong> and interrelationships as in databases) to load into R.
</div>

---
## Importing data from Excel

<img src="img/Excel_import.png" title="plot of chunk unnamed-chunk-11" alt="plot of chunk unnamed-chunk-11" width="850px" style="display: block; margin: auto;" />

---
## Import functions in 'readr'

<div style="position: absolute; left: 950px; top: 25px; z-index:100">
    <img src="img/Logo_readr.png" alt="" width=75px height=75px>
</div>

- Most of readr’s functions are concerned with turning flat files into data frames:
  - `read_delim()`: reads in files with **any delimiter**.
  - `read_csv()`: **comma** delimited files (.csv)
  - `read_csv2()`: **semicolon** separated files (.csv) - common when comma used as decimal mark
  - `read_tsv()`: **tab** delimited files (.txt files)
  - and others: `read_table()`,`read_fwf()`, `read_log()`


---

- All these functions have a similar or the same syntax:

<img src="img/Readr_functions.png" title="plot of chunk unnamed-chunk-12" alt="plot of chunk unnamed-chunk-12" width="1000px" style="display: block; margin: auto auto auto 0;" />

---
## Some demonstrations of read_csv using inline csv files

Inline csv files are useful for experimenting and for creating reproducible examples:


```r
read_csv("a,b,c
1,2,3
4,5,6")
```

```no-highlight
## # A tibble: 2 x 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```


--- &twocol
### Tweaking your import - skipping lines

*** =left
You can skip the first n lines of metadata at the top of the file using **skip = n**:

```r
read_csv("The first line of metadata
  The second line of metadata
  x,y,z
  1,2,3", skip = 2)
```

```no-highlight
## # A tibble: 1 x 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

*** =right
Or use **comment = "#"** to drop all lines that start with (e.g.) #.

```r
read_csv("# A comment to skip
  x,y,z
  1,2,3", comment = "#")
```

```no-highlight
## # A tibble: 1 x 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

--- &twocol
### Tweaking your import - column names

*** =left
If you don't have column names set **col_names = FALSE**; R labels them sequentially from X1 to Xn:

```r
read_csv("1,2,3
  4,5,6", col_names = FALSE)
```

```no-highlight
## # A tibble: 2 x 3
##      X1    X2    X3
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

*** =right
You can also pass a **character vector** to col_names:

```r
read_csv("1,2,3
  4,5,6", col_names = c("x", "y", "z"))
```

```no-highlight
## # A tibble: 2 x 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

--- 
### Tweaking your import - Specify column types

readr functions guess the type of each column and convert types when appropriate (but will NOT convert strings to factors automatically). If you want to specify other types use a **col_function** in the col_types argument to guide parsing.


```r
read_csv("your_file.csv", col_types = cols(
  a = col_integer(),
  b = col_character(),
  c = col_logical() )
)
```

--- &twocol
### Tweaking your import - NAs

The argument `na` specifies the value (or values) that are used to represent missing values in your file (-999 or -9999 is a typical place holder for missing values).

*** =left

```r
read_csv("a,b,c
  1,2,.", na = ".")
```

```no-highlight
## # A tibble: 1 x 3
##       a     b c    
##   <int> <int> <chr>
## 1     1     2 <NA>
```

*** =right

```r
read_csv("a,b,c
  1,-9999,2", na = "-9999")
```

```no-highlight
## # A tibble: 1 x 3
##       a b         c
##   <int> <chr> <int>
## 1     1 <NA>      2
```


---
## So what are these **tibbles**?

- The **'tibble'** package provides a **'tbl_df'** class (the 'tibble') that provides stricter checking and better formatting than the traditional data frame.
- **Major differences** to a data frame:
  - never changes the type of the inputs (e.g. it never converts strings to factors!)
  - never creates row names
  - never changes the names of variables
  - non-syntactic column names possible (e.g. names can contain unusual characters like a space) --> BUT DONT GO THAT ROAD!
  - tibbles generate a warning if the column you are trying to access does not exist
  - printing and subsetting differs

---
## So what are these **tibbles**? (cont)

- Functions for data frames will work also for tibbles.
- All tidyverse packages generate tibbles automatically
- To learn more check `vignette("tibble")`.

---
## Creating tibbles

- Automatically created when importing data with *readr*
- Convert an existing data frame with `tibble::as_tibble(your_dataframe)` (NOTE: tidyverse uses underscores, not points)

---
## Creating tibbles

- Automatically created when importing data with *readr*
- Convert an existing data frame with `tibble::as_tibble(your_dataframe)` (NOTE: tidyverse uses underscores, not points)

```r
iris_tbl <- as_tibble(iris)
# Compare the difference:
class(iris)
```

```no-highlight
## [1] "data.frame"
```

```r
class(iris_tbl)
```

```no-highlight
## [1] "tbl_df"     "tbl"        "data.frame"
```
As you see, **iris_tbl** inherits still the `data.frame` class, but has in addition also the `tbl_df` class.

---
## Creating tibbles (cont)

- Or you can create a new tibble from individual vectors with `tibble()`

```r
tibble(x = 1:5, y = 1, z = x ^ 2 + y)
```

```no-highlight
## # A tibble: 5 x 3
##       x     y     z
##   <int> <dbl> <dbl>
## 1     1     1     2
## 2     2     1     5
## 3     3     1    10
## 4     4     1    17
## 5     5     1    26
```
Inputs of shorter length are automatically recycled!

---
## Printing tibble

- each column reports its **type**
- only the first **10 rows** and all columns that **fit on screen** are shown --> much easier to work with large data
- if you want to change the number of rows (**n**) and columns (**width**) use `print()` and change the arguments:

---
## Printing tibble

- each column reports its **type**
- only the first **10 rows** and all columns that **fit on screen** are shown --> much easier to work with large data
- if you want to change the number of rows (**n**) and columns (**width**) use `print()` and change the arguments:


```r
print(iris_tbl, n = 2, width = Inf)  # = Inf shows all columns
```

```no-highlight
## # A tibble: 150 x 5
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
##          <dbl>       <dbl>        <dbl>       <dbl> <fct>  
## 1          5.1         3.5          1.4         0.2 setosa 
## 2          4.9         3            1.4         0.2 setosa 
## # ... with 148 more rows
```

---
## Overview of more functions:

<div class="img-with-text" style="position: absolute; left: 200px; top: 100px">
    <img src="img/Cheatsheet_readr.png" alt="" width=675px/>
 <p><span class="source-img" style = "float:right">
 Cheat sheet is freely available at 
 <a href='https://www.rstudio.com/resources/cheatsheets/' title=''>https://www.rstudio.com/resources/cheatsheets/</a></span></p>
</div>


--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- &radio bg:#EEC900
# Quiz 2: Import functions

What function would you use to **read a file where fields are separated with "|"**? 

1. _read_delim()_
2. read_csv()
3. read_csv2()
4. read_tsv()
5. read_table()
6. read_fwf()

*** .hint
<small>You should find a solution without a hint. But look in the help documentation and play around with one of the previous inline csv file examples.</small>

*** .explanation
`read_delim()` has the extra argument `delim` where you can specify the character used to seperate fields.


--- &radio bg:#EEC900
# Quiz 3: Import functions

What function would you use if you **generated a CSV file on your own computer**? 

1. read_delim()
2. read_csv()
3. _read_csv2()_
4. read_tsv()
5. read_table()
6. read_fwf()

*** .hint
<small>Check which symbol your computer uses as decimal mark (you can see that in Excel).</small>

*** .explanation
Computers in Germany typically use a comma as decimal mark, hence, when you generate a CSV file in Excel a semicolon will automatically be used as delimitor. In that case you should use `read_csv2()`.

--- &checkbox bg:#EEC900
# Quiz 4: Import functions

What arguments do `read_delim()` and `read_csv()` have **NOT** in common?

1. progress
2. quote 
3. trim_ws
4. _delim_
5. _escape_backslash_
6. guess_max
7. _escape_double_


--- &twocol bg:#EEC900
# Quiz 5: Import functions

Identify what is wrong with each of the following inline CSV files. What happens when you run the code? (You'll find the solutions at the end of the presentation.)

*** =left

```r
read_csv("a,b
  1,2,3
  4,5,6")
read_csv("a,b,c
  1,2
  1,2,3,4")
```

*** =right

```r
read_csv("a,b
  1,2
  a,b")
read_csv("a;b
  1;3")
```

--- &exercise
# Quiz 6: Tibble vs data frame

Compare and contrast the following operations on a `data.frame` and equivalent `tibble`. 


```r
df <- data.frame(abc = 1, xyz = "a")
df$x
df[, "xyz"]
df[, c("abc", "xyz")]
```

What is different? Why might the default data frame behaviours cause you frustration?

---
## Other types of data
If you have other types of files to import try one of the following packages:
- **haven** - SPSS, Stata, and SAS files
- **readxl** - Excel files (.xls and .xlsx)
- **DBI** - databases
- **jsonlite** - json
- **xml2** - XML
- **httr** - Web APIs
- **rvest** - HTML (Web Scraping)

---
## Roadmap

<img src="img/Roadmap.png" title="plot of chunk unnamed-chunk-27" alt="plot of chunk unnamed-chunk-27" width="1000px" style="display: block; margin: auto;" />

--- &slide_no_footer .segue bg:#FF8C00

# Some real example to import
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

---

<img src="img/ICES_webpage.png" title="plot of chunk unnamed-chunk-28" alt="plot of chunk unnamed-chunk-28" width="800px" style="display: block; margin: auto;" />

---

<img src="img/ICES_data_portal.png" title="plot of chunk unnamed-chunk-29" alt="plot of chunk unnamed-chunk-29" width="800px" style="display: block; margin: auto;" />

---

<img src="img/ICES_oceanographic_data.png" title="plot of chunk unnamed-chunk-30" alt="plot of chunk unnamed-chunk-30" width="800px" style="display: block; margin: auto;" />

---

<img src="img/ICES_download.png" title="plot of chunk unnamed-chunk-31" alt="plot of chunk unnamed-chunk-31" width="900px" style="display: block; margin: auto;" />

---
## Lets import the data following the roadmap

### 1.Step: Open the file in the editor to check the content

> - Go to the 'Files' pane.
> - Find the file "1111473b.csv" in the folder 'Data_Analysis_with_R/data' .
> - Click on the file and choose "View file", which opens the file in the 'Source' pane.
> - Lets check

---

<img src="img/Editor_data_check.png" title="plot of chunk unnamed-chunk-32" alt="plot of chunk unnamed-chunk-32" width="800px" style="display: block; margin: auto;" />

---
## Lets import the data following the roadmap

### 2.Step: Read the data into R

- Make sure before that you've set the **working directory** correct. 
- The **wrong** working directory is the **most common reason** for error messages!


```r
hydro <- read_csv("data/1111473b.csv")
```

---
## Lets check the data


```r
print(hydro, n = 5)
```

```no-highlight
## # A tibble: 30,012 x 11
##   Cruise Station Type  `yyyy-mm-ddThh:mm`  `Latitude [degr…
##   <chr>  <chr>   <chr> <dttm>                         <dbl>
## 1 ????   0247    B     2015-02-17 09:54:00               55
## 2 ????   0247    B     2015-02-17 09:54:00               55
## 3 ????   0247    B     2015-02-17 09:54:00               55
## 4 ????   0247    B     2015-02-17 09:54:00               55
## 5 ????   0247    B     2015-02-17 09:54:00               55
## # ... with 3.001e+04 more rows, and 6 more variables: `Longitude
## #   [degrees_east]` <dbl>, `Bot. Depth [m]` <chr>, `PRES [db]` <dbl>,
## #   `TEMP [deg C]` <dbl>, `PSAL [psu]` <dbl>, `DOXY [ml/l]` <dbl>
```

---
## Change column names

To make subsetting and data manipulation easier change the column names, e.g.


```r
names(hydro) <- c("cruise", "station", "type", "date_time",
  "lat", "long", "depth", "pres", "temp", "psal", "doxy")
```

--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- &exercise
## Checking tasks:

1. Read the file into your workspace.
2. Check the dimensions of the tibble `hydro`. Do they match with what you've seen in the Editor?
3. What happened with the empty elements in, e.g., row 127-136?
4. Do you agree with the data types of each column? 


--- &multitext bg:#EEC900
# Quiz 7: Test your R knowledge

Subset the data to get only observations of Station "0613" and 

1. calculate the mean salinity (psal) and 
2. mean oxygen concentration (doxy)
3. Calculate the mean temperature ('temp') for the surface layer (1-10 m depth = 'pres' 1-10), averaged across all stations and cruises for the entire year.

*** .explanation
1. and 2.
Either you subset first and then calculate the means or you do both in one step:

`hydro_sub1 <- hydro[hydro$station == "0613", ]` and `mean(hydro_sub1$psal)` and 
`mean(hydro_sub1$doxy)`

Alternatively:
`mean(hydro$psal[hydro$station == "0613"])` and
`mean(hydro$doxy[hydro$station == "0613"])`

3.You could subset in 2 ways:

`hydro_sub2 <- hydro[hydro$pres %in% 1:10, ]`
or `hydro_sub2 <- hydro[hydro$pres >= 1 & hydro$pres <= 10, ]` 

and then calculate the mean `mean(hydro_sub2$temp, na.rm=T)`

1. <span class='answer'>12.0872</span>
2. <span class='answer'>0.322</span>
3. <span class='answer'>10.0745985</span>



--- &slide_no_footer .segue bg:#1874CD

# Saving and exporting data

---
## Saving your data as R objects

You can save your tibble or data frame as an .R object and load it later with `save(your_tibble, "filename")` and `load("filename")`:


```r
save(your_subset, file = "My_first_object.R")
# Lets remove your subset and see what happens when we load it again
rm(your_subset)
your_subset
load(file = "My_first_object.R")
your_subset # now it should be back again
```

---
## Exporting your data 

- If you want to export your data for other programs, its best if you stick to the same format as you import, e.g. CSV files.
- Most import functions in 'readr' have a corresponding export function:
  - `read_delim()` --> **`write_delim()`**
  - `read_csv()` --> **`write_csv()`**
  - `read_tsv()` --> **`write_tsv()`**
  - other functions: **`write_excel_csv()`**
  

--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- &exercise
## Task: Saving and Exporting

With the subsets you created (or any other tibble/data frame in your workspace):

- save one as an R object and 
- one as CSV file

--- &slide_no_footer .segue bg:#E5E5E5

## Overview of functions you learned today

`install.packages()`, `library()`, `require()`, `search()`, `detach()`, `vignette()`, `browseVignettes()`,

`read_delim()`, `read_csv()`, `read_csv2()`, `read_tsv()`, `read_table()`, `read_fwf()`, `read_log()`,

`tibble()`, `as_tibble()`, `print()`, `save()`, `load()`,

`write_delim()`, `write_csv()`, `write_tsv()`, `write_excel_csv()`


--- &slide_no_footer .segue bg:#CD2626

# How do you feel now.....?

--- &vcenter

## Totally confused?
                
<img src="img/Comic_confused.png" title="plot of chunk unnamed-chunk-37" alt="plot of chunk unnamed-chunk-37" width="400px" style="display: block; margin: auto;" />

Go thorougly through the tasks and quizzes. 
Read the chapter [10 Tibbles](http://r4ds.had.co.nz/tibbles.html) and [11 Data import](http://r4ds.had.co.nz/data-import.html) in 'R for Data Science'.

--- &vcenter

## Totally bored?
                
<img src="img/Comic_bored.png" title="plot of chunk unnamed-chunk-38" alt="plot of chunk unnamed-chunk-38" width="800px" style="display: block; margin: auto auto auto 0;" />

Then try out to import, explore and export other datasets you have (from Excel).

---

## Totally content?
Then go grab a coffee, lean back and enjoy the rest of the day...!

<img src="img/Comic_hammock.png" title="plot of chunk unnamed-chunk-39" alt="plot of chunk unnamed-chunk-39" width="600px" style="display: block; margin: auto;" />

--- &thankyou


--- &slide_no_footer .segue bg:#CD2626

# Solutions

---

## Quiz 5: Import functions

1. Example: The header has 1 element (=column) less than the data --> **R skips the 3rd element** of each data row then completely (3 and 6 are not shown anymore).

2. Example: The 1st data row has 1 element less than the header and the 2nd data row --> R automatically **fills the missing element with a NA**.

3. Example: The data rows have mixed data types --> R **coerces** all values to the more general **character** data type .

4. Example: Remember, the function `read_csv()` expects a **comma** as delimiter, NOT a semicolon --> R reads it then as 1 element per row. Try alternatively:

```r
read_csv2("a;b
  1;3")
```

--- &twocol

## Quiz 6: Tibble vs. data frame



For tibbles the complete column name is needed. This can be useful in case "x" doesn't exist but 2 other columns that contain the letter x in their names.
If you subset tibbles like a matrix ([row, col]) you will always get a tibble returned and no vectors (as data frames do in the 2nd example).

```r
df_tbl <- as_tibble(df)
df_tbl$x
```

```no-highlight
## NULL
```

*** =left

```r
df_tbl[, "xyz"]
```

```no-highlight
## # A tibble: 1 x 1
##   xyz  
##   <fct>
## 1 a
```

*** =right

```r
df_tbl[, c("abc", "xyz")] 
```

```no-highlight
## # A tibble: 1 x 2
##     abc xyz  
##   <dbl> <fct>
## 1     1 a
```