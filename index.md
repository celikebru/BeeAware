---
title: "den"
author: "Ebru Celik"
date: "20 06 2021"
output: html_document
---
```{r,echo = FALSE,message=FALSE,warning=FALSE}

library(tidyverse)
library(readr)
library(dplyr)
library(readxl)
library(purrr)
library(tidyr)
library(magrittr)
library(gganimate)

wbl2021<-read_xlsx("C:/Users/Ebru/Desktop/Mat381Proje/data/WBL2021.xlsx")
names(wbl2021)[2]<-"Country"
names(wbl2021)[3]<-"Country_Code"
names(wbl2021)[6]<-"Year"

#View(wbl2021)


```
```{r,echo = FALSE,message=FALSE,warning=FALSE}
#dim(wbl2021)
```
```{r,echo = FALSE,message=FALSE,warning=FALSE}
#str(wbl2021)
```
```{r,echo = FALSE,message=FALSE,warning=FALSE,include=FALSE}
wbl2021 %>%
  group_by(Region)%>%
  summarise(total_country=n())
```

## Number of Countries per Region

```{r}
library(ggplot2)
map1<-wbl2021%>%
mutate(Region = factor(Region, levels=c("East Asia & Pacific", "Europe & Central Asia", "High income: OECD", "Latin America & Caribbean","Middle East & North Africa","South Asia","Sub-Saharan Africa"))) %>%
  count(Region)%>%
  ggplot(aes(x="",y=n,fill =`Region`))+
   geom_bar(stat = "identity", color = "black") +
  labs(title = "Number of Countries per Region") +
  coord_polar("y") +
  geom_text(aes(label = paste0(n)), position = position_stack(vjust = 0.5))+
  theme_void() + 
  theme(plot.title = element_text(hjust = 0.5, color = "black"))
map1
```
