# Основы обраотки данных с помощью R и Dplyr
Выполнено Кашинцевой Алиной Евгеньевной (l1ndo888@yandex.ru)

# Лабораторная работа №2

## Цель работы

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить практические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Ход выполнения работы

Загружаем необходимые библиотеки

``` r
library(dplyr)
```


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

``` r
library(knitr)
```

Анализ набора данных `starwars`, встроенного в пакет `dplyr`.

1.  Сколько строк в датафрейме?

``` r
starwars %>% nrow()
```

    [1] 87

1.  Сколько столбцов в датафрейме?

``` r
starwars %>% ncol()
```

    [1] 14

1.  Как просмотреть примерный вид датафрейма?

``` r
starwars %>% glimpse()
```

    Rows: 87
    Columns: 14
    $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia Or…
    $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180, 2…
    $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, 77.…
    $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown", N…
    $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light", "…
    $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blue",…
    $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57.0, …
    $ sex        <chr> "male", "none", "none", "male", "female", "male", "female",…
    $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "femini…
    $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan", "T…
    $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "Huma…
    $ films      <list> <"A New Hope", "The Empire Strikes Back", "Return of the J…
    $ vehicles   <list> <"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, "Imp…
    $ starships  <list> <"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced x1",…

1.  Сколько уникальных рас персонажей (species) представлено в данных?

``` r
starwars %>%
  distinct(species) %>%
  nrow()
```

    [1] 38

1.  Найти самого высокого персонажа.

``` r
starwars %>%
  arrange(desc(height)) %>%
  slice_head(n = 1) %>%
  select(name, height)
```

    # A tibble: 1 × 2
      name        height
      <chr>        <int>
    1 Yarael Poof    264

1.  Найти всех персонажей ниже 170.

``` r
starwars %>%
  filter(height < 170) %>%
  select(name, height) %>%
  kable
```

<table>
<thead>
<tr class="header">
<th style="text-align: left;">name</th>
<th style="text-align: right;">height</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">C-3PO</td>
<td style="text-align: right;">167</td>
</tr>
<tr class="even">
<td style="text-align: left;">R2-D2</td>
<td style="text-align: right;">96</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Leia Organa</td>
<td style="text-align: right;">150</td>
</tr>
<tr class="even">
<td style="text-align: left;">Beru Whitesun Lars</td>
<td style="text-align: right;">165</td>
</tr>
<tr class="odd">
<td style="text-align: left;">R5-D4</td>
<td style="text-align: right;">97</td>
</tr>
<tr class="even">
<td style="text-align: left;">Yoda</td>
<td style="text-align: right;">66</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Mon Mothma</td>
<td style="text-align: right;">150</td>
</tr>
<tr class="even">
<td style="text-align: left;">Wicket Systri Warrick</td>
<td style="text-align: right;">88</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Nien Nunb</td>
<td style="text-align: right;">160</td>
</tr>
<tr class="even">
<td style="text-align: left;">Watto</td>
<td style="text-align: right;">137</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Sebulba</td>
<td style="text-align: right;">112</td>
</tr>
<tr class="even">
<td style="text-align: left;">Shmi Skywalker</td>
<td style="text-align: right;">163</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Ratts Tyerel</td>
<td style="text-align: right;">79</td>
</tr>
<tr class="even">
<td style="text-align: left;">Dud Bolt</td>
<td style="text-align: right;">94</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gasgano</td>
<td style="text-align: right;">122</td>
</tr>
<tr class="even">
<td style="text-align: left;">Ben Quadinaros</td>
<td style="text-align: right;">163</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Cordé</td>
<td style="text-align: right;">157</td>
</tr>
<tr class="even">
<td style="text-align: left;">Barriss Offee</td>
<td style="text-align: right;">166</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Dormé</td>
<td style="text-align: right;">165</td>
</tr>
<tr class="even">
<td style="text-align: left;">Zam Wesell</td>
<td style="text-align: right;">168</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Jocasta Nu</td>
<td style="text-align: right;">167</td>
</tr>
<tr class="even">
<td style="text-align: left;">R4-P17</td>
<td style="text-align: right;">96</td>
</tr>
</tbody>
</table>

