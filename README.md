Answers to Questions 1, 2, 3: 

## Question 1) 
Annotate the README.md file in your logistic growth repo with more detailed information about the analysis. Add a section on the results and include the estimates for N0, r and K (mention which *.csv file you used).

**A**: The analysis is based on the data provided in `experiment1.csv`, which is based on the logistic growth data of the bacterium *Escherichia coli* in a growth medium.

In the analysis we were seeking to find estimates for each of the parameters: 
 N_0 : Initial population size. In the context of logistic growth, it represents the population size at the starting point of the growth process.

r: Intrinsic growth rate. This parameter represents the rate at which the population grows when it is not constrained by resources. It influences the steepness of the growth curve.

K: Carrying capacity. This is the maximum population size that can be sustainably supported. As the population approaches this limit, the growth rate slows down, and the population eventually stabilizes.

```R
#Script to plot the logistic growth data

growth_data <- read.csv("experiment1.csv")

install.packages("ggplot2")
library(ggplot2)

ggplot(aes(t,N), data = growth_data) +
  
  geom_point() +
  
  xlab("t") +
  
  ylab("y") +
  
  theme_bw()

ggplot(aes(t,N), data = growth_data) +
  
  geom_point() +
  
  xlab("t") +
  
  ylab("y") +
  
  scale_y_continuous(trans='log10')
```
This shows that growth plateaus at a certain point and therefore gave the carrying capacty estimate of K = 5.979e+10
![5c4bb984-7594-4e07-bc1f-6a2ad55ae557](https://github.com/1063086/logistic_growth/assets/150149096/92da0d09-3eef-4a14-ab5b-dba207bb2cbd)

```R
growth_data <- read.csv("experiment1.csv")
install.packages("ggplot2")
library(ggplot2)

ggplot(aes(t,N), data = growth_data) +
  
  geom_point() +
  
  xlab("Time (min)") +
  
  ylab("N (# cells)") +
  
  theme_bw()
```
This can then detail the N_0 figure, which in this case is estimated to be 1330.74
![2463cd46-ce4e-40e2-93d6-90157bbe64df](https://github.com/1063086/logistic_growth/assets/150149096/4dfab289-be73-4ed0-a10d-738fcffc5bf7)

```R
growth_data <- read.csv("experiment1.csv")

#Case 1. K >> N0, t is small

data_subset1 <- growth_data %>% filter(t<1200) %>% mutate(N_log = log(N))

model1 <- lm(N_log ~ t, data_subset1)
summary(model1)

#Case 2. N(t) = K

data_subset2 <- growth_data %>% filter(t>2400)

model2 <- lm(N ~ 1, data_subset2)
summary(model2)
```
This can help inform us of an approximation for r. In this case we need to use the upper and lower bounds for t, so that we are accountingfor the time during the growth phase. 

The model parameters were estimated using a linear approximation method on the data. The estimates are as follows:

- \( N_0 \): 1330.74
- \( r \): 0.0095218
- \( K \): 5.979e+10

The estimates were obtained by fitting linear models to the data under different conditions.

**Results**

The logistic growth curve was plotted using the estimated parameters:

```R
# Logistic growth function
logistic_fun <- function(t) {
  N <- (N0 * K * exp(r * t)) / (K - N0 + N0 * exp(r * t))
  return(N)
}

# Given parameter estimates
N0 <- 1330.74
r <- 0.0095218
K <- 5.979e+10

# Plotting the logistic growth model
ggplot(aes(t, N), data = growth_data) +
  geom_function(fun = logistic_fun, colour = "red") +
  geom_point()
```

## Question 2)  
Using your estimates of N0 and r to calculate the population size at t = 4980 min, assuming that the population grows exponentially. How does it compare to the population size predicted under logistic growth?

**A**: 
Using my estimates in R: 
```R
# Given parameter estimates
N0 <- 1330.74
r <- 0.0095218

# Time point
t_exponential <- 4980

# Calculate population size under exponential growth
N_exponential <- N0 * exp(r * t_exponential)

# result
cat("Exponential Growth Population Size at t =", t_exponential, "min:", N_exponential, "\n")
Exponential Growth Population Size at t = 4980 min: 5.220522e+23

Compared to logistic growth
# Given parameter estimates
N0 <- 1330.74
r <- 0.0095218
K <- 5.979e+10

# Time point
t_logistic <- 4980

# Logistic growth function
logistic_fun <- function(t, N0, r, K) {
  N <- (N0 * K * exp(r * t)) / (K - N0 + N0 * exp(r * t))
  return(N)
}

# Calculate population size under logistic growth at t = 4980
N_logistic <- logistic_fun(t_logistic, N0, r, K)

# Display the result
cat("Logistic Growth Population Size at t =", t_logistic, "minutes:", N_logistic, "\n")
Logistic Growth Population Size at t = 4980 minutes: 5.979e+10
```
So considering that exponential growth population size at t = 4980 min is 5.220522e+23 compared to
logistic growth population size at t = 4980 minutes which is 5.979e+10, there is a significant difference here. The exponential growth model predicts a much larger population size compared to the logistic growth model. This difference is realtively expected since exponential growth model doesn't account for carrying capacity, will assume unlimited resources. On the other hand, logistic growth considers a carrying capacity (K) and therefore slows down growth as the population approaches this limit. In this case, it appears that the logistic growth model predicts a population size that is much smaller than the exponential growth model.

## Question 3) 
Add an R script to your repository that makes a graph comparing the exponential and logistic growth curves (using the same parameter estimates you found). Upload this graph to your repo and include it in the README.md file so it can be viewed in the repo homepage.

**A**: 
Code can be found here: https://github.com/1063086/logistic_growth/blob/0bfd8c20f86191fb04ebdaf2f5532566a7f25756/Question%203

## Comparison graph: 

![plot](https://github.com/nadiaangelab/logistic_growth/assets/150149096/9fd9e6d4-0976-4a89-930f-e24b8fc75e7e)

