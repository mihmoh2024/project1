# LAB1

Смирнов Михаил

``` r
5+7
```

```         
[1] 12
```

``` r
x <-5+7
x
```

```         
[1] 12
```

``` r
y <-x-3
y
```

```         
[1] 9
```

``` r
z<-c(1.1,9,3.14)
z
```

```         
[1] 1.10 9.00 3.14
```

``` r
z<-555
c(z,555,z)
```

```         
[1] 555 555 555
```

``` r
z*2+100
```

```         
[1] 1210
```

``` r
my_sqrt<-sqrt(z-1)
my_sqrt
```

```         
[1] 23.5372
```

``` r
my_div <- z / my_sqrt
z * 2 + 1000
```

```         
[1] 2110
```

## 2 \| In this lesson, you'll learn how to examine your local workspace in R and begin to explore the

##\| relationship between your workspace and the file system of your machine.

``` r
getwd()
```

```         
[1] "C:/Users/mihmo/OneDrive/pr1/lab1"
```

``` r
ls()
```

```         
[1] "has_annotations" "my_div"          "my_sqrt"         "x"              
[5] "y"               "z"              
```

``` r
x<-9
ls()
```

```         
[1] "has_annotations" "my_div"          "my_sqrt"         "x"              
[5] "y"               "z"              
```

``` r
list.files()
```

```         
[1] "lab1.qmd"       "lab1.rmarkdown" "README.html"    "README.md"     
```

``` r
?list.files
```

```         
запускаю httpd сервер помощи... готово
```

``` r
args(list.files)
```

```         
function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE, 
    recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE, 
    no.. = FALSE) 
NULL
```

``` r
old.dir <- getwd()
dir.create("testdir")
setwd("testdir")
file.create("mytest.R")
```

```         
[1] TRUE
```

``` r
list.files
```

```         
function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE, 
    recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE, 
    no.. = FALSE) 
.Internal(list.files(path, pattern, all.files, full.names, recursive, 
    ignore.case, include.dirs, no..))
<bytecode: 0x000002194cd2a018>
<environment: namespace:base>
```

``` r
file.exists("mytest.R")
```

```         
[1] TRUE
```

``` r
file.info("mytest.R")
```

```         
         size isdir mode               mtime               ctime
mytest.R    0 FALSE  666 2023-09-21 11:37:52 2023-09-21 11:37:52
                       atime exe
mytest.R 2023-09-21 11:37:52  no
```

``` r
file.rename("mytest.R","mytest2.R")
```

```         
[1] TRUE
```

``` r
file.copy("mytest2.R", "mytest3.R")
```

```         
[1] TRUE
```

``` r
file.path("mytest3.R")
```

```         
[1] "mytest3.R"
```

``` r
file.path("folder1", "folder2")
```

```         
[1] "folder1/folder2"
```

``` r
dir.create(file.path("testdir2","testdir3"),recursive = TRUE)
setwd(old.dir)
```

## 3 \| In this lesson, you'll learn how to create sequences of numbers in R.

``` r
1:20
```

```         
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
```
