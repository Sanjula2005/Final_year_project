# Feature Dictionary

This document describes the context features selected for the recommendation model, the transformations applied during preprocessing, the reason for each transformation, and the final meaning of each feature.

## Selected Context Features

| Feature | Original column(s) | Transformation | Reason | Final meaning |
|---|---|---|---|---|
| city | city | OneHotEncoder | Represents business location | Business city |
| sector | sector | OneHotEncoder | Represents business type | Business sector |
| female_majority_owned | female_majority_owned | StandardScaler | Represents ownership context | Whether the business is majority female-owned |
| migrant_owner | migrant_owner | StandardScaler | Represents owner background | Whether the owner is a migrant |
| previously_unemployed_owner | previously_unemployed_owner | StandardScaler | Represents owner employment background | Whether the owner was previously unemployed |
| primary_income_earner | primary_income_earner | StandardScaler | Represents household income responsibility | Whether the owner is the primary income earner |
| owner_has_contract_job | owner_has_contract_job | StandardScaler | Represents owner's employment context | Whether the owner has a contract job |
| household_size_proxy | household_size_proxy | StandardScaler | Represents household context | Household size |
| employee_count | employee_count | StandardScaler | Represents business scale | Number of employees |
| bank_account | bank_account | StandardScaler | Represents financial access | Whether the business/owner has a bank account |
| has_loan | has_loan | StandardScaler | Represents access to credit | Whether the business/owner has a loan |
| friends_family_finance | friends_family_finance | StandardScaler | Represents informal financing access | Whether financing is obtained from friends/family |
| sells_on_credit | sells_on_credit | StandardScaler | Represents business credit practices | Whether the business sells on credit |
| buys_on_credit | buys_on_credit | StandardScaler | Represents purchasing credit practices | Whether the business buys on credit |
| mobile_money | mobile_money | StandardScaler | Represents digital financial access | Whether mobile money is used |
| computer_or_tablet | computer_or_tablet | StandardScaler | Represents technology access | Whether a computer/tablet is available |
| electricity | electricity | StandardScaler | Represents infrastructure access | Whether electricity is available |
| digital_adoption_score | digital_adoption_score | StandardScaler | Represents digital adoption | Level of digital adoption |
| household_based_business | household_based_business | StandardScaler | Represents business location/context | Whether the business is household-based |
| non_fixed_premises | non_fixed_premises | StandardScaler | Represents business premises | Whether the business operates from a non-fixed premises |
| pl_statement | pl_statement | StandardScaler | Represents financial record keeping | Whether a profit/loss statement is maintained |
| management_score_proxy | management_score_proxy | StandardScaler | Represents management capability | Management score |
| monthly_revenue_proxy_inr | monthly_revenue_proxy_inr | log1p + StandardScaler | Financial feature is right-skewed | Normalized log monthly revenue |
| monthly_profit_proxy_inr | monthly_profit_proxy_inr | log1p + StandardScaler | Financial feature is highly right-skewed | Normalized log monthly profit |
| profit_margin | monthly_profit_proxy_inr / monthly_revenue_proxy_inr | Ratio + StandardScaler | Represents profitability relative to revenue | Profit as a proportion of revenue |
| revenue_per_employee | monthly_revenue_proxy_inr / employee_count | Ratio + log1p + StandardScaler | Represents revenue generated per employee and is right-skewed | Revenue generated per employee |
| finance_constraint | finance_constraint | StandardScaler | Represents financial difficulty | Financial constraint level |
| customer_reach_constraint | customer_reach_constraint | StandardScaler | Represents customer access difficulty | Customer reach constraint level |
| management_constraint | management_constraint | StandardScaler | Represents management difficulty | Management constraint level |

## Engineered Features

### profit_margin

Calculated as:

`monthly_profit_proxy_inr / monthly_revenue_proxy_inr`

The calculation safely handles zero revenue by assigning a value of 0 when revenue is zero.

### revenue_per_employee

Calculated as:

`monthly_revenue_proxy_inr / employee_count`

The calculation safely handles zero employees by assigning a value of 0 when employee count is zero.

## Skewness and Log Transformation

Skewness was investigated before applying transformations.

The following financial features showed substantial right skewness and were transformed using `np.log1p()`:

- `monthly_revenue_proxy_inr`
- `monthly_profit_proxy_inr`
- `revenue_per_employee`

Binary/contextual variables were not log-transformed even when they had high skewness because their skewness was caused by an imbalanced binary distribution.

`profit_margin` and `management_score_proxy` were retained without log transformation.

## Excluded Features

| Feature | Reason for exclusion |
|---|---|
| business_id | Identifier only; does not represent business context |
| country | Constant value across the dataset (India), so it provides no useful variation |
| data_origin | Constant metadata field, so it provides no useful variation |
| profit_last_month | Excluded as an outcome/reward-related variable to reduce the risk of target leakage |

## Preprocessing

- `city` and `sector` are encoded using `OneHotEncoder(handle_unknown="ignore")`.
- Numerical features are standardized using `StandardScaler`.
- Selected skewed financial features are transformed using `np.log1p()` before scaling.
- The preprocessing pipeline is fitted only on the training data.
- The fitted pipeline is then used to transform both training and test data.
- Unselected columns are dropped from the preprocessing pipeline.

## Final Context Vectors

The preprocessing pipeline produces:

- Training samples: **798**
- Test samples: **200**
- Final features per sample: **38**

The 38 final features consist of:

- 24 regular numerical features
- 3 log-transformed numerical features
- 8 one-hot encoded city features
- 3 one-hot encoded sector features

The resulting vectors are saved as:

- `train_context_vectors.csv`
- `test_context_vectors.csv`

The fitted preprocessing pipeline is saved as:

- `preprocessing_pipeline.pkl`