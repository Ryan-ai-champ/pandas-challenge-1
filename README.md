# pandas-challenge-1
import pandas as pd

# Load the dataset
data = pd.read_csv('client_dataset.csv')

# Part 1: Explore the Data
# Column names and basic stats
print(data.columns)
print(data.describe())

# Top 3 categories and their subcategories
top_categories = data['category'].value_counts().head(3)
print(top_categories)

top_subcategory = (
    data[data['category'] == top_categories.index[0]]['subcategory'].value_counts().idxmax()
)
print(top_subcategory)

# Top 5 clients and their total quantities
top_clients = data['client_id'].value_counts().head(5)
top_client_ids = top_clients.index.tolist()
top_client_total_qty = data[data['client_id'] == top_client_ids[0]]['qty'].sum()

print(top_clients)
print(top_client_total_qty)

# Part 2: Transform the Data
# Add subtotal column
data['subtotal'] = data['unit_price'] * data['qty']

# Add shipping price column
data['shipping_price'] = data['unit_weight'].apply(
    lambda weight: 7 * weight if weight > 50 else 10 * weight
)

# Add total price column
data['total_price'] = (data['subtotal'] + data['shipping_price']) * 1.0925

# Add line cost column
data['line_cost'] = (data['unit_cost'] * data['qty']) + data['shipping_price']

# Add profit column
data['profit'] = data['total_price'] - data['line_cost']

# Part 3: Confirm Your Work
# Check order totals for specified IDs
order_ids_to_check = [2742071, 2173913, 6128929]
order_totals = data[data['order_id'].isin(order_ids_to_check)].groupby('order_id')['total_price'].sum()
print(order_totals)

# Part 4: Summarize and Analyze
# Total spending of top 5 clients
client_spending = (
    data[data['client_id'].isin(top_client_ids)]
    .groupby('client_id')
    .agg(total_units=('qty', 'sum'),
         total_shipping=('shipping_price', 'sum'),
         total_revenue=('total_price', 'sum'),
         total_profit=('profit', 'sum'))
)

# Convert to millions of dollars and sort by profit
client_spending['total_revenue'] /= 1_000_000
client_spending['total_profit'] /= 1_000_000
client_spending.sort_values(by='total_profit', ascending=False, inplace=True)

print(client_spending)
