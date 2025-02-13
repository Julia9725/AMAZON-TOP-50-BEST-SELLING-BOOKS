# AMAZON-TOP-50-BEST-SELLING-BOOKS

# INTRODUCTION
   Amazon is a e-commerce website were millions of different types of items are sold. Interestingly, Books was the first product sold on amazon by Jeff Bezos before he became the world’s richest person. Here, we will take a look at top 50 best selling books of amazon to derive some useful insights from them.
# BUSINESS PROBLEM
As a data analyst, Amazon marketing team and senior managers want me to run a descriptive analysis to find out some useful insights which can help them in effectively managing Books inventory so that they never run out of stock for most in demand books and I am also expected to find out if price has anything to do with a book being bestseller multiple times.

# ASSUMPTIONS

The information is still current and can be used to derive insights, which Amazon’s business team can further use to make strategic plans.
The company isn’t currently using any of the suggested solutions in the report.

# Work description
I will be analysing the data base Amazon Top 50 Bestselling Books, between 2019 and 2022, using R programming.

At the end I hop to answer the following questions:
* Which Genre is preferred more by customers?
* In non-fiction and fiction genre which author’s book has been bestseller multiple times?
* Which are the most in demand books that have been bestseller multiple times in different years?
* Are there any books from this 50 top selling books which have less than 4 ratings?
* Does price have any impact on the number of times a book has been bestseller?
* How is the ratings of this books by genre?

# PROCESS

1. Installing and loading common packages and libraries
 ```r
# This R environment comes with many helpful analytics packages installed

library(tidyverse)
library(ggplot2)
```
2. Data Importation
```r
bestsellers <- read.csv("'/kaggle/input/amazon-top-50-bestselling-books-2009-2019/bestsellers_with_categories_2022_03_27.csv')
```


#How many rows are in data frame?
```r
ncol(bestsellers)
7
```

#List of column names
```r
colnames(bestsellers)
'Name''Author''User Rating''Reviews''Price''Year''Genre'
 ```
#How many rows are in data frame?
```r
nrow(bestsellers)
550
```
#See the first 6 rows of data frame.
```r
head(bestsellers)
# A tibble: 6 × 7
  Name               Author `User Rating` Reviews Price  Year Genre
  <chr>              <chr>          <dbl>   <dbl> <dbl> <dbl> <chr>
1 10-Day Green Smoo… JJ Sm…           4.7   17350     8  2016 Non fiction
2 11/22/63: A Novel  Steph…           4.6    2052    22  2011 Fiction
3 12 Rules for Life… Jorda…           4.7   18979    15  2018 Non fictio
4 1984 (Signet Clas… Georg…           4.7   21424     6  2017 Fiction
5 5,000 Awesome Fac… Natio…           4.8    7665    12  2019 Non fiction
6 A Dance with Drag… Georg…           4.4   12643    11  2011 Fiction

```

#See list of columns and data types (numeric, character, etc)
```r
str(bestsellers)
spc_tbl_ [550 × 7] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ Name       : chr [1:550] "10-Day Green Smoothie Cleanse" "11/22/63: A Novel" "12 Rules for Life: An Antidote to Chaos" "1984 (Signet Classics)" ...
 $ Author     : chr [1:550] "JJ Smith" "Stephen King" "Jordan B. Peterson" "George Orwell" ...
 $ User Rating: num [1:550] 4.7 4.6 4.7 4.7 4.8 4.4 4.7 4.7 4.7 4.6 ...
 $ Reviews    : num [1:550] 17350 2052 18979 21424 7665 ...
 $ Price      : num [1:550] 8 22 15 6 12 11 30 15 3 8 ...
 $ Year       : num [1:550] 2016 2011 2018 2017 2019 ...
 $ Genre      : chr [1:550] "Non Fiction" "Fiction" "Non Fiction" "Fiction" ...
 - attr(*, "spec")=
  .. cols(
  ..   Name = col_character(),
  ..   Author = col_character(),
  ..   `User Rating` = col_double(),
  ..   Reviews = col_double(),
  ..   Price = col_double(),
  ..   Year = col_double(),
  ..   Genre = col_character()
  .. )
 - attr(*, "problems")=<externalptr>
```
# cleaning data

