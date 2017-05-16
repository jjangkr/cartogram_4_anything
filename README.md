# cartogram_4_anything

How to add any attribute what you want to generate cartogram of Korea

Korean cartogram for anything what you want!!

```{r first}
library(Kormaps); library(tmap); library(cartogram); library(dplyr); library(readxl)

setwd("file path")  # add any path what you need

data("korpopmap1")  # data set in Kormaps package

total <- read_excel('regionaldata_SP.xlsx', 
                  sheet = 'total', col_names = T )  
# I uploaded "regionaldata_SP.xlsx" file in this repository.

str(total)  # check the type of total data
```
In total data you can use energy consumption and GRDP of each province in Korea from 1998 to 2015 and R&D investments of each province in Korea from 2010 to 2015.


```{r second }
korpopmap1@data <- left_join(korpopmap1@data, total, 
                             by = c('code.1' = 'code'))  ## add data set to SPDF 'korpopmap1'

summary(korpopmap1@data)  # you can clarify what kind of data are added and understand statistics of data set

kor_en1998 <- cartogram(korpopmap1, "en1998", itermax=2)  
# cartogram of energy consumption of Koean province in 1998   
# if you want to get dramatical graph, you can change itermax to 5, 8 or what you want

tm_shape(kor_en1998) + tm_fill("en1998", style="cat") + 
  tm_borders() + tm_layout(frame=F)     
# generate cartogram of Koean energy consumption in 1998
```