1.  Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ
    подсчитать по формуле.

``` r
starwars %>%
  mutate(bmi = mass / (height / 100)^2) %>%
  select(name, height, mass, bmi) %>%
  kable()
```

<table>
<thead>
<tr class="header">
<th style="text-align: left;">name</th>
<th style="text-align: right;">height</th>
<th style="text-align: right;">mass</th>
<th style="text-align: right;">bmi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Luke Skywalker</td>
<td style="text-align: right;">172</td>
<td style="text-align: right;">77.0</td>
<td style="text-align: right;">26.02758</td>
</tr>
<tr class="even">
<td style="text-align: left;">C-3PO</td>
<td style="text-align: right;">167</td>
<td style="text-align: right;">75.0</td>
<td style="text-align: right;">26.89232</td>
</tr>
<tr class="odd">
<td style="text-align: left;">R2-D2</td>
<td style="text-align: right;">96</td>
<td style="text-align: right;">32.0</td>
<td style="text-align: right;">34.72222</td>
</tr>
<tr class="even">
<td style="text-align: left;">Darth Vader</td>
<td style="text-align: right;">202</td>
<td style="text-align: right;">136.0</td>
<td style="text-align: right;">33.33007</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Leia Organa</td>
<td style="text-align: right;">150</td>
<td style="text-align: right;">49.0</td>
<td style="text-align: right;">21.77778</td>
</tr>
<tr class="even">
<td style="text-align: left;">Owen Lars</td>
<td style="text-align: right;">178</td>
<td style="text-align: right;">120.0</td>
<td style="text-align: right;">37.87401</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Beru Whitesun Lars</td>
<td style="text-align: right;">165</td>
<td style="text-align: right;">75.0</td>
<td style="text-align: right;">27.54821</td>
</tr>
<tr class="even">
<td style="text-align: left;">R5-D4</td>
<td style="text-align: right;">97</td>
<td style="text-align: right;">32.0</td>
<td style="text-align: right;">34.00999</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Biggs Darklighter</td>
<td style="text-align: right;">183</td>
<td style="text-align: right;">84.0</td>
<td style="text-align: right;">25.08286</td>
</tr>
<tr class="even">
<td style="text-align: left;">Obi-Wan Kenobi</td>
<td style="text-align: right;">182</td>
<td style="text-align: right;">77.0</td>
<td style="text-align: right;">23.24598</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Anakin Skywalker</td>
<td style="text-align: right;">188</td>
<td style="text-align: right;">84.0</td>
<td style="text-align: right;">23.76641</td>
</tr>
<tr class="even">
<td style="text-align: left;">Wilhuff Tarkin</td>
<td style="text-align: right;">180</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Chewbacca</td>
<td style="text-align: right;">228</td>
<td style="text-align: right;">112.0</td>
<td style="text-align: right;">21.54509</td>
</tr>
<tr class="even">
<td style="text-align: left;">Han Solo</td>
<td style="text-align: right;">180</td>
<td style="text-align: right;">80.0</td>
<td style="text-align: right;">24.69136</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Greedo</td>
<td style="text-align: right;">173</td>
<td style="text-align: right;">74.0</td>
<td style="text-align: right;">24.72518</td>
</tr>
<tr class="even">
<td style="text-align: left;">Jabba Desilijic Tiure</td>
<td style="text-align: right;">175</td>
<td style="text-align: right;">1358.0</td>
<td style="text-align: right;">443.42857</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Wedge Antilles</td>
<td style="text-align: right;">170</td>
<td style="text-align: right;">77.0</td>
<td style="text-align: right;">26.64360</td>
</tr>
<tr class="even">
<td style="text-align: left;">Jek Tono Porkins</td>
<td style="text-align: right;">180</td>
<td style="text-align: right;">110.0</td>
<td style="text-align: right;">33.95062</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Yoda</td>
<td style="text-align: right;">66</td>
<td style="text-align: right;">17.0</td>
<td style="text-align: right;">39.02663</td>
</tr>
<tr class="even">
<td style="text-align: left;">Palpatine</td>
<td style="text-align: right;">170</td>
<td style="text-align: right;">75.0</td>
<td style="text-align: right;">25.95156</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Boba Fett</td>
<td style="text-align: right;">183</td>
<td style="text-align: right;">78.2</td>
<td style="text-align: right;">23.35095</td>
</tr>
<tr class="even">
<td style="text-align: left;">IG-88</td>
<td style="text-align: right;">200</td>
<td style="text-align: right;">140.0</td>
<td style="text-align: right;">35.00000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Bossk</td>
<td style="text-align: right;">190</td>
<td style="text-align: right;">113.0</td>
<td style="text-align: right;">31.30194</td>
</tr>
<tr class="even">
<td style="text-align: left;">Lando Calrissian</td>
<td style="text-align: right;">177</td>
<td style="text-align: right;">79.0</td>
<td style="text-align: right;">25.21625</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Lobot</td>
<td style="text-align: right;">175</td>
<td style="text-align: right;">79.0</td>
<td style="text-align: right;">25.79592</td>
</tr>
<tr class="even">
<td style="text-align: left;">Ackbar</td>
<td style="text-align: right;">180</td>
<td style="text-align: right;">83.0</td>
<td style="text-align: right;">25.61728</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Mon Mothma</td>
<td style="text-align: right;">150</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Arvel Crynyd</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Wicket Systri Warrick</td>
<td style="text-align: right;">88</td>
<td style="text-align: right;">20.0</td>
<td style="text-align: right;">25.82645</td>
</tr>
<tr class="even">
<td style="text-align: left;">Nien Nunb</td>
<td style="text-align: right;">160</td>
<td style="text-align: right;">68.0</td>
<td style="text-align: right;">26.56250</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Qui-Gon Jinn</td>
<td style="text-align: right;">193</td>
<td style="text-align: right;">89.0</td>
<td style="text-align: right;">23.89326</td>
</tr>
<tr class="even">
<td style="text-align: left;">Nute Gunray</td>
<td style="text-align: right;">191</td>
<td style="text-align: right;">90.0</td>
<td style="text-align: right;">24.67038</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Finis Valorum</td>
<td style="text-align: right;">170</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Padmé Amidala</td>
<td style="text-align: right;">185</td>
<td style="text-align: right;">45.0</td>
<td style="text-align: right;">13.14828</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Jar Jar Binks</td>
<td style="text-align: right;">196</td>
<td style="text-align: right;">66.0</td>
<td style="text-align: right;">17.18034</td>
</tr>
<tr class="even">
<td style="text-align: left;">Roos Tarpals</td>
<td style="text-align: right;">224</td>
<td style="text-align: right;">82.0</td>
<td style="text-align: right;">16.34247</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Rugor Nass</td>
<td style="text-align: right;">206</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Ric Olié</td>
<td style="text-align: right;">183</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Watto</td>
<td style="text-align: right;">137</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Sebulba</td>
<td style="text-align: right;">112</td>
<td style="text-align: right;">40.0</td>
<td style="text-align: right;">31.88776</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Quarsh Panaka</td>
<td style="text-align: right;">183</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Shmi Skywalker</td>
<td style="text-align: right;">163</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Darth Maul</td>
<td style="text-align: right;">175</td>
<td style="text-align: right;">80.0</td>
<td style="text-align: right;">26.12245</td>
</tr>
<tr class="even">
<td style="text-align: left;">Bib Fortuna</td>
<td style="text-align: right;">180</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Ayla Secura</td>
<td style="text-align: right;">178</td>
<td style="text-align: right;">55.0</td>
<td style="text-align: right;">17.35892</td>
</tr>
<tr class="even">
<td style="text-align: left;">Ratts Tyerel</td>
<td style="text-align: right;">79</td>
<td style="text-align: right;">15.0</td>
<td style="text-align: right;">24.03461</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Dud Bolt</td>
<td style="text-align: right;">94</td>
<td style="text-align: right;">45.0</td>
<td style="text-align: right;">50.92802</td>
</tr>
<tr class="even">
<td style="text-align: left;">Gasgano</td>
<td style="text-align: right;">122</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Ben Quadinaros</td>
<td style="text-align: right;">163</td>
<td style="text-align: right;">65.0</td>
<td style="text-align: right;">24.46460</td>
</tr>
<tr class="even">
<td style="text-align: left;">Mace Windu</td>
<td style="text-align: right;">188</td>
<td style="text-align: right;">84.0</td>
<td style="text-align: right;">23.76641</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Ki-Adi-Mundi</td>
<td style="text-align: right;">198</td>
<td style="text-align: right;">82.0</td>
<td style="text-align: right;">20.91623</td>
</tr>
<tr class="even">
<td style="text-align: left;">Kit Fisto</td>
<td style="text-align: right;">196</td>
<td style="text-align: right;">87.0</td>
<td style="text-align: right;">22.64681</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Eeth Koth</td>
<td style="text-align: right;">171</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Adi Gallia</td>
<td style="text-align: right;">184</td>
<td style="text-align: right;">50.0</td>
<td style="text-align: right;">14.76843</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Saesee Tiin</td>
<td style="text-align: right;">188</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Yarael Poof</td>
<td style="text-align: right;">264</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Plo Koon</td>
<td style="text-align: right;">188</td>
<td style="text-align: right;">80.0</td>
<td style="text-align: right;">22.63468</td>
</tr>
<tr class="even">
<td style="text-align: left;">Mas Amedda</td>
<td style="text-align: right;">196</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gregar Typho</td>
<td style="text-align: right;">185</td>
<td style="text-align: right;">85.0</td>
<td style="text-align: right;">24.83565</td>
</tr>
<tr class="even">
<td style="text-align: left;">Cordé</td>
<td style="text-align: right;">157</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Cliegg Lars</td>
<td style="text-align: right;">183</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Poggle the Lesser</td>
<td style="text-align: right;">183</td>
<td style="text-align: right;">80.0</td>
<td style="text-align: right;">23.88844</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Luminara Unduli</td>
<td style="text-align: right;">170</td>
<td style="text-align: right;">56.2</td>
<td style="text-align: right;">19.44637</td>
</tr>
<tr class="even">
<td style="text-align: left;">Barriss Offee</td>
<td style="text-align: right;">166</td>
<td style="text-align: right;">50.0</td>
<td style="text-align: right;">18.14487</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Dormé</td>
<td style="text-align: right;">165</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Dooku</td>
<td style="text-align: right;">193</td>
<td style="text-align: right;">80.0</td>
<td style="text-align: right;">21.47709</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Bail Prestor Organa</td>
<td style="text-align: right;">191</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Jango Fett</td>
<td style="text-align: right;">183</td>
<td style="text-align: right;">79.0</td>
<td style="text-align: right;">23.58984</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Zam Wesell</td>
<td style="text-align: right;">168</td>
<td style="text-align: right;">55.0</td>
<td style="text-align: right;">19.48696</td>
</tr>
<tr class="even">
<td style="text-align: left;">Dexter Jettster</td>
<td style="text-align: right;">198</td>
<td style="text-align: right;">102.0</td>
<td style="text-align: right;">26.01775</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Lama Su</td>
<td style="text-align: right;">229</td>
<td style="text-align: right;">88.0</td>
<td style="text-align: right;">16.78076</td>
</tr>
<tr class="even">
<td style="text-align: left;">Taun We</td>
<td style="text-align: right;">213</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Jocasta Nu</td>
<td style="text-align: right;">167</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">R4-P17</td>
<td style="text-align: right;">96</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Wat Tambor</td>
<td style="text-align: right;">193</td>
<td style="text-align: right;">48.0</td>
<td style="text-align: right;">12.88625</td>
</tr>
<tr class="even">
<td style="text-align: left;">San Hill</td>
<td style="text-align: right;">191</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Shaak Ti</td>
<td style="text-align: right;">178</td>
<td style="text-align: right;">57.0</td>
<td style="text-align: right;">17.99015</td>
</tr>
<tr class="even">
<td style="text-align: left;">Grievous</td>
<td style="text-align: right;">216</td>
<td style="text-align: right;">159.0</td>
<td style="text-align: right;">34.07922</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Tarfful</td>
<td style="text-align: right;">234</td>
<td style="text-align: right;">136.0</td>
<td style="text-align: right;">24.83746</td>
</tr>
<tr class="even">
<td style="text-align: left;">Raymus Antilles</td>
<td style="text-align: right;">188</td>
<td style="text-align: right;">79.0</td>
<td style="text-align: right;">22.35174</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Sly Moore</td>
<td style="text-align: right;">178</td>
<td style="text-align: right;">48.0</td>
<td style="text-align: right;">15.14960</td>
</tr>
<tr class="even">
<td style="text-align: left;">Tion Medon</td>
<td style="text-align: right;">206</td>
<td style="text-align: right;">80.0</td>
<td style="text-align: right;">18.85192</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Finn</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">Rey</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Poe Dameron</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">BB8</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Captain Phasma</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
<td style="text-align: right;">NA</td>
</tr>
</tbody>
</table>

