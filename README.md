- # Economics Dataset Analysis and Visualization in R
This repository contains an R script for analyzing and visualizing the economics dataset using various plots including a correlation heatmap and time series plots.
The script utilizes popular R libraries like ggplot2, tidyr, dplyr, and reshape2 for data manipulation and visualization.

- # Prerequisites
Ensure you have the following R packages installed:
ggplot2,tidyr, dplyr, reshape2, gridExtra
If not, you can install the libaries:
install.packages("ggplot2")
install.packages("tidyr")
install.packages("dplyr")
install.packages("reshape2")
install.packages("gridExtra")

- # Step 1: Loading the libraries
library(ggplot2)
library(tidyr)
library(dplyr)
library(reshape2)
library(gridExtra)

- # Step 2: Dataset Loading and Preparation
# loads the economics dataset
data(economics)
# converts the date column to Date format for proper time series analysis
economics$date <- as.Date(economics$date)

- # Step 3: Correlation Heatmap
cor_matrix <- cor(economics[, -1])
melted_cor_matrix <- melt(cor_matrix)

ggplot(data = melted_cor_matrix, aes(x = Var1, y = Var2, fill = value)) +
  geom_tile(color = "white") +
  scale_fill_gradient2(low = "blue", high = "red", mid = "white",
                       midpoint = 0, limit = c(-1, 1), space = "Lab",
                       name = "Correlation") +
  geom_text(aes(label = round(value, 2)), color = "black", size = 4) +
  theme_minimal() + 
  theme(axis.text.x = element_text(angle = 45, vjust = 1, 
                                   size = 12, hjust = 1)) +
  coord_fixed() +
  labs(title = "Correlation Heatmap for Economics Dataset",
       x = "Variables",
       y = "Variables")
       
- # Step 4: Time Series Plot of Unemployment Rate
plot_unemployment <- ggplot(data = economics, aes(x = date, y = uempmed)) +
  geom_line(color = "blue") +
  labs(title = "Unemployment Rate Over Time",
       x = "Date",
       y = "Unemployment Rate") +
  theme_minimal()

plot_unemployment

- # Step 5: Time Series Plot of Personal Consumption Expenditures
plot_consumption <- ggplot(data = economics, aes(x = date, y = pce)) +
  geom_line(color = "red") +
  labs(title = "Personal Consumption Expenditures Over Time",
       x = "Date",
       y = "Personal Consumption Expenditures") +
  theme_minimal()

plot_consumption

- # Step 6: Grid Plot of Multiple Variables
plot_pce <- ggplot(data = economics, aes(x = date, y = pce)) +
  geom_line(color = "blue") +
  labs(title = "Personal Consumption Expenditures Over Time", x = "Date", y = "PCE") +
  theme_minimal()

plot_pop <- ggplot(data = economics, aes(x = date, y = pop)) +
  geom_line(color = "green") +
  labs(title = "Population Over Time", x = "Date", y = "Population") +
  theme_minimal()

plot_psavert <- ggplot(data = economics, aes(x = date, y = psavert)) +
  geom_line(color = "red") +
  labs(title = "Personal Savings Rate Over Time", x = "Date", y = "Savings Rate") +
  theme_minimal()

plot_uempmed <- ggplot(data = economics, aes(x = date, y = uempmed)) +
  geom_line(color = "purple") +
  labs(title = "Median Duration of Unemployment Over Time", x = "Date", y = "Median Unemployment Duration") +
  theme_minimal()

plot_unemploy <- ggplot(data = economics, aes(x = date, y = unemploy)) +
  geom_line(color = "orange") +
  labs(title = "Number of Unemployed Over Time", x = "Date", y = "Unemployed") +
  theme_minimal()

grid.arrange(plot_pce, plot_pop, plot_psavert, plot_uempmed, plot_unemploy, ncol = 2, nrow = 3)

- # Output
The script will generate the following visualizations:

A correlation heatmap of the variables in the economics dataset.
A time series plot of the unemployment rate (uempmed) over time.
A time series plot of personal consumption expenditures (pce) over time.
A grid of time series plots for the variables (pce, pop, psavert, uempmed, unemploy).





