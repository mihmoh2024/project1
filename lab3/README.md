# lab3

# Информационно-аналитические технологии поиска угроз информационной безопасности

## Лабораторная работа №3

## Цель работы

1.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Исходные данные

1.  ОС Windows 10
2.  WSL2
3.  Ноутбук

## План

Проанализировать встроенные в пакет nycflights13 наборы данных с помощью
языка R и ответить на вопро- сы:

## Ход работы

``` r
library(nycflights13)
```

    Warning: пакет 'nycflights13' был собран под R версии 4.3.1

``` r
library(dplyr)
```

    Warning: пакет 'dplyr' был собран под R версии 4.3.1


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

1.Сколько встроенных в пакет nycflights13 датафреймов?

``` r
nycflights13::airlines
```

    # A tibble: 16 × 2
       carrier name                       
       <chr>   <chr>                      
     1 9E      Endeavor Air Inc.          
     2 AA      American Airlines Inc.     
     3 AS      Alaska Airlines Inc.       
     4 B6      JetBlue Airways            
     5 DL      Delta Air Lines Inc.       
     6 EV      ExpressJet Airlines Inc.   
     7 F9      Frontier Airlines Inc.     
     8 FL      AirTran Airways Corporation
     9 HA      Hawaiian Airlines Inc.     
    10 MQ      Envoy Air                  
    11 OO      SkyWest Airlines Inc.      
    12 UA      United Air Lines Inc.      
    13 US      US Airways Inc.            
    14 VX      Virgin America             
    15 WN      Southwest Airlines Co.     
    16 YV      Mesa Airlines Inc.         

``` r
nycflights13::airports
```

    # A tibble: 1,458 × 8
       faa   name                             lat    lon   alt    tz dst   tzone    
       <chr> <chr>                          <dbl>  <dbl> <dbl> <dbl> <chr> <chr>    
     1 04G   Lansdowne Airport               41.1  -80.6  1044    -5 A     America/…
     2 06A   Moton Field Municipal Airport   32.5  -85.7   264    -6 A     America/…
     3 06C   Schaumburg Regional             42.0  -88.1   801    -6 A     America/…
     4 06N   Randall Airport                 41.4  -74.4   523    -5 A     America/…
     5 09J   Jekyll Island Airport           31.1  -81.4    11    -5 A     America/…
     6 0A9   Elizabethton Municipal Airport  36.4  -82.2  1593    -5 A     America/…
     7 0G6   Williams County Airport         41.5  -84.5   730    -5 A     America/…
     8 0G7   Finger Lakes Regional Airport   42.9  -76.8   492    -5 A     America/…
     9 0P2   Shoestring Aviation Airfield    39.8  -76.6  1000    -5 U     America/…
    10 0S9   Jefferson County Intl           48.1 -123.    108    -8 A     America/…
    # ℹ 1,448 more rows

``` r
nycflights13::flights
```

    # A tibble: 336,776 × 19
        year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
       <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
     1  2013     1     1      517            515         2      830            819
     2  2013     1     1      533            529         4      850            830
     3  2013     1     1      542            540         2      923            850
     4  2013     1     1      544            545        -1     1004           1022
     5  2013     1     1      554            600        -6      812            837
     6  2013     1     1      554            558        -4      740            728
     7  2013     1     1      555            600        -5      913            854
     8  2013     1     1      557            600        -3      709            723
     9  2013     1     1      557            600        -3      838            846
    10  2013     1     1      558            600        -2      753            745
    # ℹ 336,766 more rows
    # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
    #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
    #   hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
