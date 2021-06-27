# Roberto Pérez Technical Interview Answers

## Objective
Forecast demand of a product for a given week, at a particular store.

## Project details
- Weekly delivery trucks
- Transaction:
    - Sales: Delivered product 
    - Returns: Unsold and expired products
- Demand: sales (current week) - returns (next week)

## Answers
1. Algorithm used
2. Time-series of determined product-client-agency combination
    ![Screen Shot 2021-06-27 at 17 03 41](https://user-images.githubusercontent.com/48889991/123560725-a255c500-d769-11eb-947e-2b7cf401f98b.png)
4. Metrics to support algorithm
5. Sample of clients that represent agency
6. Week 9 prediction of top 3 selled productsin client sample
7. Flowchart of algorithm steps

## Files used
- cliente_tabla.csv (ID feature: Cliente_ID)
- producto_tabla.csv (ID feature: Producto_ID)
- town_state.csv (ID feature: Agencia_ID)

## EDA Observations
- cliente_tabla.csv
    - There are 4,862 Client_ID entries that appear 2 times
    - Decided to drop the 4,862 duplicated entries assuming there is no loss of relevant information 
