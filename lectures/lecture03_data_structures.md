---
title       : Data Analysis with R
subtitle    : 3 - Data structures and basic calculations
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
--- &slide_no_footer .segue bg:grey



# Some recap on data structures
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

---
## Data structures

Five data types most often used in data analysis:

|Dimensions | Homogeneous | Heterogeneous |
|:------:|:------:|:-------:|
| 1d | Atomic vector | List |
|2d | Matrix | Data frame |
|nd | Array |  |


--- &slide_no_footer .segue bg:#1874CD

# Lists
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

---
## Lists

- are different from atomic vectors because their **elements** can be of **any type, including lists**
- you construct lists by using `list()` instead of `c()`:

```r
x <- list(1:3, "a", c(TRUE, FALSE, TRUE), c(2.3, 5.9))
str(x)
```

```no-highlight
## List of 4
##  $ : int [1:3] 1 2 3
##  $ : chr "a"
##  $ : logi [1:3] TRUE FALSE TRUE
##  $ : num [1:2] 2.3 5.9
```

---
## Lists are vectors

<img src="img/Hierarchy_vectors.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" width="450px" style="display: block; margin: auto;" />

`NULL` is often used to represent the absence of a vector (as opposed to `NA` which is used to represent the absence of a value in a vector). `NULL` typically behaves like a vector of length 0.

---
## Why is a list considered a vector?

<img src="img/ListsVsAtomicVectors.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" width="900px" style="display: block; margin: auto;" />

---
## Lists (cont)

- are sometimes called **recursive vectors**, because a list can contain other lists. 

```r
x <- list(list(list(list())))
str(x)
```

```no-highlight
## List of 1
##  $ :List of 1
##   ..$ :List of 1
##   .. ..$ : list()
```

---
## Visualization of the following lists


```r
x1 <- list(c(1, 2), c(3, 4))
x2 <- list(list(1, 2), list(3, 4))
x3 <- list(1, list(2, list(3)))
```

<div class="img-with-text" style="position: absolute; left: 150px; top: 275px">
    <img src="img/List_hierarchies.png" alt="" width=650px/>
 <p><span class="source-img" style = "float:right">source: 
    <a href='http://r4ds.had.co.nz/lists.html' title=''>R for Data Science</a> by Wickam & Grolemund, 2017 (licensed under <a href='https://creativecommons.org/licenses/by-nc-nd/3.0/us/' title=''>CC-BY-NC-ND 3.0 US</a>)</span></p>
</div>


---
## Lists (cont)

- `typeof()` a list is a list
- you can **test** for a list with `is.list()` and 
- **coerce** to a list with `as.list()` 
- you can **turn** a list into an **atomic vector** with `unlist()`. 
- if the elements of a list have different types, `unlist()` uses the **same coercion rules** as `c()`.
- lists are used to **build** up many of the more **complicated data structures** in R.

--- &twocol
## Structure of lists
A very useful tool for working with lists is `str()` because it focuses on the structure, not the content.

*** =left 

```r
x <- list(1, 2, 3)
str(x)
```

```no-highlight
## List of 3
##  $ : num 1
##  $ : num 2
##  $ : num 3
```

--- &twocol
## Structure of lists
A very useful tool for working with lists is `str()` because it focuses on the structure, not the content.

*** =left 

```r
x <- list(1, 2, 3)
str(x)
```

```no-highlight
## List of 3
##  $ : num 1
##  $ : num 2
##  $ : num 3
```

*** =right

```r
x_named <- list(a = 1, b = 2, c = 3)
str(x_named)
```

```no-highlight
## List of 3
##  $ a: num 1
##  $ b: num 2
##  $ c: num 3
```

---
## Subsetting

**Three** ways to subset a list: 

1. `[` extracts a **sublist**. 
2. `[[` extracts a **single componen**t from a list. 
3. `$` is a shorthand for extracting **named elements** of a list.

---
## Subsetting (cont)

I will demonstrate each way using the following list:


```r
a <- list(a = 1:3, b = "a string", c = pi, list(-1, -5))
str(a)
```

```no-highlight
## List of 4
##  $ a: int [1:3] 1 2 3
##  $ b: chr "a string"
##  $ c: num 3.14
##  $  :List of 2
##   ..$ : num -1
##   ..$ : num -5
```

--- &twocol
## Subsetting: '[ ]'

