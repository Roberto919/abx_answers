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
3. Metrics to support algorithm
4. Sample of clients that represent agency
    - The agency for the analysis was selected based on the total currency demand value
        - The selected agency is = {
                                        "Agencia_ID": 1129,
                                        "Town": 2011 AG. SAN ANTONIO,
                                        "State": MÉXICO, D.F.,
                                        "Demand value": $56.7 million pesos,
                                        "Participation among all agencies": 8.83%,
                                   }
    - A sample of clients related to the selected agency ("Agencia_ID": 1129) was selected based on the demand value (in pesos)
        - The sample consists of the top 55 agency clients (out of a total of 105 clients)
        - These represent the 80% of the agency's demand
5. Week 9 prediction of top 3 selled products in client sample
6. Flowchart of algorithm steps
    1. Find top 3 products 

## Files used
- cliente_tabla.csv (ID feature: Cliente_ID)
- producto_tabla.csv (ID feature: Producto_ID)
- town_state.csv (ID feature: Agencia_ID)
- df_[candidate]_small.csv (train data)
- df_[test]_small.csv (test data)

## EDA Observations
- `cliente_tabla.csv`
    - There are 4,862 Client_ID entries that appear 2 times
    - Decided to drop the 4,862 duplicated entries assuming there is no loss of relevant information

## Data features
- Semana — Week number (From Thursday to Wednesday)
- Agencia_ID — Sales Depot ID
- Canal_ID — Sales Channel ID
- Ruta_SAK — Route ID (Several routes = Sales Depot)
- Cliente_ID — Client ID
- NombreCliente — Client name
- Producto_ID — Product ID
- NombreProducto — Product Name
- Venta_uni_hoy — Sales unit this week (integer)
- Venta_hoy — Sales this week (unit: pesos)
- Dev_uni_proxima — Returns unit next week (integer)
- Dev_proxima — Returns next week (unit: pesos)
- Demanda_uni_equil — Adjusted Demand (integer) (This is the target you will predict)