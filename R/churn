# ==========================================================

# Bank Customer Churn - Exploratory Analysis (R)

# Purpose: Recreate Excel insights (tables + visuals)

# Notes: No image saving (manual export is fine)

# ==========================================================

# ---------------------------

# 1) Packages

# ---------------------------

# Install once if needed:

# install.packages(c("dplyr", "ggplot2", "scales"))

library(dplyr)
library(ggplot2)
library(scales)

# ---------------------------

# 2) Load data

# ---------------------------

# "Bank Customer Churn Prediction2CSV.csv"

df <- read.csv("Bank Customer Churn Prediction2CSV.csv")

# ---------------------------

# 3) Keep only core columns (drop Excel helper columns)

# ---------------------------
df_clean <- df %>%

  dplyr::select(

    customer_id, credit_score, country, gender, age, tenure, balance,

    products_number, credit_card, active_member, estimated_salary, churn

  ) %>%

  mutate(

    churn = as.integer(churn),

    active_member = as.integer(active_member),

    credit_card = as.integer(credit_card),

    products_number = as.integer(products_number),

    age = as.numeric(age),

    balance = as.numeric(balance),

    estimated_salary = as.numeric(estimated_salary),

    country = as.factor(country),

    gender = as.factor(gender)

  )

# Quick checks (optional)

str(df_clean)

summary(df_clean)

# ---------------------------

# 4) Feature engineering

# ---------------------------

# Age bands (same logic as your Excel)

df_clean <- df_clean %>%

  mutate(

    age_band = case_when(
      age < 30 ~ "<30",
      age < 40 ~ "30-39",
      age < 50 ~ "40-49",
      age < 60 ~ "50-59",
      TRUE ~ "60+"

    ),

    age_band = factor(age_band, levels = c("<30", "30-39", "40-49", "50-59", "60+"))

  )

# Balance group (median split)

med_bal <- median(df_clean$balance, na.rm = TRUE)

df_clean <- df_clean %>%

  mutate(

    balance_group = if_else(balance >= med_bal, "high balance", "low balance"),

    balance_group = factor(balance_group, levels = c("low balance", "high balance"))

  )

# Overall churn rate

overall_churn <- mean(df_clean$churn, na.rm = TRUE)

cat("Overall churn rate:", percent(overall_churn, accuracy = 0.1), "\n")


# ---------------------------

# 5) Pivot-style summary tables

# ---------------------------
