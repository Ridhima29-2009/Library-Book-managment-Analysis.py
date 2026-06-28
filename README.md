# Library-Book-managment-Analysis.py
This is a beginner Python data analysis project created using Pandas and Matplotlib.The project analyzes library book data such as book prices, number of copies, total value, category-wise value, and percentage contribution.
import pandas as pd
import matplotlib.pyplot as plt

data = {
    "Book": [
        "Python Basics",
        "Data Science",
        "Maths Guide",
        "English Grammar",
        "Physics Notes",
        "Computer Networks"
    ],
    "Category": [
        "Programming",
        "Programming",
        "Education",
        "Education",
        "Science",
        "Programming"
    ],
    "Price": [
        450,
        650,
        350,
        300,
        550,
        700
    ],
    "Copies": [
        20,
        15,
        25,
        18,
        12,
        10
    ]
}

df = pd.DataFrame(data)

print("Library Book Management Analysis")
print(df)

print("\nHead")
print(df.head())

# Total Value
df["Total Value"] = df["Price"] * df["Copies"]

# Most Expensive Book
Most_Expensive = df.loc[df["Price"].idxmax()]
print("\nMost Expensive Book")
print(Most_Expensive)

# Highest Total Value
Highest_Total_Value = df["Total Value"].max()
print("\nHighest Total Value:", Highest_Total_Value)

# Book with Highest Total Value
Highest_Total_Book = df.loc[df["Total Value"].idxmax()]
print("\nHighest Total Value Book")
print(Highest_Total_Book)

# Category Wise Total Value
Category = df.groupby("Category")["Total Value"].sum()
print("\nCategory Wise Total Value")
print(Category)

# Percentage Contribution
df["Percentage Contribution"] = (
    df["Total Value"] / df["Total Value"].sum()
) * 100

print("\nPercentage Contribution")
print(df[["Book", "Percentage Contribution"]])

# Sort Data
df = df.sort_values("Total Value", ascending=False)

print("\nSorted Data")
print(df)

# Graph 1
plt.bar(df["Book"], df["Total Value"])
plt.title("Library Book Data Analysis")
plt.xlabel("Book")
plt.ylabel("Total Value")
plt.xticks(rotation=20)
plt.show()

# Graph 2
plt.bar(Category.index, Category.values)
plt.title("Category Wise Book Value")
plt.xlabel("Category")
plt.ylabel("Total Value")
plt.show()