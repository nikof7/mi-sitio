---
title: Building your website with Hugo and RMarkdown
author: ''
date: '2023-03-07'
slug: building-your-website-with-hugo-and-rmarkdown
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2023-03-07T12:03:23-03:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index_files/pagedtable/css/pagedtable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/pagedtable/js/pagedtable.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>

Estuve practicando con algunos estadísticos y gráficos. Usé la carpeta datos que estan en drive; carpeta “Planillas Excel”, y cargué los archivos

- “2020_L Garzón.xlsx”
- “2020_LRocha_1ercampaña_1-5
- 10_NminyDUR.xlsx” y “2020_Solis Grande.xlsx”.

De cada tabla me quedé con el Punto, Fecha, Hora, Especie, Cantidad de individuos y Observaciones, no elimine ninguna fila. Luego unifiqué las tres en un mismo archivo csv.

# Importando tabla

``` r
data1 <- read_csv2("./datos/datos.csv", col_types = cols(
  Punto = col_character(),
  Fecha = col_date(),
  Hora = col_time(),
  Especie = col_character(),
  N = col_integer(),
  Observaciones = col_character()
))
```

``` r
tail(unique(data1$Especie))
```

    ## [1] "A. correndera?"   "paseriforme NN"   "A. pyrrholeuca"   "Anseriforme NN"  
    ## [5] "H. hydrochaeris?" "H. hydrochaeris"

Se observa que hay especies repetidas, algunas se les agrega “?” o simplemente estan mal escritas. Ej. L. gymnocerus, L. gymnocercus, L. gymnocercus?. En total hay 969 registros.

# Limpiando datos

Limpie los datos de “Especie” usando open refine. Deje solo los registros de mamiferos silvestres que lleguen hasta especie.

``` r
data <- read_csv2("./datos/datos-corredigos-silvestres.csv", col_types = cols( 
  Punto = col_character(),
  Fecha = col_date(),
  Hora = col_time(),
  Especie = col_character(),
  N = col_integer(),
  Observaciones = col_character()
))
```

<table class="table table-striped table-hover" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Punto
</th>
<th style="text-align:left;">
Fecha
</th>
<th style="text-align:left;">
Hora
</th>
<th style="text-align:left;">
Especie
</th>
<th style="text-align:right;">
N
</th>
<th style="text-align:left;">
Observaciones
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
SG01-2
</td>
<td style="text-align:left;">
2020-06-19
</td>
<td style="text-align:left;">
23:17:52
</td>
<td style="text-align:left;">
L. gymnocercus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
pasa por enfrente y luego por atrás en el otro sentido
</td>
</tr>
<tr>
<td style="text-align:left;">
SG01-2
</td>
<td style="text-align:left;">
2020-06-20
</td>
<td style="text-align:left;">
05:00:21
</td>
<td style="text-align:left;">
L. europaeus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
NA
</td>
</tr>
<tr>
<td style="text-align:left;">
SG01-2
</td>
<td style="text-align:left;">
2020-06-20
</td>
<td style="text-align:left;">
19:26:22
</td>
<td style="text-align:left;">
L. gymnocercus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
merodea buscando en el suelo
</td>
</tr>
<tr>
<td style="text-align:left;">
SG01-2
</td>
<td style="text-align:left;">
2020-06-22
</td>
<td style="text-align:left;">
02:30:42
</td>
<td style="text-align:left;">
L. gymnocercus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
NA
</td>
</tr>
<tr>
<td style="text-align:left;">
SG01-2
</td>
<td style="text-align:left;">
2020-06-22
</td>
<td style="text-align:left;">
04:41:01
</td>
<td style="text-align:left;">
L. gymnocercus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
NA
</td>
</tr>
<tr>
<td style="text-align:left;">
SG01-2
</td>
<td style="text-align:left;">
2020-06-22
</td>
<td style="text-align:left;">
21:09:21
</td>
<td style="text-align:left;">
L. gymnocercus
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
NA
</td>
</tr>
</tbody>
</table>

# Cantidad de registros por especie

Construyo una tabla con la cantidad de registros por especie y calculo el porcentaje de cada una.

