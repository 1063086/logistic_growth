##1) (10 points) Annotate the README.md file in your logistic growth repo with more detailed information about the analysis. Add a section on the results and include the estimates for N0, r and K (mention which *.csv file you used).
This repository contains scripts for analyzing logistic growth data. The analysis is based on the data provided in `experiment1.csv`.
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

2) (10 points) Use your estimates of N0 and r to calculate the population size at t = 4980 min, assuming that the population grows exponentially. How does it compare to the population size predicted under logistic growth?

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


3) (20 points) Add an R script to your repository that makes a graph comparing the exponential and logistic growth curves (using the same parameter estimates you found). Upload this graph to your repo and include it in the README.md file so it can be viewed in the repo homepage.

Comparison graph; 
![153c0c14-e8e9-46c3-ae47-77b073187da8](https://github.com/nadiaangelab/logistic_growth/assets/150149096/c8a69443-23c9-4f99-a2b9-7f22c28a605c)

