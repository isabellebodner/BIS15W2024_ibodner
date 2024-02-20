---
title: "Lab 4 Homework"
author: "Isabelle Bodner"
date: "2024-01-28"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
homerange
```

```
## # A tibble: 569 × 24
##    taxon        common.name class order family genus species primarymethod N    
##    <chr>        <chr>       <chr> <chr> <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake fishes  american e… acti… angu… angui… angu… rostra… telemetry     16   
##  2 river fishes blacktail … acti… cypr… catos… moxo… poecil… mark-recaptu… <NA> 
##  3 river fishes central st… acti… cypr… cypri… camp… anomal… mark-recaptu… 20   
##  4 river fishes rosyside d… acti… cypr… cypri… clin… fundul… mark-recaptu… 26   
##  5 river fishes longnose d… acti… cypr… cypri… rhin… catara… mark-recaptu… 17   
##  6 river fishes muskellunge acti… esoc… esoci… esox  masqui… telemetry     5    
##  7 marine fish… pollack     acti… gadi… gadid… poll… pollac… telemetry     2    
##  8 marine fish… saithe      acti… gadi… gadid… poll… virens  telemetry     2    
##  9 marine fish… lined surg… acti… perc… acant… acan… lineat… direct obser… <NA> 
## 10 marine fish… orangespin… acti… perc… acant… naso  litura… telemetry     8    
## # ℹ 559 more rows
## # ℹ 15 more variables: mean.mass.g <dbl>, log10.mass <dbl>,
## #   alternative.mass.reference <chr>, mean.hra.m2 <dbl>, log10.hra <dbl>,
## #   hra.reference <chr>, realm <chr>, thermoregulation <chr>, locomotion <chr>,
## #   trophic.guild <chr>, dimension <dbl>, preymass <dbl>, log10.preymass <dbl>,
## #   PPMR <dbl>, prey.size.reference <chr>
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
dim(homerange)
```

```
## [1] 569  24
```

```r
colnames(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", …
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3…
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car…
## $ dimension                  <dbl> 3, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3…
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N…
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, …
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20…
```


```r
mean(homerange$preymass, na.rm = T)
```

```
## [1] 3989.876
```


**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
homerange$taxon <- as.factor(homerange$taxon)
homerange$order <- as.factor(homerange$order)
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```


```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"    "afrosoricida"       "anguilliformes"    
##  [4] "anseriformes"       "apterygiformes"     "artiodactyla"      
##  [7] "caprimulgiformes"   "carnivora"          "charadriiformes"   
## [10] "columbidormes"      "columbiformes"      "coraciiformes"     
## [13] "cuculiformes"       "cypriniformes"      "dasyuromorpha"     
## [16] "dasyuromorpia"      "didelphimorphia"    "diprodontia"       
## [19] "diprotodontia"      "erinaceomorpha"     "esociformes"       
## [22] "falconiformes"      "gadiformes"         "galliformes"       
## [25] "gruiformes"         "lagomorpha"         "macroscelidea"     
## [28] "monotrematae"       "passeriformes"      "pelecaniformes"    
## [31] "peramelemorphia"    "perciformes"        "perissodactyla"    
## [34] "piciformes"         "pilosa"             "proboscidea"       
## [37] "psittaciformes"     "rheiformes"         "roden"             
## [40] "rodentia"           "salmoniformes"      "scorpaeniformes"   
## [43] "siluriformes"       "soricomorpha"       "squamata"          
## [46] "strigiformes"       "struthioniformes"   "syngnathiformes"   
## [49] "testudines"         "tetraodontiformes\xa0" "tinamiformes"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```



```r
taxa <- select(homerange, "taxon","common.name","class","order","family","genus","species")
taxa
```

```
## # A tibble: 569 × 7
##    taxon         common.name             class        order family genus species
##    <fct>         <chr>                   <chr>        <fct> <chr>  <chr> <chr>  
##  1 lake fishes   american eel            actinoptery… angu… angui… angu… rostra…
##  2 river fishes  blacktail redhorse      actinoptery… cypr… catos… moxo… poecil…
##  3 river fishes  central stoneroller     actinoptery… cypr… cypri… camp… anomal…
##  4 river fishes  rosyside dace           actinoptery… cypr… cypri… clin… fundul…
##  5 river fishes  longnose dace           actinoptery… cypr… cypri… rhin… catara…
##  6 river fishes  muskellunge             actinoptery… esoc… esoci… esox  masqui…
##  7 marine fishes pollack                 actinoptery… gadi… gadid… poll… pollac…
##  8 marine fishes saithe                  actinoptery… gadi… gadid… poll… virens 
##  9 marine fishes lined surgeonfish       actinoptery… perc… acant… acan… lineat…
## 10 marine fishes orangespine unicornfish actinoptery… perc… acant… naso  litura…
## # ℹ 559 more rows
```

**5. The variable `taxon` identifies the common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
taxon_counts <- table(homerange$taxon)
taxon_counts
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
select(homerange, "species","trophic.guild")
```

```
## # A tibble: 569 × 2
##    species     trophic.guild
##    <chr>       <chr>        
##  1 rostrata    carnivore    
##  2 poecilura   carnivore    
##  3 anomalum    carnivore    
##  4 funduloides carnivore    
##  5 cataractae  carnivore    
##  6 masquinongy carnivore    
##  7 pollachius  carnivore    
##  8 virens      carnivore    
##  9 lineatus    herbivore    
## 10 lituratus   herbivore    
## # ℹ 559 more rows
```

```r
carnivore <- filter(homerange, trophic.guild == "carnivore")
summary(carnivore$species)
```

```
##    Length     Class      Mode 
##       342 character character
```


```r
herbivore <- filter(homerange, trophic.guild == "herbivore")
summary(herbivore$species)
```

```
##    Length     Class      Mode 
##       227 character character
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivore <- filter(homerange, trophic.guild == "carnivore")
herbivore <- filter(homerange, trophic.guild == "herbivore")
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
mean(carnivore$mean.hra.m2, na.rm = T)
```

```
## [1] 13039918
```


```r
mean(herbivore$mean.hra.m2, na.rm = T)
```

```
## [1] 34137012
```
herbivores have a larger average mean.ra.m2.

**9. Make a new dataframe `owls` that is limited to the mean mass, log10 mass, family, genus, and species of owls in the database. Which is the smallest owl? What is its common name? Do a little bit of searching online to see what you can learn about this species and provide a link below** 

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
owls <- select(homerange, "order","mean.mass.g","log10.mass","family","genus","species")
owls <- filter(owls, order == "strigiformes")
owls
```

```
## # A tibble: 9 × 6
##   order        mean.mass.g log10.mass family    genus      species    
##   <fct>              <dbl>      <dbl> <chr>     <chr>      <chr>      
## 1 strigiformes       119         2.08 strigidae aegolius   funereus   
## 2 strigiformes       252         2.40 strigidae asio       otus       
## 3 strigiformes       156.        2.19 strigidae athene     noctua     
## 4 strigiformes      2191         3.34 strigidae bubo       bubo       
## 5 strigiformes      1510         3.18 strigidae bubo       virginianus
## 6 strigiformes        61.3       1.79 strigidae glaucidium passerinum 
## 7 strigiformes      1920         3.28 strigidae nyctea     scandiaca  
## 8 strigiformes       519         2.72 strigidae strix      aluco      
## 9 strigiformes       285         2.45 tytonidae tyto       alba
```

smallest owl is species passerinum with a common name Eurasian pygmy owl
https://en.wikipedia.org/wiki/Eurasian_pygmy_owl 

**10. As measured by the data, which bird species has the largest homerange? Show all of your work, please. Look this species up online and tell me about it!**.  


```r
largest_homerange <- select(homerange, "mean.hra.m2", "species", "class", "common.name")
aves <- filter(largest_homerange, class == "aves")
```


```r
aves %>% 
  arrange(desc(mean.hra.m2)) 
```

```
## # A tibble: 140 × 4
##    mean.hra.m2 species      class common.name           
##          <dbl> <chr>        <chr> <chr>                 
##  1   241000000 cheriway     aves  caracara              
##  2   200980000 pygargus     aves  Montagu's harrier     
##  3   153860000 peregrinus   aves  peregrine falcon      
##  4   117300000 pennatus     aves  booted eagle          
##  5    84300000 camelus      aves  ostrich               
##  6    78500000 gallicus     aves  short-toed snake eagle
##  7    63585000 turtur       aves  European turtle dove  
##  8    63570000 percnopterus aves  Egyptian vulture      
##  9    50240000 buteo        aves  common buzzard        
## 10    50000000 biarmicus    aves  lanner falcon         
## # ℹ 130 more rows
```
the Caracara of the species cheriway has the largest homerange
The Caracara is a type of falcon. There are many different species of caracara and they live in many different places ranging from across the southern US and Central/South America.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
