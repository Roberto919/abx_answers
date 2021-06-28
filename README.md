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
**The procedure behind every answer can be found in the notebook `notebooks/abxrp_nb.ipynb`**
1. Algorithm used
    - Random forest
2. Time-series of determined product-client-agency combination
    ![Screen Shot 2021-06-27 at 17 03 41](https://user-images.githubusercontent.com/48889991/123560725-a255c500-d769-11eb-947e-2b7cf401f98b.png)
3. Metrics to support algorithm
    - The model was selected due to its versatility and effectiveness
    - I normally support the selection of an algorithm using a particular scoring parameter (e.g. accuracy) and comparing its value across different models (e.g. linear regression, decision tree, logistic regression) by using a magic loop.
    - Due to the time constraints, I did not set up such magic-loop, therefore, no comparison is available.  
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
5. Week 9 prediction of top 3 sold products in client sample
    - The top 3 products were selected based on the demand value (in pesos):
        - Top 1 product: {"Name": "Pan Integral 680g TNB BIM 34786", "Producto_ID": 34786, "Demand value (in selected agency and client sample)": 2.55 million pesos, "Participation (in selected agency and client sample)": 5.6%}
        - Top 2 product: {"Name": "Wonder 100pct con Ajonjoli 567g MTA WON 35145", "Producto_ID": 35145, "Demand value (in selected agency and client sample)": 1.90 million pesos, "Participation (in selected agency and client sample)": 4.2%}
        - Top 3 product: {"Name": "Tortillinas 22p 570g MTA TR 48996", "Producto_ID": 48996, "Demand value (in selected agency and client sample)": 1.90 million pesos, "Participation (in selected agency and client sample)": 4.1%}
    - The predictions can be found in the `results` directory
6. Flowchart of algorithm steps
    1. Cleaning and enhancing initial data
    2. Identify the most important agency in terms of sales
    3. Identify sample of clients that represent 80% of the sales for the selected agency
    4. Find the top 3 most sold products in the selected agency and client sample
    5. Eliminate irrelevant features in the training data and filter to focus only on identified top products
    6. Prepare training data based on each features characteristics (e.g. categorical -> OHE; numerical -> standard scaler)
    7. Select a model for the regression prediction and a set of parameters for the grid search
    8. Train model with every combination of parameters and using cross validation
    9. Select model with the best accuracy score
    10. Use selected model to make prediction over the test data

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