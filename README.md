# pandas-challenge-1
Challenge: Wholesale Data Analysis
This project analyzes a dataset containing order information for clients, focusing on transforming and summarizing the data for actionable insights.
Steps to Complete the Challenge
Part 1: Explore the Data
Import the dataset and inspect column names and statistics.
Identify:
The top 3 item categories by the number of entries.
The subcategory with the most entries in the top category.
The 5 clients with the most entries and their total quantities.
Store the top client IDs in a list.
Part 2: Transform the Data
Create new columns:
Subtotal: unit_price * qty
Shipping Price: Based on unit weight ($7/lb for weights over 50 lbs, $10/lb otherwise).
Total Price: Includes subtotal, shipping price, and a sales tax of 9.25%.
Line Cost: Uses unit_cost, qty, and shipping_price.
Profit: Difference between line_price and line_cost.
Part 3: Confirm Your Work
Verify the total prices for the following orders against provided receipts:
Order ID 2742071: $152,811.89
Order ID 2173913: $162,388.71
Order ID 6128929: $923,441.25
Part 4: Summarize and Analyze
Calculate the total spending of the top 5 clients.
Create a summary DataFrame with:
Total units purchased, total shipping price, total revenue, and total profit.
Format the summary in millions of dollars, sort by total profit, and rename columns for presentation.
Write a 2–3 sentence summary of findings.
Technologies
Python
Pandas
Usage
Run the provided Python script in Jupyter Notebook or any Python IDE with Pandas installed. Ensure the dataset is in the correct directory.
