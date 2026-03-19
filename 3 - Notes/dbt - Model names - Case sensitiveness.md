Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
When building dbt models, we should avoid using uppercase characters in model names. Otherwise, for example if we have model called `clientsTotalRevenue` we can get an error like this:
```bash
When searching for a relation, dbt found an approximate match. Instead of guessing
  which relation to use, dbt will move on. Please delete dwh_fact.customersTotalRevenue, or rename it to be less ambiguous.
  Searched for: dwh_fact.customerstotalrevenue
  Found: dwh_fact.customersTotalRevenue
```

So it looks like dbt converts model names into names with lowercase characters when creating relations between tables.

To solve it, it is better to call this table `clients_total_revenue`.