Answers to Questions 1, 2, 3: 

## Question 1) 
Annotate the README.md file in your logistic growth repo with more detailed information about the analysis. Add a section on the results and include the estimates for N0, r and K (mention which *.csv file you used).

The analysis is based on the data provided in `experiment1.csv`.
The model parameters were estimated using a linear approximation method on the provided data. The estimates are as follows:

- \( N_0 \): 1330.74
- \( r \): 0.0095218
- \( K \): 5.979e+10

The estimates were obtained by fitting linear models to the data under different conditions.

Results

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

Code can be found here: https://github.com/1063086/logistic_growth/blob/0bfd8c20f86191fb04ebdaf2f5532566a7f25756/Question%203

## Comparison graph: 

![plot](https://github.com/nadiaangelab/logistic_growth/assets/150149096/9fd9e6d4-0976-4a89-930f-e24b8fc75e7e)