``` r
records_per_species <- data %>%
  group_by(Especie) %>% 
  summarize(Total = sum(N)) %>%
  arrange(Total) %>% 
  mutate(perc = round(Total / sum(Total), 3))
```

<table class="table table-striped table-hover" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Especie
</th>
<th style="text-align:right;">
Total
</th>
<th style="text-align:right;">
perc
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
G. cuja
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0.004
</td>
</tr>
<tr>
<td style="text-align:left;">
L. wiedii
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0.004
</td>
</tr>
<tr>
<td style="text-align:left;">
H. hydrochaeris
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0.006
</td>
</tr>
<tr>
<td style="text-align:left;">
M. gouazoubira
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
0.010
</td>
</tr>
<tr>
<td style="text-align:left;">
P. cancrivorus
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
0.012
</td>
</tr>
<tr>
<td style="text-align:left;">
E. sexcinctus
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:right;">
0.023
</td>
</tr>
<tr>
<td style="text-align:left;">
L. geoffroyi
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
0.027
</td>
</tr>
<tr>
<td style="text-align:left;">
D. albiventris
</td>
<td style="text-align:right;">
16
</td>
<td style="text-align:right;">
0.031
</td>
</tr>
<tr>
<td style="text-align:left;">
L. europaeus
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:right;">
0.052
</td>
</tr>
<tr>
<td style="text-align:left;">
D. novemcinctus
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
0.058
</td>
</tr>
<tr>
<td style="text-align:left;">
D. hybridus
</td>
<td style="text-align:right;">
37
</td>
<td style="text-align:right;">
0.071
</td>
</tr>
<tr>
<td style="text-align:left;">
C. thous
</td>
<td style="text-align:right;">
43
</td>
<td style="text-align:right;">
0.083
</td>
</tr>
<tr>
<td style="text-align:left;">
C. chinga
</td>
<td style="text-align:right;">
49
</td>
<td style="text-align:right;">
0.095
</td>
</tr>
<tr>
<td style="text-align:left;">
A. axis
</td>
<td style="text-align:right;">
103
</td>
<td style="text-align:right;">
0.199
</td>
</tr>
<tr>
<td style="text-align:left;">
L. gymnocercus
</td>
<td style="text-align:right;">
169
</td>
<td style="text-align:right;">
0.326
</td>
</tr>
</tbody>
</table>

Gráfico:

``` r
r <- records_per_species %>% 
  ggplot(aes(y=reorder(Especie, perc), x=perc)) +
  geom_col(fill = "gray70") +
  geom_text(aes(label = paste(perc*100, "%", sep ="")), nudge_x = 0.015, size=3.2) +
  labs(
    title = "Porcentaje de registros por especie",
    subtitle = "Para todos los sitios, falta destacar especies prioritarias o estados de conservaci0n",
    x = "Porcentaje de registros",
    y = "",
  ) +
  scale_x_continuous(labels = scales::percent) +
  theme(axis.text.y=element_text(face="italic"),
        panel.background = element_rect(fill = "white", colour = "white", size = 0.5, linetype = "solid"),
        panel.grid.major = element_line(size = 0.1, linetype = 'solid', colour = "#f2f2f2"),
        panel.grid.minor = element_line(size = 0.1, linetype = 'solid', colour = "#f2f2f2")
  )

ggplotly(r)
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"data":[{"orientation":"v","width":[0.004,0.004,0.006,0.01,0.012,0.023,0.027,0.031,0.052,0.058,0.071,0.083,0.095,0.199,0.326],"base":[0.55,1.55,2.55,3.55,4.55,5.55,6.55,7.55,8.55,9.55,10.55,11.55,12.55,13.55,14.55],"x":[0.002,0.002,0.003,0.005,0.006,0.0115,0.0135,0.0155,0.026,0.029,0.0355,0.0415,0.0475,0.0995,0.163],"y":[0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999],"text":["perc: 0.004<br />reorder(Especie, perc): G. cuja","perc: 0.004<br />reorder(Especie, perc): L. wiedii","perc: 0.006<br />reorder(Especie, perc): H. hydrochaeris","perc: 0.010<br />reorder(Especie, perc): M. gouazoubira","perc: 0.012<br />reorder(Especie, perc): P. cancrivorus","perc: 0.023<br />reorder(Especie, perc): E. sexcinctus","perc: 0.027<br />reorder(Especie, perc): L. geoffroyi","perc: 0.031<br />reorder(Especie, perc): D. albiventris","perc: 0.052<br />reorder(Especie, perc): L. europaeus","perc: 0.058<br />reorder(Especie, perc): D. novemcinctus","perc: 0.071<br />reorder(Especie, perc): D. hybridus","perc: 0.083<br />reorder(Especie, perc): C. thous","perc: 0.095<br />reorder(Especie, perc): C. chinga","perc: 0.199<br />reorder(Especie, perc): A. axis","perc: 0.326<br />reorder(Especie, perc): L. gymnocercus"],"type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(179,179,179,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[0.019,0.019,0.021,0.025,0.027,0.038,0.042,0.046,0.067,0.073,0.086,0.098,0.11,0.214,0.341],"y":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15],"text":["0.4%","0.4%","0.6%","1%","1.2%","2.3%","2.7%","3.1%","5.2%","5.8%","7.1%","8.3%","9.5%","19.9%","32.6%"],"hovertext":["perc: 0.004<br />reorder(Especie, perc): G. cuja<br />paste(perc * 100, \"%\", sep = \"\"): 0.4%","perc: 0.004<br />reorder(Especie, perc): L. wiedii<br />paste(perc * 100, \"%\", sep = \"\"): 0.4%","perc: 0.006<br />reorder(Especie, perc): H. hydrochaeris<br />paste(perc * 100, \"%\", sep = \"\"): 0.6%","perc: 0.010<br />reorder(Especie, perc): M. gouazoubira<br />paste(perc * 100, \"%\", sep = \"\"): 1%","perc: 0.012<br />reorder(Especie, perc): P. cancrivorus<br />paste(perc * 100, \"%\", sep = \"\"): 1.2%","perc: 0.023<br />reorder(Especie, perc): E. sexcinctus<br />paste(perc * 100, \"%\", sep = \"\"): 2.3%","perc: 0.027<br />reorder(Especie, perc): L. geoffroyi<br />paste(perc * 100, \"%\", sep = \"\"): 2.7%","perc: 0.031<br />reorder(Especie, perc): D. albiventris<br />paste(perc * 100, \"%\", sep = \"\"): 3.1%","perc: 0.052<br />reorder(Especie, perc): L. europaeus<br />paste(perc * 100, \"%\", sep = \"\"): 5.2%","perc: 0.058<br />reorder(Especie, perc): D. novemcinctus<br />paste(perc * 100, \"%\", sep = \"\"): 5.8%","perc: 0.071<br />reorder(Especie, perc): D. hybridus<br />paste(perc * 100, \"%\", sep = \"\"): 7.1%","perc: 0.083<br />reorder(Especie, perc): C. thous<br />paste(perc * 100, \"%\", sep = \"\"): 8.3%","perc: 0.095<br />reorder(Especie, perc): C. chinga<br />paste(perc * 100, \"%\", sep = \"\"): 9.5%","perc: 0.199<br />reorder(Especie, perc): A. axis<br />paste(perc * 100, \"%\", sep = \"\"): 19.9%","perc: 0.326<br />reorder(Especie, perc): L. gymnocercus<br />paste(perc * 100, \"%\", sep = \"\"): 32.6%"],"textfont":{"size":12.0944881889764,"color":"rgba(0,0,0,1)"},"type":"scatter","mode":"text","hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":98.6301369863014},"plot_bgcolor":"rgba(255,255,255,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Porcentaje de registros por especie","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.01705,0.35805],"tickmode":"array","ticktext":["0%","10%","20%","30%"],"tickvals":[0,0.1,0.2,0.3],"categoryorder":"array","categoryarray":["0%","10%","20%","30%"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(242,242,242,1)","gridwidth":0.132835201328352,"zeroline":false,"anchor":"y","title":{"text":"Porcentaje de registros","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,15.6],"tickmode":"array","ticktext":["G. cuja","L. wiedii","H. hydrochaeris","M. gouazoubira","P. cancrivorus","E. sexcinctus","L. geoffroyi","D. albiventris","L. europaeus","D. novemcinctus","D. hybridus","C. thous","C. chinga","A. axis","L. gymnocercus"],"tickvals":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15],"categoryorder":"array","categoryarray":["G. cuja","L. wiedii","H. hydrochaeris","M. gouazoubira","P. cancrivorus","E. sexcinctus","L. geoffroyi","D. albiventris","L. europaeus","D. novemcinctus","D. hybridus","C. thous","C. chinga","A. axis","L. gymnocercus"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(242,242,242,1)","gridwidth":0.132835201328352,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"1e28daf584b":{"x":{},"y":{},"type":"bar"},"1e283fef41d":{"x":{},"y":{},"label":{}}},"cur_data":"1e28daf584b","visdat":{"1e28daf584b":["function (y) ","x"],"1e283fef41d":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

# Probando el paquete “vegan”.

Para utilizar este paquete necesitamos que la información esté organizada de esta forma:

| **Site** | **Sp1** | **Sp2** | **Sp3** | **SpN** |
|:--------:|:-------:|:-------:|:-------:|:-------:|
|  **1**   |    4    |    2    |    0    |    0    |
|  **2**   |    0    |    0    |    2    |    5    |
|  **N**   |    0    |    0    |    0    |   10    |

Es decir, la primera columna son los sitios en formato numérico y, por lo tanto, cada fila corresponde a un sitio, el resto de columnas son las especies y el contenido en las celdas es la cantidad de registros para cada sp.

## Armado de la tabla

Elimino la fecha, hora y observaciones porque no tienen sentido para este análisis.

``` r
data_vegan_long <- data %>%
  mutate(Punto=str_extract(Punto, "^.{2}")) %>%
  select(Punto, Especie, N) %>% 
  group_by(Punto, Especie) %>% 
  summarize(Total = sum(N), .groups = 'drop')