#Checking for duplicated data
```
sum(duplicated(bestsellers))
[1] 0

```
#Checking for missing data
```
sum(is.na(bestsellers))
0
```
#Checking if there are any nulls within the data.
```
anyNA(bestsellers)
FALSE
```
#Check if there is any misspellings or duplicate entries
```
print(sort(unique(bestsellers$Author)))
[1] "Abraham Verghese"                     
  [2] "Adam Gasiewski"                       
  [3] "Adam Mansbach"                        
  [4] "Adir Levy"                            
  [5] "Admiral William H. McRaven"           
  [6] "Adult Coloring Book Designs"          
  [7] "Alan Moore"                           
  [8] "Alex Michaelides"                     
  [9] "Alice Schertle"                       
 [10] "Allie Brosh"                          
 [11] "American Psychiatric Association"     
 [12] "American Psychological Association"   
 [13] "Amor Towles"                          
 [14] "Amy Ramos"                            
 [15] "Amy Shields"                          
 [16] "Andy Weir"                            
 [17] "Angie Grace"                          
 [18] "Angie Thomas"                         
 [19] "Ann Voskamp"                          
 [20] "Ann Whitford Paul"                    
 [21] "Anthony Bourdain"                     
 [22] "Anthony Doerr"                        
 [23] "Atul Gawande"                         
 [24] "Audrey Niffenegger"                   
 [25] "B. J. Novak"                          
 [26] "Bessel van der Kolk M.D."             
 [27] "Bill Martin Jr."                      
 [28] "Bill O'Reilly"                        
 [29] "Bill Simmons"                         
 [30] "Blue Star Coloring"                   
 [31] "Bob Woodward"                         
 [32] "Brandon Stanton"                      
 [33] "Brené Brown"                          
 [34] "Brian Kilmeade"                       
 [35] "Bruce Springsteen"                    
 [36] "Carol S. Dweck"                       
 [37] "Celeste Ng"                           
 [38] "Charlaine Harris"                     
 [39] "Charles Duhigg"                       
 [40] "Charles Krauthammer"                  
 [41] "Cheryl Strayed"                       
 [42] "Chip Gaines"                          
 [43] "Chip Heath"                           
 [44] "Chris Cleave"                         
 [45] "Chris Kyle"                           
 [46] "Chrissy Teigen"                       
 [47] "Christina Baker Kline"                
 [48] "Christopher Paolini"                  
 [49] "Coloring Books for Adults"            
 [50] "Craig Smith"                          
 [51] "Crispin Boyer"                        
 [52] "Dale Carnegie"                        
 [53] "Dan Brown"                            
 [54] "Daniel H. Pink"                       
 [55] "Daniel James Brown"                   
 [56] "Daniel Kahneman"                      
 [57] "Daniel Lipkowitz"                     
 [58] "Dav Pilkey"                           
 [59] "Dave Ramsey"                          
 [60] "David Goggins"                        
 [61] "David Grann"                          
 [62] "David McCullough"                     
 [63] "David Perlmutter MD"                  
 [64] "David Platt"                          
 [65] "David Zinczenko"                      
 [66] "Deborah Diesen"                       
 [67] "Delegates of the Constitutional\u0085"
 [68] "Delia Owens"                          
 [69] "Dinah Bucholz"                        
 [70] "DK"                                   
 [71] "Don Miguel Ruiz"                      
 [72] "Donna Tartt"                          
 [73] "Doug Lemov"                           
 [74] "Dr. Seuss"                            
 [75] "Dr. Steven R Gundry MD"               
 [76] "Drew Daywalt"                         
 [77] "E L James"                            
 [78] "Eben Alexander"                       
 [79] "Edward Klein"                         
 [80] "Edward M. Kennedy"                    
 [81] "Elie Wiesel"                          
 [82] "Elizabeth Strout"                     
 [83] "Emily Winfield Martin"                
 [84] "Eric Carle"                           
 [85] "Eric Larson"                          
 [86] "Ernest Cline"                         
 [87] "F. A. Hayek"                          
 [88] "F. Scott Fitzgerald"                  
 [89] "Francis Chan"                         
 [90] "Fredrik Backman"                      
 [91] "Gallup"                               
 [92] "Garth Stein"                          
 [93] "Gary Chapman"                         
 [94] "Gayle Forman"                         
 [95] "Geneen Roth"                          
 [96] "George Orwell"                        
 [97] "George R. R. Martin"                  
 [98] "George R.R. Martin"                   
 [99] "George W. Bush"                       
[100] "Giles Andreae"                        
[101] "Gillian Flynn"                        
[102] "Glenn Beck"                           
[103] "Golden Books"                         
[104] "Greg Mortenson"                       
[105] "Harper Lee"                           
[106] "Heidi Murkoff"                        
[107] "Hillary Rodham Clinton"               
[108] "Hopscotch Girls"                      
[109] "Howard Stern"                         
[110] "Ian K. Smith M.D."                    
[111] "Ina Garten"                           
[112] "J. D. Vance"                          
[113] "J. K. Rowling"                        
[114] "J.K. Rowling"                         
[115] "James Comey"                          
[116] "James Dashner"                        
[117] "James Patterson"                      
[118] "Jay Asher"                            
[119] "Jaycee Dugard"                        
[120] "Jeff Kinney"                          
[121] "Jen Sincero"                          
[122] "Jennifer Smith"                       
[123] "Jill Twiss"                           
[124] "Jim Collins"                          
[125] "JJ Smith"                             
[126] "Joanna Gaines"                        
[127] "Joel Fuhrman MD"                      
[128] "Johanna Basford"                      
[129] "John Green"                           
[130] "John Grisham"                         
[131] "John Heilemann"                       
[132] "Jon Meacham"                          
[133] "Jon Stewart"                          
[134] "Jonathan Cahn"                        
[135] "Jordan B. Peterson"                   
[136] "Julia Child"                          
[137] "Justin Halpern"                       
[138] "Kathryn Stockett"                     
[139] "Keith Richards"                       
[140] "Ken Follett"                          
[141] "Kevin Kwan"                           
[142] "Khaled Hosseini"                      
[143] "Kristin Hannah"                       
[144] "Larry Schweikart"                     
[145] "Laura Hillenbrand"                    
[146] "Laurel Randolph"                      
[147] "Lin-Manuel Miranda"                   
[148] "Lysa TerKeurst"                       
[149] "M Prefontaine"                        
[150] "Madeleine L'Engle"                    
[151] "Malcolm Gladwell"                     
[152] "Margaret Atwood"                      
[153] "Margaret Wise Brown"                  
[154] "Marie Kondō"                          
[155] "Marjorie Sarnat"                      
[156] "Mark Hyman M.D."                      
[157] "Mark Manson"                          
[158] "Mark Owen"                            
[159] "Mark R. Levin"                        
[160] "Mark Twain"                           
[161] "Markus Zusak"                         
[162] "Marty Noble"                          
[163] "Mary Ann Shaffer"                     
[164] "Maurice Sendak"                       
[165] "Melissa Hartwig Urban"                
[166] "Michael Lewis"                        
[167] "Michael Pollan"                       
[168] "Michael Wolff"                        
[169] "Michelle Obama"                       
[170] "Mike Moreno"                          
[171] "Mitch Albom"                          
[172] "Muriel Barbery"                       
[173] "Naomi Kleinberg"                      
[174] "Nathan W. Pyle"                       
[175] "National Geographic Kids"             
[176] "Neil deGrasse Tyson"                  
[177] "Paper Peony Press"                    
[178] "Patrick Lencioni"                     
[179] "Patrick Thorpe"                       
[180] "Paul Kalanithi"                       
[181] "Paula Hawkins"                        
[182] "Paula McLain"                         
[183] "Paulo Coelho"                         
[184] "Pete Souza"                           
[185] "Peter A. Lillback"                    
[186] "Phil Robertson"                       
[187] "Pierre Dukan"                         
[188] "Pretty Simple Press"                  
[189] "R. J. Palacio"                        
[190] "Rachel Hollis"                        
[191] "Raina Telgemeier"                     
[192] "Randall Munroe"                       
[193] "Randy Pausch"                         
[194] "Ray Bradbury"                         
[195] "Rebecca Skloot"                       
[196] "Ree Drummond"                         
[197] "RH Disney"                            
[198] "Rick Riordan"                         
[199] "Rob Bell"                             
[200] "Rob Elliott"                          
[201] "Robert Jordan"                        
[202] "Robert Munsch"                        
[203] "Rod Campbell"                         
[204] "Roger Priddy"                         
[205] "Ron Chernow"                          
[206] "Rupi Kaur"                            
[207] "Rush Limbaugh"                        
[208] "Samin Nosrat"                         
[209] "Sandra Boynton"                       
[210] "Sara Gruen"                           
[211] "Sarah Palin"                          
[212] "Sarah Young"                          
[213] "Sasha O'Hara"                         
[214] "Scholastic"                           
[215] "School Zone"                          
[216] "Sherri Duskey Rinker"                 
[217] "Sheryl Sandberg"                      
[218] "Silly Bear"                           
[219] "Stephen Kendrick"                     
[220] "Stephen King"                         
[221] "Stephen R. Covey"                     
[222] "Stephenie Meyer"                      
[223] "Steve Harvey"                         
[224] "Steven D. Levitt"                     
[225] "Stieg Larsson"                        
[226] "Susan Cain"                           
[227] "Suzanne Collins"                      
[228] "Ta-Nehisi Coates"                     
[229] "Tara Westover"                        
[230] "Tatiana de Rosnay"                    
[231] "The College Board"                    
[232] "The Staff of The Late Show with\u0085"
[233] "The Washington Post"                  
[234] "Thomas Campbell"                      
[235] "Thomas Piketty"                       
[236] "Thug Kitchen"                         
[237] "Timothy Ferriss"                      
[238] "Tina Fey"                             
[239] "Todd Burpo"                           
[240] "Tony Hsieh"                           
[241] "Tucker Carlson"                       
[242] "Veronica Roth"                        
[243] "W. Cleon Skousen"                     
[244] "Walter Isaacson"                      
[245] "William Davis"                        
[246] "William P. Young"                     
[247] "Wizards RPG Team"                     
[248] "Zhi Gang Sha"
```
# STATISTICAL SUMMARY
```
summary(bestsellers)
Name              Author           User Rating   
 Length:550         Length:550         Min.   :3.300  
 Class :character   Class :character   1st Qu.:4.500  
 Mode  :character   Mode  :character   Median :4.700  
                                       Mean   :4.618  
                                       3rd Qu.:4.800  
                                       Max.   :4.900  
    Reviews          Price            Year         Genre          
 Min.   :   37   Min.   :  0.0   Min.   :2009   Length:550        
 1st Qu.: 4058   1st Qu.:  7.0   1st Qu.:2011   Class :character  
 Median : 8580   Median : 11.0   Median :2014   Mode  :character  
 Mean   :11953   Mean   : 13.1   Mean   :2014                     
 3rd Qu.:17253   3rd Qu.: 16.0   3rd Qu.:2017                     
 Max.   :87841   Max.   :105.0   Max.   :2019
```
* Most of the books have a rating between 4.7 and 4.9 with a median rating of 4.7
* The number of book reviews was under 20000 reviews for most books with a median of 8580 reviews per book
* The most common prices for books were less than 15 dollars with a median of 11 dollars

