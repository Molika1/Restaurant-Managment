# Restaurant_Managment
This project is a simple Restaurant Management System using NumPy, Pandas, and Matplotlib. It manages order data, calculates total sales, analyzes item-wise performance, and displays sales trends using graphs to help understand restaurant performance easily.

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
menu = {
    "Item": ["Burger", "chicken tikka", "paneer rara", "chicken roll", "chicken biryani"],
    "Price": [120, 250, 180, 80, 100]
    }

menu_df = pd.DataFrame(menu)
print("\n--- MENU ---")
print(menu_df)


orders = {
    "Item": ["Burger", "Pizza", "Burger", "Coffee", "Pasta", "Pizza", "Coffee"],
    "Quantity": [2, 1, 1, 3, 1, 2, 2]
}

orders_df = pd.DataFrame(orders)


bill_df = orders_df.merge(menu_df, on="Item")
bill_df["Total"] = bill_df["Price"] * bill_df["Quantity"]

print("\n--- ORDER DETAILS ---")
print(bill_df)


total_bill = np.sum(bill_df["Total"])
print("\nTotal Bill Amount: ₹", total_bill)


sales_summary = bill_df.groupby("Item")["Quantity"].sum()

print("\n--- SALES SUMMARY ---")
print(sales_summary)


plt.figure()
sales_summary.plot(kind="bar")
plt.title("Most Sold Items in Restaurant")
plt.xlabel("Food Items")
plt.ylabel("Quantity Sold")
plt.tight_layout()
plt.show()
