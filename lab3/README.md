# Основы обраотки данных с помощью R и Dplyr
Выполнено Кашинцевой Алиной Евгеньевной (l1ndo888@yandex.ru)

# Лабораторная работа №3

## Цель работы

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить практические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Ход выполнения работы

Загружаем необходимые библиотеки:

::: {.cell}

``` r
library(dplyr)
```

::: {.cell-output .cell-output-stderr}


    Присоединяю пакет: 'dplyr'

:::

::: {.cell-output .cell-output-stderr}

    Следующие объекты скрыты от 'package:stats':

        filter, lag

:::

::: {.cell-output .cell-output-stderr}

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

:::

``` r
library(nycflights13)
```

:::

Анализ наборов данных, встроенных в пакет `nycflights13`, с помощью R.

Сколько встроенных в пакет nycflights13 датафреймов?

::: {.cell}

``` r
data(package = "nycflights13")$results[, "Item"]
```

::: {.cell-output .cell-output-stdout}

    [1] "airlines" "airports" "flights"  "planes"   "weather" 

::: :::

Сколько строк в каждом датафрейме?

::: {.cell}

``` r
list(
  flights = nrow(flights),
  airlines = nrow(airlines),
  airports = nrow(airports),
  planes = nrow(planes),
  weather = nrow(weather)
)
```

::: {.cell-output .cell-output-stdout}

    $flights
    [1] 336776

    $airlines
    [1] 16

    $airports
    [1] 1458

    $planes
    [1] 3322

    $weather
    [1] 26115

::: :::

Сколько столбцов в каждом датафрейме?

::: {.cell}

``` r
list(
  flights = ncol(flights),
  airlines = ncol(airlines),
  airports = ncol(airports),
  planes = ncol(planes),
  weather = ncol(weather)
)
```

::: {.cell-output .cell-output-stdout}

    $flights
    [1] 19

    $airlines
    [1] 2

    $airports
    [1] 8

    $planes
    [1] 9

    $weather
    [1] 15

::: :::

Как просмотреть примерный вид датафрейма?

::: {.cell}

``` r
flights %>% glimpse()
```

::: {.cell-output .cell-output-stdout}

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

::: :::

Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных?

::: {.cell}

``` r
length(unique(flights$carrier))
```

::: {.cell-output .cell-output-stdout}

    [1] 16

::: :::

Сколько рейсов принял аэропорт John F Kennedy Intl в мае?

::: {.cell}

``` r
flights %>%
  filter(dest == "JFK", month == 5) %>%
  nrow()
```

::: {.cell-output .cell-output-stdout}

    [1] 0

::: :::

Какой самый северный аэропорт?

::: {.cell}

``` r
airports %>%
  arrange(desc(lat)) %>%
  select(name, lat) %>%
  head(1)
```

::: {.cell-output .cell-output-stdout}

    # A tibble: 1 × 2
      name                      lat
      <chr>                   <dbl>
    1 Dillant Hopkins Airport  72.3

::: :::

Какой аэропорт самый высокогорный (находится выше всех над уровнем
моря)?

::: {.cell}

``` r
airports %>%
  arrange(desc(alt)) %>%
  select(name, alt) %>%
  head(1)
```

::: {.cell-output .cell-output-stdout}

    # A tibble: 1 × 2
      name        alt
      <chr>     <dbl>
    1 Telluride  9078

::: :::

Какие бортовые номера у самых старых самолетов?

::: {.cell}

``` r
planes %>%
  arrange(year) %>%
  select(tailnum, year) %>%
  head(5)
```

::: {.cell-output .cell-output-stdout}

    # A tibble: 5 × 2
      tailnum  year
      <chr>   <int>
    1 N381AA   1956
    2 N201AA   1959
    3 N567AA   1959
    4 N378AA   1963
    5 N575AA   1963

::: :::

Какая средняя температура воздуха была в сентябре в аэропорту John F
Kennedy Intl?

::: {.cell}

``` r
weather %>%
  filter(origin == "JFK", month == 9) %>%
  summarise(mean_temp_C = mean((temp - 32) * 5/9, na.rm = TRUE))
```

::: {.cell-output .cell-output-stdout}

    # A tibble: 1 × 1
      mean_temp_C
            <dbl>
    1        19.4

::: :::

Самолеты какой авиакомпании совершили больше всего вылетов в июне?

::: {.cell}

``` r
flights %>%
  filter(month == 6) %>%
  group_by(carrier) %>%
  summarise(flight_count = n()) %>%
  arrange(desc(flight_count)) %>%
  head(1)
```

::: {.cell-output .cell-output-stdout}

    # A tibble: 1 × 2
      carrier flight_count
      <chr>          <int>
    1 UA              4975

::: :::

Самолеты какой авиакомпании задерживались чаще других в 2013 году?

::: {.cell}

``` r
flights %>%
  group_by(carrier) %>%
  summarise(avg_delay = mean(arr_delay, na.rm = TRUE)) %>%
  arrange(desc(avg_delay)) %>%
  head(1)
```

::: {.cell-output .cell-output-stdout}

    # A tibble: 1 × 2
      carrier avg_delay
      <chr>       <dbl>
    1 F9           21.9

::: :::

## Вывод

В ходе выполнения данной лабораторной раоты был проведён анализ наборов
данных, встроенных в пакет `nycflights13`, и даны ответы на заданные
вопросы