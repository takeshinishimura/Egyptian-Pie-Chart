Egyptian Pie Chart
================

``` r
library(dplyr)
library(ggplot2)
library(ggforce)

data <- data.frame(
  category = c("Sky", "Shady side of pyramid", "Sunny side of pyramid", "Sky"),
  fill = c("#6d9eeb", "#7f6000", "gold", "#6d9eeb"),
  proportion = c(0.38, 0.07, 0.17, 0.38)
) |>
  mutate(
    area = proportion * (2 * pi),
    start = c(0, head(cumsum(area), -1)),
    end = cumsum(area)
  )

ggplot(data) +
  geom_arc_bar(
    aes(x0 = 0, y0 = 0, r0 = 0, r = 1, start = start, end = end, fill = fill),
    color = NA
  ) +
  scale_fill_identity(
    guide = "legend",
    labels = data$category
  ) +
  coord_fixed() +
  theme_void() +
  theme(
    legend.title = element_blank()
  )
```

![](README_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->