1.`[` extracts a sublist. The **result** will always be a **list** (it keeps the original list 'container' and removes all elements not selected). Like with vectors, you can subset with a **logical, integer, or character vector**.

*** =left 

```r
str(a[1:2])
```

```no-highlight
## List of 2
##  $ a: int [1:3] 1 2 3
##  $ b: chr "a string"
```

```r
str(a[4])
```

```no-highlight
## List of 1
##  $ :List of 2
##   ..$ : num -1
##   ..$ : num -5
```

*** =right 

--- &twocol
## Subsetting: '[ ]'

1.`[` extracts a sublist. The **result** will always be a **list** (it keeps the original list 'container' and removes all elements not selected). Like with vectors, you can subset with a **logical, integer, or character vector**.

*** =left 

```r
str(a[1:2])
```

```no-highlight
## List of 2
##  $ a: int [1:3] 1 2 3
##  $ b: chr "a string"
```

```r
str(a[4])
```

```no-highlight
## List of 1
##  $ :List of 2
##   ..$ : num -1
##   ..$ : num -5
```

*** =right 

```r
a[4]
```

```no-highlight
## [[1]]
## [[1]][[1]]
## [1] -1
## 
## [[1]][[2]]
## [1] -5
```

--- &twocol
## Subsetting: '[[ ]]'

2.`[[` extracts a single component from a list. It **removes a level of hierarchy** from the list (= you remove **one** 'container').

*** =left 

```r
str(a[[1]])
```

```no-highlight
##  int [1:3] 1 2 3
```

```r
str(a[[4]])
```

```no-highlight
## List of 2
##  $ : num -1
##  $ : num -5
```

*** =right 

```r
a[[4]]
```

```no-highlight
## [[1]]
## [1] -1
## 
## [[2]]
## [1] -5
```

--- &twocol
## Subsetting: '$'

3.`$` is a **shorthand for extracting named** elements of a list. It works similarly to `[[` except that you don’t need to use quotes.

*** =left

```r
a$a
```

```no-highlight
## [1] 1 2 3
```

*** =right

```r
# same as 
a[["a"]]
```

```no-highlight
## [1] 1 2 3
```

---
## Some visualization of subsetting lists

<div class="img-with-text" style="position: absolute; left: 250px; top: 120px">
    <img src="img/Subsetting_lists.png" alt="" width=550px/>
 <p><span class="source-img" style = "float:right">source: 
    <a href='http://r4ds.had.co.nz/lists.html' title=''>R for Data Science</a> by Wickam & Grolemund, 2017 (licensed under <a href='https://creativecommons.org/licenses/by-nc-nd/3.0/us/' title=''>CC-BY-NC-ND 3.0 US</a>)</span></p>
</div>


--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- --- &exercise
# Visualize the following lists as nested sets 

<span style="font-size:25px">1. list(a, b, list(c, d), list(e, f))</span>

<span style="font-size:25px">2. list(list(list(list(list(list(a))))))</span>


--- &radio bg:#EEC900
# Quiz 1: Subsetting lists

The following list has been created:

```r
list_example <- list(one = 1:10, two = letters, 
  three = list(abc = c(132, 876, 42), xyz = c(T,F,F,T,F,T)), four = NULL)
```
What does the following return? `list_example[1:2]`

1. a vector with the first 2 elements of each list
2. a list of all sublists, each containing only the first 2 elements of the original sublists
3. _a list containing only sublist "one" and "two"_
4. NA

*** .explanation
`[` extracts always sublists and returns a list. In this example, you extract the first and second sublists, which are the numeric vector "one" and the character vector "two".


--- &radio bg:#EEC900
# Quiz 2: Subsetting lists

The following list has been created:

```r
list_example <- list(one = 1:10, two = letters, 
  three = list(abc = c(132, 876, 42), xyz = c(T,F,F,T,F,T)), four = NULL)
```
What does the following return? `list_example["four"]`

1. NULL 
2. error message 
3. _a list containing NULL_
4. a vector with NULL elements
 
*** .explanation
`[` extracts always sublists and returns a list. In this example, you extract the sublist that is called "four", which is the fourth sublist containing NULL elements. 


--- &radio bg:#EEC900
# Quiz 3: Subsetting lists

The following list has been created:

```r
list_example <- list(one = 1:10, two = letters, 
  three = list(abc = c(132, 876, 42), xyz = c(T,F,F,T,F,T)), four = NULL)
```
What does the following return? `list_example[[1]][2]`

