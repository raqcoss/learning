# Statistics with R

###  '%whatever%' Notation
The dplyr package introduced the %.% operator to pass the left hand side as an argument of the function on the right hand side, similar to a *NIX pipe.

```
"%,%" <- function(x, y) paste0(x, ", ", y)

# test run

"Hello" %,% "World"
## [1] "Hello, World"
```


%>% is similar to pipe in Unix. For example, in

```
a <- combined_data_set %>% group_by(Outlet_Identifier) %>% tally()

this line is equivalent to
a <- tally(group_by(combined_data_set, Outlier_Identifier))
```
the output of combined_data_set will go into group_by and its output will go into tally, then the final output is assigned to a.

This gives you handy and easy way to use functions in series without creating variables and storing intermediate values.

```
head(food_consumption)
# A tibble: 6 × 4
  country   food_category consumption co2_emission
  <chr>     <fct>               <dbl>        <dbl>
1 Argentina pork                10.5         37.2 
2 Argentina poultry             38.7         41.5 
3 Argentina beef                55.5       1712   
4 Argentina lamb_goat            1.56        54.6 
5 Argentina fish                 4.36         6.96
6 Argentina eggs                11.4         10.5


food_consumption %>%
  # Filter for Belgium and USA
  filter(country %in% c("Belgium", "USA")) %>%
  # Group by country
  group_by(country)%>%
  # Get mean_consumption and median_consumption
  summarize(mean_consumption = mean(consumption),
      median_consumption = median(consumption))
# A tibble: 2 × 3
  country mean_consumption median_consumption
  <chr>              <dbl>              <dbl>
1 Belgium             42.1               12.6
2 USA                 44.6               14.6
```
Using ggplot2 histogram
```
food_consumption %>%
  # Filter for rice food category
  filter(food_category == "rice") %>%
  # Create histogram of co2_emission
  ggplot(aes(co2_emission)) +
    geom_histogram()
```
## Measures of Spread
### Variance
``` var(dataset$column_name)```
### Standard deviation
``` sd(dataset$column_name)```
### Mean Absolute Deviation
```
dists <- dataset$column_name - mean(dataset$column_name)
mean(abs(dists)
```
### Quartiles
```
quantile(dataset$column_name,probs=c(0.00,0.25,0.50,0.75,1.00))
quantile(dataset$column_name,probs = seq(0,1,1/5)) #seq(start, end, step)
ggplot(dataset, aes(y=column_name))+
  geom_boxplot()
```
### Interquartile Range (IQR)
distance between the 25th and 75th percentile
```
iqr <- quantile(dataset$column_name, 0.75) - quantile(dataset$column_name, 0.25)
```
### Ourtliers
if (data < Q1 - 1.5 * IQR | data > Q3 + 1.5 * IQR)
```
lower_threshold <- quantile(dataset$column_name,0.25) - 1.5 * iqr
upper_threshold <- quantile(dataset$column_name,0.75) + 1.5 * iqr
dataset %>% filter(column_name<lower_threshold | column_name>upper_threshold) %>%
  select(ID, name, column_name1, column_name2)
```
### Excercises
```
# Calculate variance and sd of co2_emission for each food_category
food_consumption %>% 
  group_by(food_category) %>% 
  summarize(var_co2 = var(co2_emission),
           sd_co2 = sd(co2_emission))

ggplot(food_consumption, aes(x=co2_emission)) +
  # Create a histogram
  geom_histogram() +
  # Create a separate sub-graph for each food_category
  facet_wrap(~food_category)
```
```
# Calculate total co2_emission per country: emissions_by_country
emissions_by_country <- food_consumption %>%
  group_by(country) %>%
  summarize(total_emission = sum(co2_emission))

# Compute the first and third quartiles and IQR of total_emission
q1 <- quantile(emissions_by_country$total_emission, 0.25)
q3 <- quantile(emissions_by_country$total_emission, 0.75)
iqr <- q3 - q1

# Calculate the lower and upper cutoffs for outliers
lower <- q1 - 1.5 * iqr
upper <- q3 + 1.5 * iqr

# Filter emissions_by_country to find outliers
emissions_by_country %>%
  filter(total_emission<lower | total_emission>upper)
```






