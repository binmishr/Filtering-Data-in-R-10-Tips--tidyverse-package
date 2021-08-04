# Filtering-Data-in-R-10-Tips--tidyverse-package
filtering data in r, In this tutorial describes how to filter or extract data frame rows based on certain criteria.

In this tutorial, you will learn the filter R functions from the tidyverse package.

The main idea is to showcase different ways of filtering from the data set.

Filtering data is one of the common tasks in the data analysis process. When you want to remove or extract a part of the data use tidyverse package ’filter()’ function.
Load Library

library(tidyverse)
head(msleep)
name                       genus      vore  order        conservation sleep_total sleep_rem sleep_cycle awake  brainwt  bodywt
                                                                          
 1 Cheetah                    Acinonyx   carni Carnivora    lc                  12.1      NA        NA      11.9 NA        50    
 2 Owl monkey                 Aotus      omni  Primates     NA                  17         1.8      NA       7    0.0155    0.48 
 3 Mountain beaver            Aplodontia herbi Rodentia     nt                  14.4       2.4      NA       9.6 NA         1.35 
 4 Greater short-tailed shrew Blarina    omni  Soricomorpha lc                  14.9       2.3       0.133   9.1  0.00029   0.019
 5 Cow                        Bos        herbi Artiodactyla domesticated         4         0.7       0.667  20    0.423   600    
 6 Three-toed sloth           Bradypus   herbi Pilosa       NA                  14.4       2.2       0.767   9.6 NA         3.85 

We’ll use the R built-in msleep data set, which we will use for a different types of filtering.
Example 1

data1<-msleep %>%
  select(name,sleep_total) %>%
  filter(sleep_total>15)

Output:-

      name                           sleep_total                                    
  1 Owl monkey                            17  
  2 Long-nosed armadillo                  17.4
  3 North American Opossum                18  
  4 Big brown bat                         19.7
  5 Thick-tailed opposum                  19.4
  6 Little brown bat                      19.9
  7 Tiger                                 15.8
  8 Giant armadillo                       18.1
  9 Arctic ground squirrel                16.6
 10 Golden-mantled ground squirrel        15.9
 11 Eastern american chipmunk             15.8
 12 Tenrec                                15.6

Example 2

data2<-msleep %>%
  select(name,sleep_total) %>%
  filter(!sleep_total>15)

Output:-

     name                       sleep_total                                
  1 Cheetah                           12.1
  2 Mountain beaver                   14.4
  3 Greater short-tailed shrew        14.9
  4 Cow                                4  
  5 Three-toed sloth                  14.4
  6 Northern fur seal                  8.7
  7 Vesper mouse                       7  
  8 Dog                               10.1
  9 Roe deer                           3  
 10 Goat                               5.3

Example 3

Power analysis in Statistics with R »

data3<-msleep %>%
  select(name,order,bodywt,sleep_total) %>%
  filter(order=="Primates", bodywt>15)

Output:-

    name       order    bodywt sleep_total                     
 1 Human      Primates   62           8  
 2 Chimpanzee Primates   52.2         9.7
 3 Baboon     Primates   25.2         9.4

Example 4

Principal component analysis (PCA) in R »

data4<-msleep %>%
select(name, order, bodywt,sleep_total) %>%
  filter(order=="Primates" | bodywt>15)

Output:-

    name              order           bodywt sleep_total                                    
  1 Cheetah           Carnivora        50           12.1
  2 Owl monkey        Primates          0.48        17  
  3 Cow               Artiodactyla    600            4  
  4 Northern fur seal Carnivora        20.5          8.7
  5 Goat              Artiodactyla     33.5          5.3
  6 Grivet            Primates          4.75        10  
  7 Asian elephant    Proboscidea    2547            3.9
  8 Horse             Perissodactyla  521            2.9
  9 Donkey            Perissodactyla  187            3.1
 10 Patas monkey      Primates         10           10.9

Example 5

data5<-msleep %>%
  select(name,sleep_total) %>%
  filter(name=="Cow" |
           name=="Dog"|
           name=="Goat")

Output:-

   name  sleep_total          
 1 Cow           4  
 2 Dog          10.1
 3 Goat          5.3

Example 6

data6<-msleep %>%
  select(name, sleep_total) %>%
  filter(name %in% c("Cow","Dog","Goat"))

Output:-

   name  sleep_total          
 1 Cow           4  
 2 Dog          10.1
 3 Goat          5.3

Example 7

data7<-msleep %>%
  select(name, sleep_total) %>%
  filter(between(sleep_total,16,18))

Output:-

   name                   sleep_total                           
 1 Owl monkey                    17  
 2 Long-nosed armadillo          17.4
 3 North American Opossum        18  
 4 Arctic ground squirrel        16.6

Example 8

data8<-msleep %>%
  select(name, sleep_total) %>%
  filter(near(sleep_total,17, tol=0.5))

Output:-

   name                   sleep_total                           
 1 Owl monkey                    17  
 2 Long-nosed armadillo          17.4
 3 Arctic ground squirrel        16.6

Example 9

data9<-msleep %>%
  select(name, conservation,sleep_total) %>%
  filter(is.na(conservation))

Output:-

   name                        conservation sleep_total                                         
  1 "Owl monkey"                NA                  17  
  2 "Three-toed sloth"          NA                  14.4
  3 "Vesper mouse"              NA                   7  
  4 "African giant pouched rat" NA                   8.3
  5 "Western american chipmunk" NA                  14.9
  6 "Galago"                    NA                   9.8
  7 "Human"                     NA                   8  
  8 "Macaque"                   NA                  10.1
  9 "Vole "                     NA                  12.8
 10 "Little brown bat"          NA                  19.9

Example 10

data10<-msleep %>%   
select(name, conservation,sleep_total) %>%   
filter(!is.na(conservation)) 

Output:-

    name                       conservation sleep_total                                        
  1 Cheetah                    lc                  12.1
  2 Mountain beaver            nt                  14.4
  3 Greater short-tailed shrew lc                  14.9
  4 Cow                        domesticated         4  
  5 Northern fur seal          vu                   8.7
  6 Dog                        domesticated        10.1
  7 Roe deer                   lc                   3  
  8 Goat                       lc                   5.3
  9 Guinea pig                 domesticated         9.4
 10 Grivet                     lc                  10 
