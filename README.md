# R-programming-practice-codes


### R practice codes and use cases for practice.


### Here's an example of a variable
first_variable = "This is my variable"
second_variable = 12.5

### to create vectors having similar datatypes, also checking the validity & length
vec_1 = c(13, 48.5, 71, 101.5,2)
vec_1
text_vector = c("Sarah", "Tokoni", "Barugu")
integer_vector = c(20L,78L)
typeof(vec_1)
typeof(text_vector)
length(integer_vector)
is.integer(integer_vector)

### renaming elements within a vector
x= c(1,3,5)
names(x) = c("first", "second", "third")
x

### to create list having different datatypes, also checking the validity & length as well as renaming the elements in the list
list("baba", 24L, 29.9, TRUE)
list(list(list(98L, 0.5)))
str(list("baba", 24L, 29.9, FALSE))
list("Blessing" = 1, "FALSE" = 5, "Virtue" = 10)

### Working with dates and time

today()
now()
ymd("2021-01-10")
dmy("15-09-2022")

### working with data frames-table creation as SQL. Not needed mostly cause needed files are largely imported.

data.frame(color=c("red","blue","green","yellow","orange"), amount=c(20L,15L,8L,25L,30L))

### create a folder to hold all files, create a blank file in a chosen file type.

dir.create("R_Files")
create files using file.create("new_text_file.txt"), file.create("new_word_file.docx"), file.create("new_csv_file.csv")
copy files to a folder using file.copy("new_text_file.txt","destination folder")
delete files using unlink("new_text_file.txt")

### working with Matrices, has same data type all through

matrix(c(10:24), nrow = 5)
matrix(c(1:6), ncol = 3)

### my first calculation

imago = 21
gengen = 16
difference = imago - gengen
difference

ogbonge = difference * 2
ogbonge

### logical operators: AND is &/&&, OR is |/||, NOT is !. Works similarly as like sql. AND operator must have both conditions true to return true while OR will need both conditions to be FALSE before returning false.

x=10
x> 2 & x<4
y=11
y<4 | y>20
creator != 23

### conditional statements: if(), else(), elseif()

x = 18
if (x>17){print("x is an adult")} else {print("x is a child")}

y = 20 
x = 25
if (x>17 & y <19){print("no classification")} else if(x>19 | y>20){print("valid classification")} else {"gangan"}

### using pipe for easier code reads, that is, for nested codes

install.packages("dplyr")
library(tidyverse)
library("dplyr")
(#load an already imported dataset) with data("named_dataset")
  View("named_dataset")
  filtered_tg = filter(named_dataset,column==value)
  arrange(filtered_tg,'column to sort or order by')
  
### to show the above query as a nested one using pipe
  
  filtered_dataset = "named_dataset" %>% 
    filter(column==value) %>%
    group_by("column") %>% 
    arrange('column to sort with' in asc) or (-"column to sort with" in desc)
  
  or
"dataframe" %>% group_by("column") %>% drop_na() %>% summarise("new_column_criteria_alias" = aggregate function("column"))

where drop_na eliminates all rows having na.action
summarize acts like having clause in sql
  

### using data to load, view to view, head to see the first six column headers, str to check structure of data frame, colname to see all column names, mutate to create a derived column. tibble is like a table view with just 10 rows in display, glimpse and skim without charts to see details of a dataframe
  
  data("diamonds")
  View(diamonds)
  head(diamonds)
  str(diamonds)
  glimpse(diamonds)
  skim_without_charts(diamonds)
  colnames(diamonds)
  as_tibble(diamonds)
  mutate(diamonds, new_column = old_column * 2) #to get a derived column
  separate(dataframe, column to separate, into = c("col1_name","col2_name"), sep="inside here should be the delimiter")
  unite(dataframe,"new column_name to merge"), col1_name, col2_name, sep="delimiter")

library(readxl)
read.csv()
readxl_example()  
read_excel(readxl_example("type-me.xlsx"))
excel_sheets(readxl_example("type-me.xlsx"))
read_excel(readxl_example("type-me.xlsx"), sheet= "numeric_coercion")  #to select a specific known sheet

install.packages("here")
library("here")
install.packages("skimr")
library("skimr")
install.packages("janitor")
library("janitor")
install.packages("dplyr")
library("dplyr")

### DATA CLEANING STEPS

"dataframe" %>% select(column) or select(-column) #to select specific column(s)
"dataframe" %>% rename(old_column = new_column)  #to change a column name
rename_with("dataframe",tolower) #to change all column names to lowercase or uppercase
clean_names("dataframe") #to remove all unnecessary characters except letter,number,underscores.
pivot_wider and pivot_longer() #to unpivot and pivot dataframes respectively

### to check for bias in R using SimDesign package. an unbiased outcome is closer to zero(actual outcome is higher than predicted by that amount) while a high result indicates bias(predicted outcome is larger than zero).

actual= c(23, 62, 28, 36, 88)
predicted= c(62, 36, 63, 48, 58)
bias(actual,predicted)

### To make a plot using R

ggplot(data=penguins)+geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,alpha=species,linetype=species,color=species,shape=species,size=species))

OR

ggplot(data=penguins)+geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g), color="red",shape="triangle")

OR

ggplot(data=diamonds)+geom_bar(mapping = aes(x=cut,fill=clarity))

ggplot(data=penguins)+geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g))+geom_smooth(mapping = aes(x=flipper_length_mm,y=body_mass_g))

### adding facets to one or more group

ggplot(data=penguins)+geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,color=species))+facet_wrap(~species)
ggplot(data=penguins)+geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,color=species))+facet_grid(sex~species)

### using filter from dplyr

data %>%
  filter(variable1 == "DS") %>%  
  ggplot(aes(x = weight, y = variable2, colour = variable1)) +  
  geom_point(alpha = 0.3,  position = position_jitter()) + stat_smooth(method = "lm")

### to add a title, subtitle, caption, annotation. You can assign the plot to a variable.

ggplot(data=penguins)+geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,color=species))+facet_grid(sex~species)+labs(title = "Palmer Penguins: Body Mass vs. Flipper Length",subtitle = "Sample of three penguin species",caption = "Data collected by Dr. Kristen Gorman")

ggplot(data=penguins)+geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,color=species))+facet_grid(sex~species)+labs(title = "Palmer Penguins: Body Mass vs. Flipper Length",subtitle = "Sample of three penguin species",caption = "Data collected by Dr. Kristen Gorman")+annotate("text",x=220,y=3500,label="The Gentoos are the largest",color="brown",fontface="bold",size=4.5,angle=25)

### to save our last visual plot using ggsave() function attached to any of the query example above

+ ggsave("Three Penguin Species.png")