#BOOKS BY GENRE
#Show how many book Genres
```
length(unique(bestsellers$Genre))
2
```
unique(bestsellers$Genre)
"Non Fiction" "Fiction"
```
table(bestsellers$Genre)
Fiction Non Fiction 
 240         310
 ```

#Pie chart of book genres
```r
ggplot(data=bestsellers, aes(x = "", fill = Genre)) +
  geom_bar(width = 1, position = "fill") + 
  coord_polar(theta = "y") +
  labs(fill = "Genre") +
  ggtitle("Distribution of Book Genres")
```
![image](https://github.com/user-attachments/assets/40cd57c0-3a6e-4dd6-8d1c-c3b168d05b90)

* There're only to types of book genre, Fiction and non fiction
* Percentage of Fiction Genre = 46.49%
* Percentage of Non Fiction Genre = 53.51%
* The reader prefer more Non Fiction books
  

 #Show how many Authors
 ```
print(length(unique(bestsellers$Author)))
[1] 248
```
#Show how many books
```
print(length(unique(bestsellers$Name)))
[1] 351
```

There are 248 different authors and 351 books listed in the top 50 best selling books for the period 2009-2019

#To know the Author with more books published
```r
df_books_in_author_desc<-bestsellers%>%
group_by(Author)%>%
summarise(count_Author=n())%>%
arrange(desc(count_Author))
head(df_books_in_author_desc)
 Author                             count_Author
  <chr>                                     <int>
1 Jeff Kinney                                  12
2 Gary Chapman                                 11
3 Rick Riordan                                 11
4 Suzanne Collins                              11
5 American Psychological Association           10
6 Dr. Seuss                                     9
 ```
The Author with more books published is Jeff Kinney and Gary Chapman


#Average Price of Books by the most prolific Authors
```r
top_author <- bestsellers %>%
  group_by(Author) %>%
  summarise(Num_Books = n_distinct(Name),
            Ave_Price = mean(Price)) %>%
  arrange(desc(Num_Books)) %>%
  head(15)
top_author
# A tibble: 15 × 3
   Author           Num_Books Ave_Price
   <chr>                <int>     <dbl>
 1 Jeff Kinney             12      9.25
 2 Rick Riordan            10      9.91
 3 Stephenie Meyer          7     19.9 
 4 Bill O'Reilly            6     10.6 
 5 Dav Pilkey               6      6.29
 6 J.K. Rowling             6     20.2 
 7 E L James                5     15.3 
 8 John Grisham             5     16.2 
 9 Suzanne Collins          5     13.4 
10 Charlaine Harris         4     10.2 
11 Stephen King             4     16.8 
12 Stieg Larsson            4      9.5 
13 Dan Brown                3     15.3 
14 Gary Chapman             3     17.2 
15 Glenn Beck               3      8
```

#Horizontal bar plot for the top authors with the most books
```r
ggplot(top_author, aes(x = reorder(Author, Ave_Price), y = Ave_Price)) +
  geom_bar(stat = "identity", fill = "lightblue") +
  labs(x = "Author", y = "Avg_Price") +
  ggtitle("Author name vs Average Price Books") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1
  ```
![image](https://github.com/user-attachments/assets/39321f23-5403-4800-9475-dc9c5ccb4b68)


* The author J. K. Rowling has the highest average price per book 23.9
* The autor Dav Pilkey has the lowest average price per book 6.33

  #Authors who achieved highest ratings and median reviews for their books ranked by price
  ```r
   best_author <- bestsellers %>%
    filter("User_Rating" > 4.8 & "Reviews" >= 8580) %>%
    group_by(Name) %>%
    distinct(Name, .keep_all = TRUE) %>%
    arrange(desc(Reviews)) %>%
    head(15)
  best_author
  #A tibble: 15 × 7
   Name              Author `User Rating` Reviews Price  Year Genre
   <chr>             <chr>          <dbl>   <dbl> <dbl> <dbl> <chr>
  1 Where the Crawda… Delia…           4.8   87841    15  2019 Fiction…
  2 The Girl on the … Paula…           4.1   79446    18  2015 Fiction…
  3 Becoming          Miche…           4.8   61133    11  2018 Non Fiction…
  4 Gone Girl         Gilli…           4     57271    10  2012 Fiction…
  5 The Fault in Our… John …           4.7   50482    13  2012 Fiction…
  6 The Nightingale:… Krist…           4.8   49288    11  2015 Fiction…
  7 Fifty Shades of … E L J…           3.8   47265    14  2012 Fiction…
  8 The Martian       Andy …           4.7   39459     9  2015 Fiction…
  9 All the Light We… Antho…           4.6   36348    14  2014 Fiction…
  10 The Alchemist     Paulo…           4.7   35799    39  2014 Fiction…
  11 The Goldfinch: A… Donna…           3.9   33844    20  2013 Fiction…
  12 The Hunger Games  Suzan…           4.7   32122    14  2010 Fiction…
  13 The Hunger Games… Suzan…           4.7   32122     8  2011 Fiction…
  14 The Wonky Donkey  Craig…           4.8   30183     4  2018 Fiction…
  15 Unbroken: A Worl… Laura…           4.8   29673    16  2010 Non Fiction …
```
* The Non fiction book with the highest rating vs. high number of reviews is "Becoming" from Michelle Obama
* The fiction book with the highest rating vs. high number of reviews is "Where the crawdads sing" from Delia Owen.


#Books which achieved the worst ratings (lower than 4)
```r
worst_author <- bestsellers %>%
    filter("User_Rating" < 4 & "Reviews" >= 8580) %>%
    group_by(Name) %>%
    distinct(Name, .keep_all = TRUE) %>%
    arrange(desc(Reviews))
worst_author
[1] 0
```
![Sheet 1 (1)](https://github.com/user-attachments/assets/0ffc79b4-48fc-4d9a-a63c-bf4ed0d39e0b)

Ratings of Fiction and Non fiction
```


#Author review
```r
 author_reviews <- bestsellers %>%
  group_by(Author) %>%
  distinct(Name, .keep_all = TRUE) %>%
  summarise(Number_Reviews = sum(Reviews, na.rm = TRUE)) %>%
  arrange(desc(Number_Reviews)) %>%
  top_n(15, wt = Number_Reviews)
 author_reviews
   Author          Number_Reviews
    <chr>                    <dbl>
   1 E L James               130746
   2 Suzanne Collins         130548
   3 Delia Owens              87841
   4 Paula Hawkins            79446
   5 J.K. Rowling             70535
   6 Jeff Kinney              67482
   7 Michelle Obama           61133
   8 John Grisham             60961
   9 John Green               58973
   10 Dan Brown                57302
   11 Gillian Flynn            57271
   12 Bill O'Reilly            54445
   13 Veronica Roth            51092
   14 Kristin Hannah           49288
   15 Dav Pilkey               44261
```


#Top 15 reviews by Book and by Author
```r
 book_reviews <- bestsellers %>%
  group_by(Name) %>%
  distinct(Author, .keep_all = TRUE) %>%
  summarise(Number_Reviews = sum(Reviews, na.rm = TRUE)) %>%
  arrange(desc(Number_Reviews)) %>%
  top_n(15, wt = Number_Reviews)
 book_reviews
    A tibble: 15 × 2
   Name                                              Number_Reviews
   <chr>                                                      <dbl>
   1 Where the Crawdads Sing                                    87841
   2 The Girl on the Train                                      79446
   3 Becoming                                                   61133
   4 Gone Girl                                                  57271
   5 The Fault in Our Stars                                     50482
   6 The Nightingale: A Novel                                   49288
   7 Fifty Shades of Grey: Book One of the Fifty Shad…          47265
   8 The Martian                                                39459
   9 All the Light We Cannot See                                36348
   10 The Alchemist                                              35799
   11 The Goldfinch: A Novel (Pulitzer Prize for Ficti…          33844
   12 The Hunger Games                                           32122
   13 The Hunger Games (Book 1)                                  32122
   14 The Wonky Donkey                                           30183
   15 Unbroken: A World War II Story of Survival, Resi…          29673 
```



# Conclusions :
Non-Fiction books were bestsellers 310 times and fictional books were best sellers 240 times
* On an average Non-Fiction books are more costly than fiction books
* On an average both genre had near about same ratings.
* Books from only 5 authors were bestselling for 10 times or more times.
* Irrespective of price, books have been bestsellers once or multiple times.

# Recommendations :
The recommendations are based on the insights derived from the data and will help in inventory management. In order to put the suggestions in action data visuals can be used as a reference.

* Its better to have non-fiction books more in stock than fiction books, as more people prefer to read them.
* It’s vital and advised to keep stock of all those books which are found to have been bestsellers multiple times as that means they have been most in demand.
* In general as price doesn’t play a role in a book being bestseller multiple times, it shouldn’t be considered while managing inventory.
* Ensuring that we have the books from authors who are well preferred in a particular and well known among readers is important. Good thing is, we now know authors whose 
  books were bestsellers multiple times in a decade, so having stock of books written by them is important.
