
# Importing necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
import os

# Step 1: Verify and Load Data
data_path =  r"C:\Users\vibhu\OneDrive\Documents\review\review\Reviews\data\daily-new-confirmed-covid-19-cases-per-million-people.csv"


# Check if file exists
if not os.path.exists(data_path):
    print(f"Error: File '{data_path}' not found! Place the file in the script directory.")
else:
    df = pd.read_csv(data_path, encoding="utf-8")  # Adjust encoding if needed
    print("Dataset loaded successfully!")

    # Step 2: Bar Chart (Matplotlib)
    plt.figure(figsize=(8, 5))
    df.groupby("Category")["Value"].sum().plot(kind="bar", color='skyblue')
    plt.xlabel("Category")
    plt.ylabel("Total Value")
    plt.title("Category-wise Distribution")
    plt.savefig("bar_chart.png")  # Save for GitHub
    plt.show()

    # Step 3: Pie Chart (Matplotlib)
    plt.figure(figsize=(6, 6))
    df["Category"].value_counts().plot(kind="pie", autopct="%1.1f%%", colors=["#ff9999", "#66b3ff", "#99ff99", "#ffcc99"])
    plt.title("Category Distribution")
    plt.savefig("pie_chart.png")
    plt.show()

    # Step 4: Scatter Plot (Seaborn)
    plt.figure(figsize=(8, 5))
    sns.scatterplot(x=df["X_Value"], y=df["Y_Value"], hue=df["Category"], palette="coolwarm")
    plt.title("Scatter Plot of X vs Y")
    plt.savefig("scatter_plot.png")
    plt.show()

    # Step 5: Interactive Scatter Plot (Plotly)
    fig = px.scatter(df, x="X_Value", y="Y_Value", color="Category", hover_data=["Details"])
    fig.update_layout(title="Interactive Scatter Plot")
    fig.write_html("interactive_scatter.html")  # Save interactive plot for GitHub
    fig.show()

    # Step 6: README File Template
    readme_content = """
# Data Visualization Project

## Overview
This project presents multiple types of data visualizations using Python, ensuring clarity, aesthetics, interactivity, and meaningful insights.

## Visualizations
- **Bar Chart:** Shows category-wise distribution.
- **Pie Chart:** Displays percentage breakdown of categories.
- **Scatter Plot:** Highlights relationships between X and Y values.
- **Interactive Plot:** Provides hover tooltips for detailed exploration.

## How to Run
1. Install dependencies: `pip install pandas matplotlib seaborn plotly`
2. Run `python visualize.py`
3. Open `interactive_scatter.html` for interactive visualization.

## Dataset
Ensure `daily-new-confirmed-covid-19-cases-per-million-people.csv` is in the same directory before running the script.

"""
    with open("README.md", "w") as f:
        f.write(readme_content)

    print("Project files saved successfully! Ready for GitHub upload.")