```

La tabla ahora luce de esta forma:

<table class="table table-striped table-hover" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Punto
</th>
<th style="text-align:left;">
Especie
</th>
<th style="text-align:right;">
Total
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:left;">
A. axis
</td>
<td style="text-align:right;">
97
</td>
</tr>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:left;">
C. chinga
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:left;">
D. hybridus
</td>
<td style="text-align:right;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:left;">
D. novemcinctus
</td>
<td style="text-align:right;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:left;">
E. sexcinctus
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:left;">
G. cuja
</td>
<td style="text-align:right;">
2
</td>
</tr>
</tbody>
</table>

Para cada punto hay un n de las especies. Con esto, ahora puedo transformar esta tabla larga (long) a una ancha (wide) que el paquete vegan utiliza.

``` r
data_vegan_wide <- data_vegan_long %>% 
  spread(Especie, Total) %>% 
  mutate_if(is.numeric, ~replace(., is.na(.), 0)) %>%   # rellena con ceros los NA's
  column_to_rownames("Punto")

### Guardo qué número es cada punto
puntos <- row.names(data_vegan_wide)

#data_vegan_wide <- select(data_vegan_wide, -Punto)
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:100%; ">

<table class="table table-striped table-hover" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
A. axis
</th>
<th style="text-align:right;">
C. chinga
</th>
<th style="text-align:right;">
C. thous
</th>
<th style="text-align:right;">
D. albiventris
</th>
<th style="text-align:right;">
D. hybridus
</th>
<th style="text-align:right;">
D. novemcinctus
</th>
<th style="text-align:right;">
E. sexcinctus
</th>
<th style="text-align:right;">
G. cuja
</th>
<th style="text-align:right;">
H. hydrochaeris
</th>
<th style="text-align:right;">
L. europaeus
</th>
<th style="text-align:right;">
L. geoffroyi
</th>
<th style="text-align:right;">
L. gymnocercus
</th>
<th style="text-align:right;">
L. wiedii
</th>
<th style="text-align:right;">
M. gouazoubira
</th>
<th style="text-align:right;">
P. cancrivorus
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:right;">
97
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
LR
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
36
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
16
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
17
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
108
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
SG
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
39
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
27
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
21
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
</tr>
</tbody>
</table>