1.  Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по
    отношению массы (mass) к росту (height) персонажей.

``` r
starwars %>%
  mutate(stretchiness = mass / height) %>%
  arrange(desc(stretchiness)) %>%            
  select(name, height, mass, stretchiness) %>% 
  head(10)    
```

    # A tibble: 10 × 4
       name                  height  mass stretchiness
       <chr>                  <int> <dbl>        <dbl>
     1 Jabba Desilijic Tiure    175  1358        7.76 
     2 Grievous                 216   159        0.736
     3 IG-88                    200   140        0.7  
     4 Owen Lars                178   120        0.674
     5 Darth Vader              202   136        0.673
     6 Jek Tono Porkins         180   110        0.611
     7 Bossk                    190   113        0.595
     8 Tarfful                  234   136        0.581
     9 Dexter Jettster          198   102        0.515
    10 Chewbacca                228   112        0.491

1.  Найти средний возраст персонажей каждой расы вселенной Звездных
    войн.

``` r
starwars %>%
  filter(!is.na(birth_year)) %>%              
  group_by(species) %>%                       
  summarise(average_age = mean(birth_year, na.rm = TRUE)) %>% 
  arrange(desc(average_age)) %>%
  kable
```

<table>
<thead>
<tr class="header">
<th style="text-align: left;">species</th>
<th style="text-align: right;">average_age</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Yoda’s species</td>
<td style="text-align: right;">896.00000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Hutt</td>
<td style="text-align: right;">600.00000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Wookiee</td>
<td style="text-align: right;">200.00000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Cerean</td>
<td style="text-align: right;">92.00000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Zabrak</td>
<td style="text-align: right;">54.00000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Human</td>
<td style="text-align: right;">53.74231</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Droid</td>
<td style="text-align: right;">53.33333</td>
</tr>
<tr class="even">
<td style="text-align: left;">Trandoshan</td>
<td style="text-align: right;">53.00000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gungan</td>
<td style="text-align: right;">52.00000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Mirialan</td>
<td style="text-align: right;">49.00000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Twi’lek</td>
<td style="text-align: right;">48.00000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Rodian</td>
<td style="text-align: right;">44.00000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Mon Calamari</td>
<td style="text-align: right;">41.00000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Kel Dor</td>
<td style="text-align: right;">22.00000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Ewok</td>
<td style="text-align: right;">8.00000</td>
</tr>
</tbody>
</table>

