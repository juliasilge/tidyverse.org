---
title: scales 1.1.0
author: Hadley Wickham
date: '2019-11-18'
slug: scales-1-1-0
description: 
  scales 1.1.0 now available on CRAN. It includes a new naming scheme 
  (with `breaks_` and `labels_` prefixes) and greatly improved documentation.
categories:
  - package
tags:
  - ggplot2
  - scales
  - r-lib
photo: 
  url: https://unsplash.com/photos/d0CasEMHDQs
  author: David Clode
---



We're thrilled to announce the release of [scales](https://scales.r-lib.org/) 1.1.0.
The scales package provides much of the infrastructure that underlies ggplot2's scales, and using it allow you to customize the transformations, breaks, and labels used by ggplot2. Get the latest version with:


```r
install.packages("scales")
```

The biggest improvements in this release are related to usability and documentation:

* Axis breaks and labels have a new naming scheme: functions that generate
  breaks from limits are called `breaks_`; functions that generate labels
  from breaks are called `labels_`.

* All the examples for breaks and labels have been overhauled to use new 
  `demo_continuous()`, `demo_discrete()`, and `demo_log10()`. These make
  it much easier to see how you'd use scales functions with ggplot2, so
  when you're [browsing the documentation](https://scales.r-lib.org/reference/index.html),
  you can immediately see how the functions work with ggplot2. 


```r
library(scales)
```

There are also a few new breaks and labels functions:

*   New [`breaks_width()`](https://scales.r-lib.org/reference/breaks_width.html)
    allows you to specify the distance between breaks rather than the number 
    of them.
  
    
    ```r
    demo_continuous(c(0, 100), breaks = breaks_width(10))
    #> scale_x_continuous(breaks = breaks_width(10))
    ```
    
    <img src="figs/unnamed-chunk-3-1.png" width="700px" style="display: block; margin: auto;" />
    
*   [`label_number()`](https://scales.r-lib.org/reference/label_number.html) and
    [`label_percent()`](https://scales.r-lib.org/reference/label_percent.html) 
    do a better job of picking the default `accuracy`, which means that you 
    should generally get the correct number of decimal place by default.
  
    
    ```r
    demo_continuous(c(0, 0.1), labels = label_number())
    #> scale_x_continuous(labels = label_number())
    ```
    
    <img src="figs/unnamed-chunk-4-1.png" width="700px" style="display: block; margin: auto;" />
    
    ```r
    demo_continuous(c(0, 0.1), labels = label_percent())
    #> scale_x_continuous(labels = label_percent())
    ```
    
    <img src="figs/unnamed-chunk-4-2.png" width="700px" style="display: block; margin: auto;" />

*   New [`label_bytes()`](https://scales.r-lib.org/reference/label_bytes.html) 
    replaces `number_bytes_format()` with a more convenient interface. It takes 
    a single `unit` argument which can either be an SI unit (e.g. "kB"), a 
    binary unit (e.g. "kIB"), or an automatic unit (either "auto_si" or
    "auto_binary").
  
    
    ```r
    # default is "auto_si"
    demo_continuous(c(1, 1e6), label = label_bytes())
    #> scale_x_continuous(label = label_bytes())
    ```
    
    <img src="figs/unnamed-chunk-5-1.png" width="700px" style="display: block; margin: auto;" />
    
    ```r
    # supply a unit if you want all labels to use the same unit
    demo_continuous(c(1, 1e6), label = label_bytes("kB"))
    #> scale_x_continuous(label = label_bytes("kB"))
    ```
    
    <img src="figs/unnamed-chunk-5-2.png" width="700px" style="display: block; margin: auto;" />
  
*   New [`label_number_auto()`](https://scales.r-lib.org/reference/label_number_auto.html)
    automatically picks between `label_number()` and `label_scientific()` based 
    on the range of the input. It should produce compact labels over a very wide
    range of inputs. We are considering making this the default labeller for
    a future version of ggplot2.
    
    
    ```r
    demo_continuous(c(1, 1e5), labels = label_number_auto())
    #> scale_x_continuous(labels = label_number_auto())
    ```
    
    <img src="figs/unnamed-chunk-6-1.png" width="700px" style="display: block; margin: auto;" />
    
    ```r
    demo_continuous(c(1, 1e10), labels = label_number_auto())
    #> scale_x_continuous(labels = label_number_auto())
    ```
    
    <img src="figs/unnamed-chunk-6-2.png" width="700px" style="display: block; margin: auto;" />
    
*   New [`label_number_si()`](https://scales.r-lib.org/reference/label_number_si.html)
    formats numeric vectors with SI units. 
  
    
    ```r
    demo_continuous(c(1, 1e9), label = label_number_si())
    #> scale_x_continuous(label = label_number_si())
    ```
    
    <img src="figs/unnamed-chunk-7-1.png" width="700px" style="display: block; margin: auto;" />
    
    ```r
    demo_log10(c(1, 1e9), breaks = log_breaks(10), labels = label_number_si())
    #> scale_x_log10(breaks = log_breaks(10), labels = label_number_si())
    ```
    
    <img src="figs/unnamed-chunk-7-2.png" width="700px" style="display: block; margin: auto;" />
  
*   New [`label_date_short()`](https://scales.r-lib.org/reference/label_date.html)
    creates labels for a date axis that only show the components of the date 
    that have changed since the previous label.

    
    ```r
    five_months <- as.POSIXct(c("2019-11-01", "2020-03-01"))
    demo_datetime(five_months)
    #> scale_x_datetime()
    ```
    
    <img src="figs/unnamed-chunk-8-1.png" width="700px" style="display: block; margin: auto;" />
    
    ```r
    demo_datetime(five_months, labels = label_date_short())
    #> scale_x_datetime(labels = label_date_short())
    ```
    
    <img src="figs/unnamed-chunk-8-2.png" width="700px" style="display: block; margin: auto;" />

See the [change log](https://scales.r-lib.org/news/index.html#scales-1-1-0) for a full list of changes and bug fixes in this version.
  
## Acknowledgements

A big thanks to all the GitHub contributors who helped make this release happen! [&#x0040;agila5](https://github.com/agila5), [&#x0040;Anirudhsekar96](https://github.com/Anirudhsekar96), [&#x0040;apsalverda](https://github.com/apsalverda), [&#x0040;b-lev](https://github.com/b-lev), [&#x0040;bhogan-mitre](https://github.com/bhogan-mitre), [&#x0040;billdenney](https://github.com/billdenney), [&#x0040;bjedwards](https://github.com/bjedwards), [&#x0040;bkkkk](https://github.com/bkkkk), [&#x0040;blairj09](https://github.com/blairj09), [&#x0040;clauswilke](https://github.com/clauswilke), [&#x0040;const-ae](https://github.com/const-ae), [&#x0040;davidmasp](https://github.com/davidmasp), [&#x0040;dpseidel](https://github.com/dpseidel), [&#x0040;eliocamp](https://github.com/eliocamp), [&#x0040;GegznaV](https://github.com/GegznaV), [&#x0040;hadley](https://github.com/hadley), [&#x0040;HenrikBengtsson](https://github.com/HenrikBengtsson), [&#x0040;hvaret](https://github.com/hvaret), [&#x0040;jcheng5](https://github.com/jcheng5), [&#x0040;kiernann](https://github.com/kiernann), [&#x0040;kuriwaki](https://github.com/kuriwaki), [&#x0040;mikmart](https://github.com/mikmart), [&#x0040;njtierney](https://github.com/njtierney), [&#x0040;paleolimbot](https://github.com/paleolimbot), [&#x0040;sada1993](https://github.com/sada1993), [&#x0040;schloerke](https://github.com/schloerke), [&#x0040;sflippl](https://github.com/sflippl), [&#x0040;slowkow](https://github.com/slowkow), [&#x0040;sobrietie](https://github.com/sobrietie), [&#x0040;tdawry](https://github.com/tdawry), [&#x0040;teramonagi](https://github.com/teramonagi), [&#x0040;thomasp85](https://github.com/thomasp85), [&#x0040;topepo](https://github.com/topepo), [&#x0040;tungmilan](https://github.com/tungmilan), [&#x0040;turgeonmaxime](https://github.com/turgeonmaxime), [&#x0040;wibeasley](https://github.com/wibeasley), [&#x0040;woodwards](https://github.com/woodwards), and [&#x0040;zamorarr](https://github.com/zamorarr).