nycflights13::planes
```

    # A tibble: 3,322 × 9
       tailnum  year type              manufacturer model engines seats speed engine
       <chr>   <int> <chr>             <chr>        <chr>   <int> <int> <int> <chr> 
     1 N10156   2004 Fixed wing multi… EMBRAER      EMB-…       2    55    NA Turbo…
     2 N102UW   1998 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
     3 N103US   1999 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
     4 N104UW   1999 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
     5 N10575   2002 Fixed wing multi… EMBRAER      EMB-…       2    55    NA Turbo…
     6 N105UW   1999 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
     7 N107US   1999 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
     8 N108UW   1999 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
     9 N109UW   1999 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
    10 N110UW   1999 Fixed wing multi… AIRBUS INDU… A320…       2   182    NA Turbo…
    # ℹ 3,312 more rows

``` r
nycflights13::weather
```

    # A tibble: 26,115 × 15
       origin  year month   day  hour  temp  dewp humid wind_dir wind_speed
       <chr>  <int> <int> <int> <int> <dbl> <dbl> <dbl>    <dbl>      <dbl>
     1 EWR     2013     1     1     1  39.0  26.1  59.4      270      10.4 
     2 EWR     2013     1     1     2  39.0  27.0  61.6      250       8.06
     3 EWR     2013     1     1     3  39.0  28.0  64.4      240      11.5 
     4 EWR     2013     1     1     4  39.9  28.0  62.2      250      12.7 
     5 EWR     2013     1     1     5  39.0  28.0  64.4      260      12.7 
     6 EWR     2013     1     1     6  37.9  28.0  67.2      240      11.5 
     7 EWR     2013     1     1     7  39.0  28.0  64.4      240      15.0 
     8 EWR     2013     1     1     8  39.9  28.0  62.2      250      10.4 
     9 EWR     2013     1     1     9  39.9  28.0  62.2      260      15.0 
    10 EWR     2013     1     1    10  41    28.0  59.6      260      13.8 
    # ℹ 26,105 more rows
    # ℹ 5 more variables: wind_gust <dbl>, precip <dbl>, pressure <dbl>,
    #   visib <dbl>, time_hour <dttm>

2.Сколько строк в каждом датафрейме?

``` r
nrow(nycflights13::airlines)
```

    [1] 16

``` r
nrow(nycflights13::airports)
```

    [1] 1458

``` r
nrow(nycflights13::flights)
```

    [1] 336776

``` r
nrow(nycflights13::planes)
```

    [1] 3322

``` r
nrow(nycflights13::weather)
```

    [1] 26115

3.Сколько столбцов в каждом датафрейме?

``` r
ncol(nycflights13::airlines)
```

    [1] 2

``` r
ncol(nycflights13::airports)
```

    [1] 8

``` r
ncol(nycflights13::flights)
```

    [1] 19

``` r
ncol(nycflights13::planes)
```

    [1] 9

``` r
ncol(nycflights13::weather)
```

    [1] 15

4.Как просмотреть примерный вид датафрейма?

``` r
nycflights13::airlines %>% glimpse()
```

    Rows: 16
    Columns: 2
    $ carrier <chr> "9E", "AA", "AS", "B6", "DL", "EV", "F9", "FL", "HA", "MQ", "O…
    $ name    <chr> "Endeavor Air Inc.", "American Airlines Inc.", "Alaska Airline…

``` r
nycflights13::airports %>% glimpse()
```

    Rows: 1,458
    Columns: 8
    $ faa   <chr> "04G", "06A", "06C", "06N", "09J", "0A9", "0G6", "0G7", "0P2", "…
    $ name  <chr> "Lansdowne Airport", "Moton Field Municipal Airport", "Schaumbur…
    $ lat   <dbl> 41.13047, 32.46057, 41.98934, 41.43191, 31.07447, 36.37122, 41.4…
    $ lon   <dbl> -80.61958, -85.68003, -88.10124, -74.39156, -81.42778, -82.17342…
    $ alt   <dbl> 1044, 264, 801, 523, 11, 1593, 730, 492, 1000, 108, 409, 875, 10…
    $ tz    <dbl> -5, -6, -6, -5, -5, -5, -5, -5, -5, -8, -5, -6, -5, -5, -5, -5, …
    $ dst   <chr> "A", "A", "A", "A", "A", "A", "A", "A", "U", "A", "A", "U", "A",…
    $ tzone <chr> "America/New_York", "America/Chicago", "America/Chicago", "Ameri…

``` r
nycflights13::flights %>% glimpse()
```

    Rows: 336,776
    Columns: 19
    $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2…
    $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, …
    $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, …
    $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1…
    $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,…
    $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,…
    $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1…
    $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "…
    $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4…
    $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394…
    $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",…
    $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",…
    $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1…
    $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, …
    $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6…
    $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0…
    $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0…

``` r
nycflights13::planes %>% glimpse()
```

    Rows: 3,322
    Columns: 9
    $ tailnum      <chr> "N10156", "N102UW", "N103US", "N104UW", "N10575", "N105UW…
    $ year         <int> 2004, 1998, 1999, 1999, 2002, 1999, 1999, 1999, 1999, 199…
    $ type         <chr> "Fixed wing multi engine", "Fixed wing multi engine", "Fi…
    $ manufacturer <chr> "EMBRAER", "AIRBUS INDUSTRIE", "AIRBUS INDUSTRIE", "AIRBU…
    $ model        <chr> "EMB-145XR", "A320-214", "A320-214", "A320-214", "EMB-145…
    $ engines      <int> 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    $ seats        <int> 55, 182, 182, 182, 55, 182, 182, 182, 182, 182, 55, 55, 5…
    $ speed        <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ engine       <chr> "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turb…

``` r
nycflights13::weather %>% glimpse()
```

    Rows: 26,115
    Columns: 15
    $ origin     <chr> "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EW…
    $ year       <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,…
    $ month      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    $ day        <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    $ hour       <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 13, 14, 15, 16, 17, 18, …
    $ temp       <dbl> 39.02, 39.02, 39.02, 39.92, 39.02, 37.94, 39.02, 39.92, 39.…
    $ dewp       <dbl> 26.06, 26.96, 28.04, 28.04, 28.04, 28.04, 28.04, 28.04, 28.…
    $ humid      <dbl> 59.37, 61.63, 64.43, 62.21, 64.43, 67.21, 64.43, 62.21, 62.…
    $ wind_dir   <dbl> 270, 250, 240, 250, 260, 240, 240, 250, 260, 260, 260, 330,…
    $ wind_speed <dbl> 10.35702, 8.05546, 11.50780, 12.65858, 12.65858, 11.50780, …
    $ wind_gust  <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 20.…
    $ precip     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
    $ pressure   <dbl> 1012.0, 1012.3, 1012.5, 1012.2, 1011.9, 1012.4, 1012.2, 101…
    $ visib      <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10,…
    $ time_hour  <dttm> 2013-01-01 01:00:00, 2013-01-01 02:00:00, 2013-01-01 03:00…

5.Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных
(представлено в наборах дан- ных)?

``` r
length(airlines$carrier)
```

    [1] 16

6.Сколько рейсов принял аэропорт John F Kennedy Intl в мае?

``` r
filter(airports,name == "John F Kennedy Intl")
```

    # A tibble: 1 × 8
      faa   name                  lat   lon   alt    tz dst   tzone           
      <chr> <chr>               <dbl> <dbl> <dbl> <dbl> <chr> <chr>           
    1 JFK   John F Kennedy Intl  40.6 -73.8    13    -5 A     America/New_York

``` r
filter(flights,dest == "JFK",month == 5)
```

    # A tibble: 0 × 19
    # ℹ 19 variables: year <int>, month <int>, day <int>, dep_time <int>,
    #   sched_dep_time <int>, dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>, carrier <chr>, flight <int>,
    #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
    #   hour <dbl>, minute <dbl>, time_hour <dttm>

7.Какой самый северный аэропорт?

``` r
filter(airports,lat == max(airports$lat))
```

    # A tibble: 1 × 8
      faa   name                      lat   lon   alt    tz dst   tzone
      <chr> <chr>                   <dbl> <dbl> <dbl> <dbl> <chr> <chr>
    1 EEN   Dillant Hopkins Airport  72.3  42.9   149    -5 A     <NA> 

8.Какой аэропорт самый высокогорный (находится выше всех над уровнем
моря)?

``` r
filter(airports,alt == max(airports$alt))
```

    # A tibble: 1 × 8
      faa   name        lat   lon   alt    tz dst   tzone         
      <chr> <chr>     <dbl> <dbl> <dbl> <dbl> <chr> <chr>         
    1 TEX   Telluride  38.0 -108.  9078    -7 A     America/Denver

9.Какие бортовые номера у самых старых самолетов?

``` r
head(arrange(planes, year),n=10)
```

    # A tibble: 10 × 9
       tailnum  year type              manufacturer model engines seats speed engine
       <chr>   <int> <chr>             <chr>        <chr>   <int> <int> <int> <chr> 
     1 N381AA   1956 Fixed wing multi… DOUGLAS      DC-7…       4   102   232 Recip…
     2 N201AA   1959 Fixed wing singl… CESSNA       150         1     2    90 Recip…
     3 N567AA   1959 Fixed wing singl… DEHAVILLAND  OTTE…       1    16    95 Recip…
     4 N378AA   1963 Fixed wing singl… CESSNA       172E        1     4   105 Recip…
     5 N575AA   1963 Fixed wing singl… CESSNA       210-…       1     6    NA Recip…
     6 N14629   1965 Fixed wing multi… BOEING       737-…       2   149    NA Turbo…
     7 N615AA   1967 Fixed wing multi… BEECH        65-A…       2     9   202 Turbo…
     8 N425AA   1968 Fixed wing singl… PIPER        PA-2…       1     4   107 Recip…
     9 N383AA   1972 Fixed wing multi… BEECH        E-90        2    10    NA Turbo…
    10 N364AA   1973 Fixed wing multi… CESSNA       310Q        2     6   167 Recip…

10.Какая средняя температура воздуха была в сентябре в аэропорту John F
Kennedy Intl (в градусах Цельсия).

``` r
nycflights13::weather %>%
  filter(month == 9,origin == "JFK") %>%
  summarise("temp" = ((temp = mean(temp,0))-32)*5/9)
```

    # A tibble: 1 × 1
       temp
      <dbl>
    1  19.4

11.Самолеты какой авиакомпании совершили больше всего вылетов в июне?

``` r
polet <- nycflights13::flights %>%
  group_by(carrier) %>%
  summarise('polet' = n())
top1 <- head(arrange(polet,desc(polet)),n=1)
filter(nycflights13::airlines,carrier == top1$carrier)
```

    # A tibble: 1 × 2
      carrier name                 
      <chr>   <chr>                
    1 UA      United Air Lines Inc.

12.Самолеты какой авиакомпании задерживались чаще других в 2013 году?

``` r
polet2 <- nycflights13::flights %>%
  group_by(carrier) %>%
  filter(dep_delay > 0, arr_delay > 0) %>%
  summarise('polet' = n())
top2 <- head(arrange(polet2,desc(polet)),n=1)
filter(nycflights13::airlines,carrier == top2$carrier)
```

    # A tibble: 1 × 2
      carrier name                    
      <chr>   <chr>                   
    1 EV      ExpressJet Airlines Inc.
