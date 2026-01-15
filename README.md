# ==========================================
# RESTAURANT MANAGEMENT SYSTEM
# ==========================================

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# ------------------------------
# 1. Restaurant Menu
# ------------------------------
menu = {
    "Item": ["Burger", "Pizza", "Pasta", "Sandwich", "Cold Drink"],
    "Price": [120, 200, 180, 100, 50]
}

menu_df = pd.DataFrame(menu)
print("\n------ MENU ------")
print(menu_df)

# ------------------------------
# 2. Customer Orders
# ------------------------------
orders = {
    "Item": ["Burger", "Pizza", "Cold Drink", "Burger", "Sandwich", "Pizza"],
    "Quantity": [2, 1, 3, 1, 2, 1]
}

orders_df = pd.DataFrame(orders)

# ------------------------------
# 3. Billing System
# ------------------------------
bill_df = pd.merge(orders_df, menu_df, on="Item")
bill_df["Total"] = bill_df["Price"] * bill_df["Quantity"]

print("\n------ BILL DETAILS ------")
print(bill_df)

# ------------------------------
# 4. Total Bill Amount
# ------------------------------
total_amount = np.sum(bill_df["Total"])
gst = total_amount * 0.05
grand_total = total_amount + gst

print("\nSubtotal: ₹", total_amount)
print("GST (5%): ₹", gst)
print("Grand Total: ₹", grand_total)

# ------------------------------
# 5. Sales Summary
# ------------------------------
sales_summary = bill_df.groupby("Item")["Quantity"].sum()

print("\n------ SALES SUMMARY ------")
print(sales_summary)

# ------------------------------
# 6. Sales Visualization
# ------------------------------
plt.figure()
sales_summary.plot(kind="bar")
plt.title("Restaurant Sales Report")
plt.xlabel("Food Items")
plt.ylabel("Quantity Sold")
plt.tight_layout()
plt.show()
