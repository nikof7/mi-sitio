---
title: 'NaturalistaUY: Fauna atropellada del Uruguay'
author: ''
date: '2023-03-15'
slug: naturalistauy-atropellos
categories: []
tags: [NaturalistaUY]
summary: 'Este proyecto busca analizar y describir los datos sobre atropellos de vertebrados en el Uruguay. Utiliza los datos que se reúnen en otro proyecto de NaturalistaUY llamado "Fauna Atropellada del Uruguay'
authors: []
external_link: ''
image:
  caption: ''
  focal_point: ''
  preview_only: yes
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''
slides: ''
---
<script src="{{< blogdown/postref >}}index.es_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index.es_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.es_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index.es_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.es_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index.es_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.es_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index.es_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.es_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index.es_files/lightable/lightable.css" rel="stylesheet" />





[Puedes visitar el proyecto de Naturalista UY desde aquí](https://www.naturalista.uy/projects/fauna-atropellada-del-uruguay)


Falta describir un poco más sobre de qué es el proyecto. En qué etapa está, a dónde apunta, etc.
Revisar código y datos generados.
Actualizar base de datos.

## Utilizando el csv del proyecto

Se descarga el archivo csv desde iNaturalist y se carga.


```r
data <- read.csv2("data.csv", sep = ",") %>% 
  select(id, user_id, iconic_taxon_name, scientific_name, common_name, quality_grade, latitude, longitude, time_observed_at, created_at, tag_list, description, license, url) %>% 
  as_tibble() %>%
  mutate(time_observed_at = ymd_hms(time_observed_at), created_at = ymd_hms(created_at))
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:100%; "><table class=" lightable-material-dark" style='font-family: "Source Sans Pro", helvetica, sans-serif; margin-left: auto; margin-right: auto;'>
 <thead>
  <tr>
   <th style="text-align:right;"> ID </th>
   <th style="text-align:right;"> ID de usuario </th>
   <th style="text-align:left;"> Clase </th>
   <th style="text-align:left;"> Nombre científico </th>
   <th style="text-align:left;"> Nombre común </th>
   <th style="text-align:left;"> Grado de calidad </th>
   <th style="text-align:left;"> Latitud </th>
   <th style="text-align:left;"> Longitud </th>
   <th style="text-align:left;"> Observado </th>
   <th style="text-align:left;"> Creado </th>
   <th style="text-align:left;"> Lista de tags </th>
   <th style="text-align:left;"> Descripción </th>
   <th style="text-align:left;"> Licencia </th>
   <th style="text-align:left;"> URL </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 87222 </td>
   <td style="text-align:right;"> 1178 </td>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> Procyon cancrivorus </td>
   <td style="text-align:left;"> Mano pelada </td>
   <td style="text-align:left;"> research </td>
   <td style="text-align:left;"> -34.1866718618 </td>
   <td style="text-align:left;"> -53.7563180923 </td>
   <td style="text-align:left;"> NA </td>
   <td style="text-align:left;"> 2012-06-04 14:15:57 </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> CC-BY </td>
   <td style="text-align:left;"> http://www.inaturalist.org/observations/87222 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1266639 </td>
   <td style="text-align:right;"> 1178 </td>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> Cerdocyon thous </td>
   <td style="text-align:left;"> Zorro De Monte </td>
   <td style="text-align:left;"> research </td>
   <td style="text-align:left;"> -34.182589 </td>
   <td style="text-align:left;"> -53.752885 </td>
   <td style="text-align:left;"> 2011-01-10 12:52:33 </td>
   <td style="text-align:left;"> 2015-03-02 17:25:37 </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> CC-BY </td>
   <td style="text-align:left;"> http://www.inaturalist.org/observations/1266639 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6970136 </td>
   <td style="text-align:right;"> 477998 </td>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> Didelphis albiventris </td>
   <td style="text-align:left;"> Comadreja overa </td>
   <td style="text-align:left;"> research </td>
   <td style="text-align:left;"> -32.37997905 </td>
   <td style="text-align:left;"> -53.92697861 </td>
   <td style="text-align:left;"> 2017-07-08 09:49:38 </td>
   <td style="text-align:left;"> 2017-07-08 19:43:56 </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> CC-BY-NC </td>
   <td style="text-align:left;"> https://www.inaturalist.org/observations/6970136 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6970137 </td>
   <td style="text-align:right;"> 477998 </td>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> Cerdocyon thous </td>
   <td style="text-align:left;"> Zorro De Monte </td>
   <td style="text-align:left;"> research </td>
   <td style="text-align:left;"> -32.37826382 </td>
   <td style="text-align:left;"> -54.00389455 </td>
   <td style="text-align:left;"> 2017-07-08 11:22:24 </td>
   <td style="text-align:left;"> 2017-07-08 19:44:01 </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> CC-BY-NC </td>
   <td style="text-align:left;"> https://www.inaturalist.org/observations/6970137 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6970138 </td>
   <td style="text-align:right;"> 477998 </td>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> Lycalopex gymnocercus </td>
   <td style="text-align:left;"> Zorro Gris </td>
   <td style="text-align:left;"> research </td>
   <td style="text-align:left;"> -32.38082107 </td>
   <td style="text-align:left;"> -54.01652109 </td>
   <td style="text-align:left;"> 2017-07-08 11:29:39 </td>
   <td style="text-align:left;"> 2017-07-08 19:44:03 </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> CC-BY-NC </td>
   <td style="text-align:left;"> https://www.inaturalist.org/observations/6970138 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 7036602 </td>
   <td style="text-align:right;"> 477998 </td>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> Conepatus chinga </td>
   <td style="text-align:left;"> Zorrino </td>
   <td style="text-align:left;"> research </td>
   <td style="text-align:left;"> -32.56051339 </td>
   <td style="text-align:left;"> -54.57835282 </td>
   <td style="text-align:left;"> 2017-07-11 10:29:07 </td>
   <td style="text-align:left;"> 2017-07-13 15:04:37 </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> CC-BY-NC </td>
   <td style="text-align:left;"> https://www.inaturalist.org/observations/7036602 </td>
  </tr>
</tbody>
</table></div>

## Exploración de los datos

Se comienza por describir la cantidad de observaciones por clase taxonómica.


```r
obs_per_class <- data %>% 
  group_by(iconic_taxon_name) %>% 
  summarise(Sum = n()) %>% 
  arrange(Sum)
```

<table class=" lightable-material-dark" style='font-family: "Source Sans Pro", helvetica, sans-serif; margin-left: auto; margin-right: auto;'>
 <thead>
  <tr>
   <th style="text-align:center;"> Clase </th>
   <th style="text-align:center;"> Cantidad </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> Amphibia </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Aves </td>
   <td style="text-align:center;"> 14 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Reptilia </td>
   <td style="text-align:center;"> 86 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Mammalia </td>
   <td style="text-align:center;"> 116 </td>
  </tr>
</tbody>
</table>

Se observa un claro sesgo hacia los registros de mamíferos.


Pasemos a analizar esta característica pero en relación a los años, para esto se debe trabajar un poco la información.



```r
data_times <- data %>%
  drop_na(time_observed_at) %>% 
  arrange(time_observed_at) %>%
  mutate(years = year(time_observed_at)) %>% 
  select(iconic_taxon_name, years) 
```


<table class=" lightable-material-dark" style='font-family: "Source Sans Pro", helvetica, sans-serif; margin-left: auto; margin-right: auto;'>
 <thead>
  <tr>
   <th style="text-align:left;"> Clase taxonómica </th>
   <th style="text-align:left;"> Año </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2011 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2012 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2012 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2014 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2015 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2015 </td>
  </tr>
</tbody>
</table>

Total de registros por año

```r
data_total_year <- data_times %>%
  mutate(years = as.integer(years)) %>% 
  group_by(years) %>%
  summarise(Sum = n()) %>% 
  arrange(-years) %>%
  filter(years != '2023')
```

<table class=" lightable-material-dark" style='font-family: "Source Sans Pro", helvetica, sans-serif; margin-left: auto; margin-right: auto;'>
 <thead>
  <tr>
   <th style="text-align:left;"> Años </th>
   <th style="text-align:left;"> Total </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 2022 </td>
   <td style="text-align:left;"> 124 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2021 </td>
   <td style="text-align:left;"> 20 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2020 </td>
   <td style="text-align:left;"> 29 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2019 </td>
   <td style="text-align:left;"> 5 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2018 </td>
   <td style="text-align:left;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2017 </td>
   <td style="text-align:left;"> 14 </td>
  </tr>
</tbody>
</table>

Registros por año por taxón


```r
data_year_taxon <- data_times %>%
  group_by(iconic_taxon_name, years)
```

<table class=" lightable-material-dark" style='font-family: "Source Sans Pro", helvetica, sans-serif; margin-left: auto; margin-right: auto;'>
 <thead>
  <tr>
   <th style="text-align:left;"> Clase taxonómica </th>
   <th style="text-align:left;"> Año </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2022 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Reptilia </td>
   <td style="text-align:left;"> 2022 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2022 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mammalia </td>
   <td style="text-align:left;"> 2022 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Aves </td>
   <td style="text-align:left;"> 2023 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Aves </td>
   <td style="text-align:left;"> 2023 </td>
  </tr>
</tbody>
</table>




```r
data_times %>% 
  ggplot(aes(x=years, fill=factor(iconic_taxon_name))) +
  geom_bar(position=position_dodge()) +
  scale_x_continuous(labels=as.character(data_times$years),breaks=data_times$years)
```

<img src="{{< blogdown/postref >}}index.es_files/figure-html/unnamed-chunk-12-1.png" width="672" />