1. a list containing "a"
3. a list containing 1
6. a vector containing "b"
8. _a vector containing 2_

*** .explanation
`[[` extracts always single components from a list. In this case, it extracts the first sublist, which is a vector, and from there the 2nd element, which is a 2. So the returned object is also a vector containing only the number 2.


--- &radio bg:#EEC900
# Quiz 4: Subsetting lists

The following list has been created:

```r
list_example <- list(one = 1:10, two = letters, 
  three = list(abc = c(132, 876, 42), xyz = c(T,F,F,T,F,T)), four = NULL)
```
What does the following return? `list_example[3][[2]]`

1. NA
2. a list containing FALSE
3. the logical vector 'xyz'
4. a vector containing "c"
5. _error message_

*** .explanation
This is a bit trickier! The code snippet tries to subset the following: return a list that extracts from 'list_example' the 3rd sublist and from this list take sublist 2. 
BUT: that list has only 1 element, which is the list 'three' (containing vectors 'abc' and 'xyz'); a sublist 2 doesn't exist. However, the following would have worked: `list_example[2:3][[2]]` since now the extracted list contains 2 sublists, "two" and "three", from which it can subset list "three".


--- &checkbox bg:#EEC900
# Quiz 5: Subsetting lists

What is equivalent to the following code (multiple answers correct)? And which of the options below returns a suprising value?

`list_example[["three"]][c("abc", "xyz")]`

1. _list_example[[3]][1:2]_
2. list_example[[3]][[1:2]]
3. _list_example[[3]][c("abc", "xyz")]_
4. _list_example$three[1:2]_
5. _list_example$three[c("abc", "xyz")]_

*** .explanation
Option 2 subsets something else, which is not so intuitive: it extracts also the 3rd sublist "three", but from there it subsets the 2nd element of the 1st sublist (the vector "abc"). DO NOT use this notation for extracting the number '876', use instead: `list_example[[3]][[1]][2]` (element 2 in sublist 1 within sublist 3)!!!

--- &multitext bg:#EEC900
# Quiz 6 - Challenge: Subsetting lists

Create a new vector that contains the 4th element of sublist "one" and element 1 and 3 from sublist "abc" within "three" in 'list_example'. 

1. What is the sum of this vector?

*** .hint
<small>Within the vector you extract first the value from sublist "one" and then values from sublist "abc" within sublist "three" (both seperated by a comma).</small>

*** .explanation
To get the correct answer you could subset for instance like this:   
`sum( c(list_example[[1]][2], list_example[[3]][[1]][c(1,3)]) )`   
or using the `$` sign:   
`sum( c(list_example$one[2], list_example$three$abc[c(1,3)]) )` 

1. <span class='answer'>176</span>


--- &multitext bg:#EEC900
# Quiz 7 - Challenge: Subsetting lists

Execute the following R command in your console

```r
lm_list <- lm(Sepal.Length ~ Sepal.Width, data = iris)
```
and look at the structure of the list you created with

```r
str(lm_list, max.level = 1) # max.level=1 shows only the first level 
# of the hierarchy (and not all sub/sub/..lists))
```
1. What is the last value of the 'residuals'?

*** .hint
<small>Look at the names of the sublists in `lm_list`. Is there anything that sounds like what we are looking for? If you found it check the number of elements it contains (we want the last one!).</small>

*** .explanation
The object created from a linear regression (that is what the `lm()` function does) is a long list with many nested lists. lm_list contains 12 sublists amongst one is a vector called 'residuals' (thats what we are after). So to get the last value (from the 150 values) type:
`lm_list$residuals[150]`

1. <span class='answer'>0.0438606</span>


--- &slide_no_footer .segue bg:#1874CD

# Other homogeneous data structures: matrices and arrays
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

--- &twocol
## Matrices and arrays

*** =left
- Adding a `dim` attribute to an atomic vector allows it to behave like a **multi**-dimensional **array**. 
- A special case of the array is the **matrix**, which has **two** dimensions. 
- **Matrices** are used commonly as part of the **mathematical machinery** of statistics. 
- Arrays are much **rarer**, but worth being aware of.

*** =right

<img src="img/Arrays.jpg" title="plot of chunk unnamed-chunk-23" alt="plot of chunk unnamed-chunk-23" width="500px" style="display: block; margin: auto;" />



--- 
## Creating matrices

Matrices are **created** with 

