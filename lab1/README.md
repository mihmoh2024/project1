# LAB1
Смирнов Михаил

# Информационно-аналитические технологии поиска угроз информационной безопасности

## Лабораторная работа №1

## Цель работы

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Развить навыки работы в Rstudio IDE: установка пакетов работа с
    проектами в Rstudio настройка и работа с Git
3.  Закрепить знания базовых типов данных языка R и простейших операций
    с ними

## Исходные данные

1.  ОС Windows 10
2.  WSL2
3.  Ноутбук

## План

Используя программный пакет swirl, освоить базовые операции в языке
программирования R.

## Ход работы

``` r
5+7
```

    [1] 12

``` r
x <-5+7
x
```

    [1] 12

``` r
y <-x-3
y
```

    [1] 9

``` r
z<-c(1.1,9,3.14)
z
```

    [1] 1.10 9.00 3.14

``` r
z<-555
c(z,555,z)
```

    [1] 555 555 555

``` r
z*2+100
```

    [1] 1210

``` r
my_sqrt<-sqrt(z-1)
my_sqrt
```

    [1] 23.5372

``` r
my_div <- z / my_sqrt
z * 2 + 1000
```

    [1] 2110

## 2 | In this lesson, you’ll learn how to examine your local workspace in R and begin to explore the

##| relationship between your workspace and the file system of your
machine.

``` r
getwd()
```

    [1] "C:/Users/mihmo/OneDrive/pr1/lab1"

``` r
ls()
```

    [1] "has_annotations" "my_div"          "my_sqrt"         "x"              
    [5] "y"               "z"              

``` r
x<-9
ls()
```

    [1] "has_annotations" "my_div"          "my_sqrt"         "x"              
    [5] "y"               "z"              

``` r
list.files()
```

    [1] "lab1.qmd"       "lab1.rmarkdown" "README.md"      "testdir"       

``` r
?list.files
```

    запускаю httpd сервер помощи... готово

``` r
args(list.files)
```

    function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE, 
        recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE, 
        no.. = FALSE) 
    NULL

``` r
old.dir <- getwd()
dir.create("testdir")
```

    Warning in dir.create("testdir"): 'testdir' уже существует

``` r
setwd("testdir")
file.create("mytest.R")
```

    [1] TRUE

``` r
list.files
```

    function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE, 
        recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE, 
        no.. = FALSE) 
    .Internal(list.files(path, pattern, all.files, full.names, recursive, 
        ignore.case, include.dirs, no..))
    <bytecode: 0x000001f9b69f85f0>
    <environment: namespace:base>

``` r
file.exists("mytest.R")
```

    [1] TRUE

``` r
file.info("mytest.R")
```

             size isdir mode               mtime               ctime
    mytest.R    0 FALSE  666 2023-10-05 11:49:18 2023-10-05 11:49:18
                           atime exe
    mytest.R 2023-10-05 11:49:18  no

``` r
file.rename("mytest.R","mytest2.R")
```

    [1] TRUE

``` r
file.copy("mytest2.R", "mytest3.R")
```

    [1] FALSE

``` r
file.path("mytest3.R")
```

    [1] "mytest3.R"

``` r
file.path("folder1", "folder2")
```

    [1] "folder1/folder2"

``` r
dir.create(file.path("testdir2","testdir3"),recursive = TRUE)
```

    Warning in dir.create(file.path("testdir2", "testdir3"), recursive = TRUE):
    'testdir2\testdir3' уже существует

``` r
setwd(old.dir)
```

## 3 | In this lesson, you’ll learn how to create sequences of numbers in R.

``` r
1:20
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

``` r
pi:10
```

    [1] 3.141593 4.141593 5.141593 6.141593 7.141593 8.141593 9.141593

``` r
15:1
```

     [1] 15 14 13 12 11 10  9  8  7  6  5  4  3  2  1

``` r
seq(1,20)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

``` r
seq(0, 10, by=0.5)
```

     [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0
    [16]  7.5  8.0  8.5  9.0  9.5 10.0

``` r
seq(5, 10, length=30)
```

     [1]  5.000000  5.172414  5.344828  5.517241  5.689655  5.862069  6.034483
     [8]  6.206897  6.379310  6.551724  6.724138  6.896552  7.068966  7.241379
    [15]  7.413793  7.586207  7.758621  7.931034  8.103448  8.275862  8.448276
    [22]  8.620690  8.793103  8.965517  9.137931  9.310345  9.482759  9.655172
    [29]  9.827586 10.000000

``` r
my_seq <- seq(5, 10, length=30)
length(my_seq)
```

    [1] 30

``` r
1:length(my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

``` r
seq(along.with = my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

``` r
seq_along(my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

``` r
rep(0, times = 40)
```

     [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
    [39] 0 0

``` r
rep(c(0, 1, 2), times = 10)
```

     [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2

``` r
rep(c(0, 1, 2), each = 10)
```

     [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2

## 4 | The simplest and most common data structure in R is the vector.

``` r
num_vect <- c(0.5,55,-10,6)
num_vect < 1
```

    [1]  TRUE FALSE  TRUE FALSE

``` r
tf <- num_vect < 1
tf
```

    [1]  TRUE FALSE  TRUE FALSE

``` r
num_vect >= 6
```

    [1] FALSE  TRUE FALSE  TRUE

``` r
my_char <- c("My","name","is")
my_char
```

    [1] "My"   "name" "is"  

``` r
paste(my_char, collapse = " ")
```

    [1] "My name is"

``` r
c(my_char, "Mikhail")
```

    [1] "My"      "name"    "is"      "Mikhail"

``` r
my_name <- c(my_char, "Mikhail")
my_name
```

    [1] "My"      "name"    "is"      "Mikhail"

``` r
paste(my_name,collapse = " ")
```

    [1] "My name is Mikhail"

``` r
paste("Hello", "world!", sep = " ")
```

    [1] "Hello world!"

``` r
paste(1:3, c("X", "Y", "Z"), sep = "")
```

    [1] "1X" "2Y" "3Z"

``` r
paste(LETTERS, 1:4, sep = "-")
```

     [1] "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4"
    [13] "M-1" "N-2" "O-3" "P-4" "Q-1" "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4"
    [25] "Y-1" "Z-2"