</div>

## Cálculo de estadísticos

Riqueza, diversidad, índice de dominancia, etc. Elimino los SD porque dan todos cero ¿qué será? Además, desde chao en adelante dan todos números enteros. Cuando hago un pool y calculo lo mismo da números con coma ¿es importante?

``` r
datos <- data_vegan_wide

outcome <- tibble(
    richness_ = specnumber(datos),
    shannon_ = diversity(datos, index = "shannon"),
    simpson_ = diversity(datos, index = "simpson"),
    invsimpson_ = diversity(datos, index = "invsimpson"),
    specpool(datos, pool = puntos)
  ) %>% 
  select(-Species, -ends_with(".se")) %>%
  mutate(Punto = puntos, .before=1)
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:100%; ">

<table class="table table-striped table-hover" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Punto
</th>
<th style="text-align:right;">
richness\_
</th>
<th style="text-align:right;">
shannon\_
</th>
<th style="text-align:right;">
simpson\_
</th>
<th style="text-align:right;">
invsimpson\_
</th>
<th style="text-align:right;">
chao
</th>
<th style="text-align:right;">
jack1
</th>
<th style="text-align:right;">
jack2
</th>
<th style="text-align:right;">
boot
</th>
<th style="text-align:right;">
n
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
LG
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
1.226760
</td>
<td style="text-align:right;">
0.5718144
</td>
<td style="text-align:right;">
2.335436
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
LR
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
1.685130
</td>
<td style="text-align:right;">
0.7311610
</td>
<td style="text-align:right;">
3.719698
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
SG
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
1.888639
</td>
<td style="text-align:right;">
0.8072320
</td>
<td style="text-align:right;">
5.187584
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
1
</td>
</tr>
</tbody>
</table>

</div>

``` r
paged_table(outcome)
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Punto"],"name":[1],"type":["chr"],"align":["left"]},{"label":["richness_"],"name":[2],"type":["int"],"align":["right"]},{"label":["shannon_"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["simpson_"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["invsimpson_"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["chao"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["jack1"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["jack2"],"name":[8],"type":["int"],"align":["right"]},{"label":["boot"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["n"],"name":[10],"type":["int"],"align":["right"]}],"data":[{"1":"LG","2":"10","3":"1.226760","4":"0.5718144","5":"2.335436","6":"10","7":"10","8":"10","9":"10","10":"1","_row":"LG"},{"1":"LR","2":"10","3":"1.685130","4":"0.7311610","5":"3.719699","6":"10","7":"10","8":"10","9":"10","10":"1","_row":"LR"},{"1":"SG","2":"11","3":"1.888639","4":"0.8072320","5":"5.187584","6":"11","7":"11","8":"11","9":"11","10":"1","_row":"SG"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

Esto es lo que decía antes sobre los números con coma:

``` r
specpool(datos)
```

    ##     Species chao  chao.se jack1 jack1.se    jack2     boot boot.se n
    ## All      15   21 6.928203    19 2.828427 20.66667 16.85185 1.45815 3

Abundancia de las especies en los diferentes sitios:

``` r
mdsEuclidean <- metaMDS(datos, distance="euc", autotransform=FALSE, trace=0)
plot(mdsEuclidean, display="sites", type="text", main = "Euclidean")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-16-1.png" width="672" />

``` r
mdsCurtis <- metaMDS(datos, distance="bray", autotransform=FALSE, trace=0)
plot(mdsCurtis, display="sites", type="text", main="BrayCurtis")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-16-2.png" width="672" />

Son gráficos multidimensionales no métricos (NMDS) muestran las distancias aproximadas entre sitios. Las distancias euclidianas tienden a enfatizar las diferencias debido a las especies más abundantes, mientras que BrayCurtis no.

``` r
#Estandariza
datos.perfil <- decostand(datos, method = "total")
# Verificación, tiene que dar 1 en todos.
apply(datos.perfil, 1, sum)
```

    ## LG LR SG 
    ##  1  1  1