- `matrix()` 
- or by **combining vectors** (of **equal length**) to a matrix using `cbind()`
(stands for column-binding).


--- &twocol
## Creating matrices

Matrices are **created** with 

- `matrix()` 
- or by **combining vectors** (of **equal length**) to a matrix using `cbind()`
(stands for column-binding).

*** =left 

```r
a <- matrix(1:6, ncol = 3, nrow = 2)
a
```

```no-highlight
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

*** =right

```r
v1 <- 1:3
v2 <- 4:6
a <- cbind(v1, v2)
a
```

```no-highlight
##      v1 v2
## [1,]  1  4
## [2,]  2  5
## [3,]  3  6
```

---
## Attributes length and names

`length()` and `names()` have **high-dimensional generalisations**:

--- &twocol
## Attribute length

`length()` generalises to 

- `nrow()` and `ncol()` for **matrices**, and 
- `dim()` for arrays.

*** =left 

```r
length(a)
```

```no-highlight
## [1] 6
```

*** =right

```r
nrow(a)
```

```no-highlight
## [1] 3
```

```r
ncol(a)
```

```no-highlight
## [1] 2
```

---
## Attribute names

`names()` generalises to 

- `rownames()` and `colnames()` for **matrices**, and 
- `dimnames()`, a list of character vectors, for arrays.


```r
colnames(a) <- c("A","B")
rownames(a) <- c("a","b","c")
a
```

```no-highlight
##   A B
## a 1 4
## b 2 5
## c 3 6
```

--- 
## Subsetting matrices and arrays

Most common way of subsetting matrices (2d) and arrays (>2d) is a simple **generalisation of 1d subsetting**: 

- You supply a **1d index** for each dimension, separated by a comma (*integer, logical, or character* indices allowed). 
- **Blank subsetting** is now useful because it lets you keep all rows or all columns.

--- &twocol
## Subsetting matrices and arrays

Most common way of subsetting matrices (2d) and arrays (>2d) is a simple **generalisation of 1d subsetting**: 

- You supply a **1d index** for each dimension, separated by a comma (*integer, logical, or character* indices allowed). 
- **Blank subsetting** is now useful because it lets you keep all rows or all columns.

*** =left 

```r
a <- matrix(1:9, nrow = 3)
colnames(a) <- c("A", "B", "C")
a
```

```no-highlight
##      A B C
## [1,] 1 4 7
## [2,] 2 5 8
## [3,] 3 6 9
```

*** =right

```r
a[1:2, 2]
a[, c("A", "C") ] 
```
**Guess which values you get!**

--- &twocol
## Subsetting matrices and arrays

Most common way of subsetting matrices (2d) and arrays (>2d) is a simple **generalisation of 1d subsetting**: 

- You supply a **1d index** for each dimension, separated by a comma (*integer, logical, or character* indices allowed). 
- **Blank subsetting** is now useful because it lets you keep all rows or all columns.

*** =left 

```r
a <- matrix(1:9, nrow = 3)
colnames(a) <- c("A", "B", "C")
a
```

```no-highlight
##      A B C
## [1,] 1 4 7
## [2,] 2 5 8
## [3,] 3 6 9
```

*** =right

```r
a[1:2, 2]
```

```no-highlight
## [1] 4 5
```

```r
a[, c("A", "C") ] 
```

```no-highlight
##      A C
## [1,] 1 7
## [2,] 2 8
## [3,] 3 9
```

--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- &submitcompare1 bg:#EEC900
# Quiz 8: Subsetting matrices

Subset the following matrix...

```r
(mat <- matrix(c(0,NA,4,18,35,97,7,9,20), nrow = 3))
```

```no-highlight
##      [,1] [,2] [,3]
## [1,]    0   18    7
## [2,]   NA   35    9
## [3,]    4   97   20
```
... to get all values in row 1

*** .explanation
This is what you should have written:
`mat[1, ]`

--- &submitcompare1 bg:#EEC900
# Quiz 9: Subsetting matrices

Subset the following matrix...

```r
(mat <- matrix(c(0,NA,4,18,35,97,7,9,20), nrow = 3))
```

```no-highlight
##      [,1] [,2] [,3]
## [1,]    0   18    7
## [2,]   NA   35    9
## [3,]    4   97   20
```
... to get all values in row 1 and 3

*** .explanation
This is what you should have written:
`mat[c(1,3), ]`

--- &submitcompare1 bg:#EEC900
# Quiz 10: Subsetting matrices
Subset the following matrix...

```r
(mat <- matrix(c(0,NA,4,18,35,97,7,9,20), nrow = 3))
```

```no-highlight
##      [,1] [,2] [,3]
## [1,]    0   18    7
## [2,]   NA   35    9
## [3,]    4   97   20
```
... to get all values in column 2

*** .explanation
This is what you should have written:
`mat[ ,2]`

--- &submitcompare1 bg:#EEC900
# Quiz 11: Subsetting matrices
Subset the following matrix...

```r
(mat <- matrix(c(0,NA,4,18,35,97,7,9,20), nrow = 3))
```

```no-highlight
##      [,1] [,2] [,3]
## [1,]    0   18    7
## [2,]   NA   35    9
## [3,]    4   97   20
```
... to get all values in row 2 and 3 and column 1 and 2

*** .explanation
This is what you should have written:
`mat[c(2,3),c(1,2)]`


--- &slide_no_footer .segue bg:#1874CD

# Other heterogeneous data structures: data frames
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

--- 
## Data frames
<img src="img/Data_frames.png" style="width:250px;border:0;position: absolute; left: 700px; top: 25px" </img> 

- **Most common way** of storing data in R.  
- Represents a **list of equal-length vectors** 
  - → makes it 2-dimensional structure
- Shares properties of both the matrix and the list: 


--- 
## Data frames
<img src="img/Data_frames.png" style="width:250px;border:0;position: absolute; left: 700px; top: 25px" </img> 

- **Most common way** of storing data in R.  
- Represents a **list of equal-length vectors** 
  - → makes it 2-dimensional structure
- Shares properties of both the matrix and the list: 
  - **names**: has `names()`, `colnames()`, and `rownames()`, although `names()` and `colnames()` are the same thing. 
  - **length**: `length()`is the length of the underlying list and so is the same as `ncol()`; `nrow()` gives the number of rows.

---
## Generating data frames
You create a data frame using `data.frame()` (note the **point** inbetween both words!), which takes **named vectors** as input:


```r
df <- data.frame(x = 1:3, y = c("a", "b", "c")) 
str(df)
```

```no-highlight
## 'data.frame':	3 obs. of  2 variables:
##  $ x: int  1 2 3
##  $ y: Factor w/ 3 levels "a","b","c": 1 2 3
```


---
## Generating data frames
You create a data frame using `data.frame()` (note the **point** inbetween both words!), which takes **named vectors** as input:


```r
df <- data.frame(x = 1:3, y = c("a", "b", "c")) 
str(df)
```

```no-highlight
## 'data.frame':	3 obs. of  2 variables:
##  $ x: int  1 2 3
##  $ y: Factor w/ 3 levels "a","b","c": 1 2 3
```

- Beware of `data.frame()`s default behaviour, which turns **strings into factors**. Use `stringsAsFactors = FALSE` to suppress this behaviour:


```r
df <- data.frame(x = 1:3, y = c("a", "b", "c"), stringsAsFactors = FALSE)
str(df)
```

```no-highlight
## 'data.frame':	3 obs. of  2 variables:
##  $ x: int  1 2 3
##  $ y: chr  "a" "b" "c"
```

--- &twocol
## Subsetting data frames

*** =left
Either like a **matrix** (useful if several columns and rows are selected)

```r
df[1:2, 1] # row 1-2, column 1
```

```no-highlight
## [1] 1 2
```

*** =right

--- &twocol
## Subsetting data frames

*** =left
Either like a **matrix** (useful if several columns and rows are selected)

```r
df[1:2, 1] # row 1-2, column 1
```

```no-highlight
## [1] 1 2
```

*** =right
Or like a **list**

```r
df$x  # shows all elements of column 'x'
```

```no-highlight
## [1] 1 2 3
```

```r
df$y[2]  # 2nd element of column 'y'
```

```no-highlight
## [1] "b"
```

```r
df[[2]][2]  # same
```

```no-highlight
## [1] "b"
```

--- &slide_no_footer .segue bg:#EEC900

# Your turn...

--- --- &exercise

## Generate a data frame yourself...

... that contains 
- **4 variables** with differet data types (logical, character, double, and/or integer), 
- all of **length 20** and
- give each variable a **name**.


--- &radio bg:#EEC900
# Quiz 12: `iris` dataset - data structure

Explore the following dataset 

```r
head(iris, 1)
```

```no-highlight
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
```

What type of data structure is `iris`?

1. list
2. matrix
3. array
4. _data frame_

*** .hint
<small>Use the `class()` function to answer this question.</small>

*** .explanation
`iris` is a data frame because it is 2-dimensional and contains different types (it is heterogeneous).


--- &radio bg:#EEC900
# Quiz 13: `iris` dataset - dimensions

What are the dimensions of the dataset `iris`?

1. 5 rows, 150 columns
2. _150 rows, 5 columns_

*** .hint
<small>Use the `nrow()` and `ncol()` functions to answer this question.</small>


--- &checkbox bg:#EEC900
# Quiz 14: `iris` dataset - data type

Which basic data types does the dataset `iris` contain?

1. logical
2. integer
3. _double_
4. character
5. _factor_
6. date

*** .hint
<small>Use the `str()` function to answer this question.</small>

*** .explanation
The first 4 columns contain decimal numbers, the last is a character vector with additional attributes, which makes it a factor (see also `attributes(iris$Species)`).

--- &multitext bg:#EEC900
# Quiz 15: `iris` dataset - subsetting

1. Calculate the sum of all observations in the dataset using the function `sum()`

*** .explanation
The easiest is to subset matrix-like within the `sum` function: `sum( iris[, 1:4] )`

1. <span class='answer'>2078.7</span>


--- &slide_no_footer .segue bg:#1874CD

# The workspace or the global environment
<img src="img/Data_science_1a.png" style="height:150px;border:0;position: absolute; left: 900px; top: 50px" </img> 

---
When you create R objects, you'll see them appear in your environment pane under **Global Environment**:


```r
x <- 1:10
y <- 1:10
z <- cbind(x,y)  # matrix
```

<img src="img/Workspace.png" title="plot of chunk unnamed-chunk-45" alt="plot of chunk unnamed-chunk-45" width="600px" style="display: block; margin: auto auto auto 0;" />

---
The global environment, more often known as the **user's workspace**, is the first item on the search path. When a user starts a new session in R, the R system creates a new environment **for objects created during that session**.

You can list all objects in the workspace using the function `ls()`:




```r
x <- 1:10
y <- 1:10
z <- cbind(x,y)  # matrix
ls()
```

```no-highlight
## [1] "x" "y" "z"
```


--- &twocol
## Remove objects from workspace

*** =left
You can remove an object with `rm()`:

```r
x <- 4
x
rm(x)
```

--- &twocol

## Remove objects from workspace

*** =left
You can remove an object with `rm()`:


```r
x <- 4
x
rm(x)
```

*** =right
Or remove all objects in one go:
<img src="img/Clear_workspace.png" title="plot of chunk unnamed-chunk-50" alt="plot of chunk unnamed-chunk-50" width="350px" style="display: block; margin: auto;" />

--- &slide_no_footer .segue bg:#E5E5E5

## Overview of functions you learned today

`str()`, `[`, `[[`, `$`, 

`matrix()`, `cbind()`, `nrow()`, `ncol()`, `dim`, `rownames()`, `colnames()`, `dimnames()`, 

`data.frame()`, `data.frame(stringsAsFactors = FALSE)`


--- &slide_no_footer .segue bg:#CD2626

# How do you feel now.....?

--- &vcenter

## Totally confused?
                
<img src="img/Comic_confused.png" title="plot of chunk unnamed-chunk-51" alt="plot of chunk unnamed-chunk-51" width="400px" style="display: block; margin: auto;" />

Again, try out the [online tutorial at Data Camp](https://campus.datacamp.com/courses/free-introduction-to-r/chapter-1-intro-to-basics-1?ex=1).

And go over this lecture again and do the quizzes.

---
## Totally bored?

<img src="img/Comic_bored.png" title="plot of chunk unnamed-chunk-52" alt="plot of chunk unnamed-chunk-52" width="800px" style="display: block; margin: auto;" />

Then try out the following: Calculate for the `iris` data set

- the mean sepal and petal length per species, and
- the minimum petal width for the species "setose".
- Which species has the longest sepal width?

---
## Totally content?
Then go grab a coffee, lean back and enjoy the rest of the day...!

<img src="img/Comic_hammock.png" title="plot of chunk unnamed-chunk-53" alt="plot of chunk unnamed-chunk-53" width="600px" style="display: block; margin: auto;" />


--- &thankyou