1.  Найти самый распространенный цвет глаз персонажей вселенной Звездных
    войн.

``` r
starwars %>%
  group_by(eye_color) %>%                     # Группируем по цвету глаз
  summarise(count = n()) %>%                  # Считаем количество персонажей
  arrange(desc(count)) %>%                    # Сортировка по убыванию
  slice(1)                                    # Самый популярный цвет
```

    # A tibble: 1 × 2
      eye_color count
      <chr>     <int>
    1 brown        21

1.  Подсчитать среднюю длину имени в каждой расе вселенной Звездных
    войн.

``` r
starwars %>%
  mutate(name_length = nchar(name)) %>%
  group_by(species) %>%                       
  summarise(average_name_length = mean(name_length, na.rm = TRUE)) %>% 
  arrange(desc(average_name_length)) %>%
  kable()
```

<table>
<thead>
<tr class="header">
<th style="text-align: left;">species</th>
<th style="text-align: right;">average_name_length</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Ewok</td>
<td style="text-align: right;">21.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Hutt</td>
<td style="text-align: right;">21.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Geonosian</td>
<td style="text-align: right;">17.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Besalisk</td>
<td style="text-align: right;">15.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Mirialan</td>
<td style="text-align: right;">14.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Toong</td>
<td style="text-align: right;">14.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Aleena</td>
<td style="text-align: right;">12.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Cerean</td>
<td style="text-align: right;">12.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gungan</td>
<td style="text-align: right;">11.666667</td>
</tr>
<tr class="even">
<td style="text-align: left;">Human</td>
<td style="text-align: right;">11.342857</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Iktotchi</td>
<td style="text-align: right;">11.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Neimodian</td>
<td style="text-align: right;">11.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Quermian</td>
<td style="text-align: right;">11.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Twi’lek</td>
<td style="text-align: right;">11.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">NA</td>
<td style="text-align: right;">10.500000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Chagrian</td>
<td style="text-align: right;">10.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Clawdite</td>
<td style="text-align: right;">10.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Pau’an</td>
<td style="text-align: right;">10.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Skakoan</td>
<td style="text-align: right;">10.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Tholothian</td>
<td style="text-align: right;">10.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Zabrak</td>
<td style="text-align: right;">9.500000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Nautolan</td>
<td style="text-align: right;">9.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Sullustan</td>
<td style="text-align: right;">9.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Kaleesh</td>
<td style="text-align: right;">8.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Kel Dor</td>
<td style="text-align: right;">8.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Muun</td>
<td style="text-align: right;">8.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Togruta</td>
<td style="text-align: right;">8.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Vulptereen</td>
<td style="text-align: right;">8.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Wookiee</td>
<td style="text-align: right;">8.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Dug</td>
<td style="text-align: right;">7.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Kaminoan</td>
<td style="text-align: right;">7.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Xexto</td>
<td style="text-align: right;">7.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Mon Calamari</td>
<td style="text-align: right;">6.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Rodian</td>
<td style="text-align: right;">6.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Toydarian</td>
<td style="text-align: right;">5.000000</td>
</tr>
<tr class="even">
<td style="text-align: left;">Trandoshan</td>
<td style="text-align: right;">5.000000</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Droid</td>
<td style="text-align: right;">4.833333</td>
</tr>
<tr class="even">
<td style="text-align: left;">Yoda’s species</td>
<td style="text-align: right;">4.000000</td>
</tr>
</tbody>
</table>

## Вывод

В ходе выполнения данной лабораторной раоты был проведён анализ набора
данных `starwars`, встроенного в пакет `dplyr` и даны ответы на заданные
вопросы
