---
title: "Deber de Inferencia Estadística"
author: "González Reyes Rocío"
date: "2023-08-29"
output:
  word_document: default
  html_document:
    df_print: paged
  pdf_document:
    latex_engine: pdflatex
---

---



## Introducción

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:



```r
library (tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.2     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.0
## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
## ✔ purrr     1.0.1     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

## Ejercicio 1: Comparación de ingresos medios
Estás comparando los ingresos medios de dos grupos diferentes de trabajadores. ¿Qué grupo tiene un
ingreso promedio más alto?


```r
trabajadores1 <- c(2250.874, 2178.265, 1955.121, 2430.015, 2659.831, 2713.799, 2375.522, 2993.470,
                   2303.118, 2331.465, 2066.033, 2235.951, 3005.093, 2596.543, 2156.393, 2067.230,
                   2206.910, 2769.340, 3197.505, 2485.516, 2289.275, 2492.882, 2938.398, 2578.256,
                   2488.872, 2060.718, 2643.604, 2725.154,3179.045, 2917.966, 1915.504, 2957.806,
                   2410.418, 2320.605, 2649.970, 2626.137, 2466.415, 2697.411, 2395.003, 2367.791,
                   2181.179, 2813.058, 2823.114, 2516.957, 1718.990, 2533.165, 2060.041, 2539.865,
                   2883.900, 2699.181)
trabajadores2 <- c(2075.544, 2260.147, 2210.747, 2125.751, 2280.511, 2353.806, 2375.084,
                   2572.256, 1681.255, 2378.751, 2001.336, 2497.114, 2186.822, 2310.368,
                   2775.799, 2218.408, 2191.969, 2401.429, 2144.689, 2036.791, 2390.669,
                   2476.481, 2316.912, 1819.158, 2588.756, 2303.756, 2142.683, 2450.559,
                   2172.056, 2010.873, 2294.688, 2205.054, 2479.581, 2883.266, 2066.749,
                   2469.883, 2314.934, 2415.943, 2139.904, 2336.129, 1956.293, 2384.111,
                   2281.950, 2696.983, 2350.144, 2055.625, 2531.372, 2058.953, 2074.512,
                   2422.559, 2381.457, 2512.807, 2604.340, 2222.830, 2289.438, 2410.723,
                   2784.361, 2518.547, 2436.065, 1606.304)
```



```r
datos <- data.frame(
  salario = c(trabajadores1, trabajadores2),
  grupo = factor(rep(1:2, times = c(length(trabajadores1),length(trabajadores2))),
                 labels=c("Trabajadores 1", "Trabajadores 2"))
)
```


```r
ggplot(datos, aes(x=salario, fill=grupo)) +
  geom_histogram(position="identity", alpha=0.5, bins=30) +
  theme_minimal() +
  labs(title = "Distribución de Salarios", y = "Frecuencia", x = "Salario") +
  scale_fill_manual(values=c("#F8766D", "#00BA38"))
```

![](Informe-Final_files/figure-docx/3-1.png)<!-- -->

```r
ggplot(datos, aes(x=grupo, y=salario, fill=grupo)) +
  geom_boxplot() +
  theme_minimal() +
  labs(title = "Distribución de Salarios", y = "Salario", x = "Grupo") +
  scale_fill_manual(values=c("#F8766D", "#00BA38"))
```

![](Informe-Final_files/figure-docx/4-1.png)<!-- -->


```r
# Cálculo de los ingresos promedios para cada grupo
promedio_trabajadores1 <- mean(trabajadores1)
promedio_trabajadores2 <- mean(trabajadores2)

# Comparación de los ingresos promedios
if (promedio_trabajadores1 > promedio_trabajadores2) {
  resultado <- "Trabajadores 1"
} else if (promedio_trabajadores2 > promedio_trabajadores1) {
  resultado <- "Trabajadores 2"
} else {
  resultado <- "Ambos grupos tienen el mismo ingreso promedio"
}

# Imprimir el resultado
cat("El grupo con un ingreso promedio más alto es:", resultado)
```

```
El grupo con un ingreso promedio más alto es: Trabajadores 1
```


## Including Plots

You can also embed plots, for example:

![](Informe-Final_files/figure-docx/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