``` r
# Matriz de distancias entre perfiles
d18 <- dist(datos.perfil, method = "euclidean")
# Cluster utilizando esta distancia entre sitios.
cl18 <- hclust(d18)

p <- ggdendrogram(cl18, rotate = FALSE, size = 2) +
  labs(title = "Dendrograma con distancias euclidianas",
       x = "Sitios",
       y = "Similitud")

ggplotly(p)
```

<div id="htmlwidget-2" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"data":[{"visible":false,"showlegend":false,"xaxis":null,"yaxis":null,"hoverinfo":"text","frame":null},{"x":[1.75,1,null,1,1,null,1.75,2.5,null,2.5,2.5,null,2.5,2,null,2,2,null,2.5,3,null,3,3],"y":[0.713689504932815,0.713689504932815,null,0.713689504932815,0,null,0.713689504932815,0.713689504932815,null,0.713689504932815,0.50061390217169,null,0.50061390217169,0.50061390217169,null,0.50061390217169,0,null,0.50061390217169,0.50061390217169,null,0.50061390217169,0],"text":["xend: 1.0<br />yend: 0.7136895<br />x: 1.75<br />y: 0.7136895","xend: 1.0<br />yend: 0.7136895<br />x: 1.75<br />y: 0.7136895",null,"xend: 1.0<br />yend: 0.0000000<br />x: 1.00<br />y: 0.7136895","xend: 1.0<br />yend: 0.0000000<br />x: 1.00<br />y: 0.7136895",null,"xend: 2.5<br />yend: 0.7136895<br />x: 1.75<br />y: 0.7136895","xend: 2.5<br />yend: 0.7136895<br />x: 1.75<br />y: 0.7136895",null,"xend: 2.5<br />yend: 0.5006139<br />x: 2.50<br />y: 0.7136895","xend: 2.5<br />yend: 0.5006139<br />x: 2.50<br />y: 0.7136895",null,"xend: 2.0<br />yend: 0.5006139<br />x: 2.50<br />y: 0.5006139","xend: 2.0<br />yend: 0.5006139<br />x: 2.50<br />y: 0.5006139",null,"xend: 2.0<br />yend: 0.0000000<br />x: 2.00<br />y: 0.5006139","xend: 2.0<br />yend: 0.0000000<br />x: 2.00<br />y: 0.5006139",null,"xend: 3.0<br />yend: 0.5006139<br />x: 2.50<br />y: 0.5006139","xend: 3.0<br />yend: 0.5006139<br />x: 2.50<br />y: 0.5006139",null,"xend: 3.0<br />yend: 0.0000000<br />x: 3.00<br />y: 0.5006139","xend: 3.0<br />yend: 0.0000000<br />x: 3.00<br />y: 0.5006139"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,0,0,1)","dash":"solid"},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":22.648401826484},"paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Dendrograma con distancias euclidianas","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.9,3.1],"tickmode":"array","ticktext":["LG","LR","SG"],"tickvals":[1,2,3],"categoryorder":"array","categoryarray":["LG","LR","SG"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-90,"showline":false,"linecolor":null,"linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"Sitios","font":{"color":"transparent","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.0356844752466407,0.749373980179455],"tickmode":"array","ticktext":["0.0","0.2","0.4","0.6"],"tickvals":[0,0.2,0.4,0.6],"categoryorder":"array","categoryarray":["0.0","0.2","0.4","0.6"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-90,"showline":false,"linecolor":null,"linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":null,"family":null,"size":0}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"1e285b24415":{"type":"scatter"},"1e28285d7ee5":{"xend":{},"yend":{},"x":{},"y":{}}},"cur_data":"1e285b24415","visdat":{"1e285b24415":["function (y) ","x"],"1e28285d7ee5":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

# Anotaciones

Dejo algunas inquietudes:

- ¿Qué pasa con los mamíferos domésticos? ¿Cómo se incluirían en el análisis?
- ¿Cómo calcular esfuerzo de muestreo? ¿Qué tener en cuenta? Esto supongo que debe ser necesario porque en todos los sitios el esfuerzo debe ser diferente y debe influenciar a riqueza y abundancia de las especies en los sitios.
- Cada área protegida tiene varios sistemas ¿estos se tienen que agrupar todos en uno? Así lo hice en el documento
