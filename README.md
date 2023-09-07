# Rscript Projects
#### These are small projects I decided to work on to improve my R skills, they are very varied and all were done with the aim of filling gaps in my R scripting.

#### IMDB Web scraper
#installing packages
#install.packages("rvest")
#install.packages("dplyr")

library(rvest)
library(dplyr)

#adding link to IMDB current top 50 Adventure films and TV shows

link = "https://www.imdb.com/search/title/?genres=Adventure&ref_=nv_sr_srsg_0_tt_7_nm_0_q_adventure"

page = read_html(link)

#add variables
titles = page %>%
  html_nodes(".lister-item-header a") %>% 
  html_text()

titles

year = page %>%
  html_nodes(".text-muted.unbold") %>%
  html_text()

year

rating = page %>%
  html_nodes(".ratings-imdb-rating strong") %>%
  html_text()
rating
#ratings cause issue as list incldues movies not yet rated

description = page %>%
  html_nodes(".text-muted+ .text-muted , .ratings-bar+ .text-muted") %>%
  html_text()
description

#make a dataframe
movies = data.frame(titles, year, description, stringsAsFactors = FALSE)

#link to url
movie_url = page %>%
  html_nodes(".lister-item-header a") %>%
  html_attr("href") %>%
  paste("https://www.imdb.com", .,sep=" ")
movie_url

#make a dataframe + add url
movies = data.frame(titles, year, description,movie_url, stringsAsFactors = FALSE)
view(movies)



### Fibonacci sequence generator

x = as.integer(readline("How many terms of Fibonacci sequence do you want"))

fibonacci = function(x){

n1=0
n2=1
n3=n1+n2
count=2
if(x<=0){print("Please enter correct number of terms to be generated(postive integer)?")
  }else if (x==1){print("Fibonacci Sequence :")
print(n1)
  } else {
    print("Fibonacci Sequence :")
    print(n1)
    print(n2)
    while(count < x){
      n3=n1+n2
      print(n3)
      n1 = n2
      n2 = n3
      count = count +1
    }
  } 
}

fibonacci(x = as.integer(readline("how many terms do you want? :")))


##################################
### Calculator function
f= (readline("Do you want to Add(a)
             \n Subtract(s)
             \n Divide(d)
             \n Multiply(m)
             \n Modulo(mod)
             \n Power(p) :"))

x = as.numeric(readline("Enter your first number :"))
y = as.numeric(readline("Enter your second number:"))


result = switch(f, 
                "a" = cat("Addition =", x+y),
                "s" = cat("Subtraction =", x-y),
                "d" = cat("Division =", x/y),
                "m" = cat("Multiply =", x*y),
                "mod" = cat("Modulo =", x%%y),
                "p" = cat("Power =", x^y)
)


