# Lab

```
Assignment 1
c=c(5,10,15,20,25,30) //c() is a fnc that is used to "combine or concatenate". Used to create vectors(of same type/ if different values are mixed, R will convert them to the most general type) by combining multiple values into a single vector
```
cmax=max(c) //computes max and min values of c
cmin=min(c)

print(paste("max: ",cmax," min: ",cmin))

class(n) //returns the dataType of N

result<-switch(
  choice,
  "1"=inp1+inp2,
  "2"=inp2-inp1,
  "3"=inp1-inp2,
  "4"=inp1*inp2,
  "5"=inp2/inp1,
  "6"=inp1/inp2,
  stop("Invalid Choice")
)
print(paste("Result is: ",result))

plot(3,2)
plot(sin,-2*pi,2*pi)
plot(tan,-2*pi,2*pi)

bar=c(2,6,8,7,5)*10
barplot(bar,xlab="X axis",ylab="Y axis")

Assignment2

1. sample(dataSet,no of outcomes)
sample(data,no of outcomes, replace=TRUE, probSet ex- prob=c(0.9,0.1))

2.sapply(ns,funName) //sapply applies this function for each member of the ns vector or list, returns a vector
lapply(ns,funName) //returns a list

Assignment3
1. pnorm(jiskiPercentValueNikalniHo,Mean,SD,lower.tail = FALSE(optional, 1- nhi krna phdega))

2. ppois(x,lambda) Cumulative Probability, lambda = mean number of events
#helps compute cumulative probabilities directly instead of summing individual probabilities.

3. dpois(x,lambda) calculates the probability of exactly x events
This method explicitly sums the individual probabilities rather than computing the cumulative probability.

```
conditional_prob <- function(prob_a_and_b, prob_b) {
  return(prob_a_and_b / prob_b)
}

prob_cloudy <- 0.4
prob_rain <- 0.2
prob_cloud_given_rain <- 0.85

prob_rain_given_cloudy <-
  conditional_prob(prob_cloud_given_rain * prob_rain, prob_cloudy)

print(prob_rain_given_cloudy)
```
```
calculate_birthday_probability <- function(n) {
  prod <- 1
  for (i in 1:(n-1)) {
    prod <- prod * (1 - i / 365)
  }
  probability <- 1 - prod
  return(probability)
}

n <- 20
while (calculate_birthday_probability(n) <= 0.5) {
  n <- n + 1
}
cat("The smallest n where probability exceeds 0.5 is:", n, "\n")
```

```
stimulateBirthdayParties <- function(n, simulations=1000){
  matchCount=0
  for(i in 1:simulations){
    birthdays=sample(1:365,n,replace=TRUE)
    # print(birthdays)
    # print(unique(birthdays))
    if(length(unique(birthdays))<n){
      matchCount=matchCount+1
    }
  }

  prob = matchCount/simulations
  return(prob)
}

ns=5:50
prob = sapply(ns,stimulateBirthdayParties)
print(prob)
```

