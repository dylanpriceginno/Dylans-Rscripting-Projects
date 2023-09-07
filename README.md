#### These are small projects I decided to work on to improve my R skills, they are very varied and all were done with the aim of filling gaps in my R scripting.

#### IMDB Web scraper

## Installation
Before using the IMDb Web Scraper, make sure to install the required packages by running the following commands:

install.packages("rvest")

install.packages("dplyr")

library(rvest)

library(dplyr)

## Usage

To scrape the current top 50 Adventure films and TV shows on IMDb, use the following code:

## Define the IMDb Adventure genre link
link <- "https://www.imdb.com/search/title/?genres=Adventure&ref_=nv_sr_srsg_0_tt_7_nm_0_q_adventure"

## Read the HTML page
page <- read_html(link)

## Extract movie titles
titles <- page %>%
  html_nodes(".lister-item-header a") %>%
  html_text()

## Extract release years
year <- page %>%
  html_nodes(".text-muted.unbold") %>%
  html_text()

## Extract ratings
rating <- page %>%
  html_nodes(".ratings-imdb-rating strong") %>%
  html_text()

#### I decided to exclude rating as some of the movies/tv did not have a review yet

## Extract movie descriptions
description <- page %>%
  html_nodes(".text-muted+ .text-muted , .ratings-bar+ .text-muted") %>%
  html_text()

## Extract URL
movie_url = page %>%
  html_nodes(".lister-item-header a") %>%
  html_attr("href") %>%
  paste("https://www.imdb.com", .,sep="")
movie_url

## Create a dataframe
movies = data.frame(titles, year, description,movie_url, stringsAsFactors = FALSE)

## View the dataframe
view(movies)

Results

![image](https://github.com/dylanpriceginno/Dylans-Rscripting-Projects/assets/85695465/afca8c60-105f-4ed5-979a-02e6d526aaf6)


## Fibonacci Sequence Generator
### Generate a Fibonacci sequence with a specified number of terms using the following code:

x <- as.integer(readline("How many terms of the Fibonacci sequence do you want?"))

fibonacci <- function(x) {
  n1 <- 0
  n2 <- 1
  n3 <- n1 + n2
  count <- 2
  
  if (x <= 0) {
    print("Please enter a correct number of terms to be generated (positive integer).")
  } else if (x == 1) {
    print("Fibonacci Sequence:")
    print(n1)
  } else {
    print("Fibonacci Sequence:")
    print(n1)
    print(n2)
    
    while (count < x) {
      n3 <- n1 + n2
      print(n3)
      n1 <- n2
      n2 <- n3
      count <- count + 1
    }
  }
}


## Fibnacci Sequence Generator in action

fibonacci(x)

How many terms of the Fibonacci sequence do you want?: 8

[1] "Fibonacci Sequence :"
[1] 0
[1] 1
[1] 1
[1] 2
[1] 3
[1] 5
[1] 8
[1] 13

## Calculator Function
### Perform basic mathematical operations with this calculator function:


f <- readline("Do you want to:\nAdd(a)\nSubtract(s)\nDivide(d)\nMultiply(m)\nModulo(mod)\nPower(p): ")

x <- as.numeric(readline("Enter your first number: "))

y <- as.numeric(readline("Enter your second number: "))

result <- switch(
  f,
  "a" = cat("Addition =", x + y),
  "s" = cat("Subtraction =", x - y),
  "d" = cat("Division =", x / y),
  "m" = cat("Multiply =", x * y),
  "mod" = cat("Modulo =", x %% y),
  "p" = cat("Power =", x^y)
)

## Calculator in Action

Do you want to:
Add(a)
Subtract(s)
Divide(d)
Multiply(m)
Modulo(mod)
Power(p): 

a

Enter your first number: 12

Enter your second number: 12

Addition = 24
