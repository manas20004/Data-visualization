# Data-visualization
"""
Task 3: Data Visualization
----------------------------


Requirements (terminal mein chalao):
    pip install pandas matplotlib seaborn
"""

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns


# ---------- STEP 1: Data load karo ----------
df = pd.read_csv("../scraped_data.csv")

# Price column se '£' hata ke number (float) mein convert karo
df["price"] = df["price"].replace(r"[£Â]", "", regex=True).astype(float)

print("Data preview:")
print(df.head())
print(f"\nTotal rows: {len(df)}")


# ---------- STEP 2: Style set karo (achha dikhne ke liye) ----------
sns.set_theme(style="whitegrid")


# ---------- CHART 1: Price Distribution (Histogram) ----------
plt.figure(figsize=(8, 5))
sns.histplot(df["price"], bins=10, kde=True, color="steelblue")
plt.title("Book Prices Distribution")
plt.xlabel("Price (£)")
plt.ylabel("Number of Books")
plt.tight_layout()
plt.savefig("chart_price_distribution.png")
plt.close()
print("✅ Saved: chart_price_distribution.png")


# ---------- CHART 2: Top 10 Most Expensive Books (Bar Chart) ----------
top10 = df.sort_values("price", ascending=False).head(10)

plt.figure(figsize=(10, 6))
sns.barplot(data=top10, x="price", y="title", hue="title", legend=False, palette="viridis")
plt.title("Top 10 Most Expensive Books")
plt.xlabel("Price (£)")
plt.ylabel("Book Title")
plt.tight_layout()
plt.savefig("chart_top10_expensive.png")
plt.close()
print("✅ Saved: chart_top10_expensive.png")


# ---------- CHART 3: Stock Availability (Pie Chart) ----------
stock_counts = df["stock"].value_counts()

plt.figure(figsize=(6, 6))
plt.pie(
    stock_counts.values,
    labels=stock_counts.index,
    autopct="%1.1f%%",
    colors=sns.color_palette("pastel"),
    startangle=90,
)
plt.title("Stock Availability of Books")
plt.tight_layout()
plt.savefig("chart_stock_availability.png")
plt.close()
print("✅ Saved: chart_stock_availability.png")


# ---------- CHART 4: Price Range Summary (Boxplot) ----------
plt.figure(figsize=(6, 5))
sns.boxplot(y=df["price"], color="lightcoral")
plt.title("Price Range Summary (Boxplot)")
plt.ylabel("Price (£)")
plt.tight_layout()
plt.savefig("chart_price_boxplot.png")
plt.close()
print("✅ Saved: chart_price_boxplot.png")


print("\n🎉 Sabhi charts ban gaye! Apne folder mein 4 PNG files dekh lo:")
print(" - chart_price_distribution.png")
print(" - chart_top10_expensive.png")
print(" - chart_stock_availability.png")
print(" - chart_price_boxplot.png")
