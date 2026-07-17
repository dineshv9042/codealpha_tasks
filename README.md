# codealpha_tasks
Task2: Stock Portfolio Tracker:
# -------------------------------
# Simple Stock Investment Tracker
# -------------------------------

# Hardcoded stock prices
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "GOOGL": 140,
    "MSFT": 330,
    "AMZN": 135
}

total_investment = 0
stock_details = []

# Get number of stocks
while True:
    try:
        n = int(input("Enter the number of stocks: "))
        if n > 0:
            break
        else:
            print("Please enter a number greater than 0.")
    except ValueError:
        print("Please enter a valid integer.")

# Input stock details
for i in range(n):
    print(f"\nStock {i+1}")

    # Stock name
    while True:
        stock_name = input("Enter stock name: ").upper()
        if stock_name in stock_prices:
            break
        else:
            print("Stock not found! Available stocks:", ", ".join(stock_prices.keys()))

    # Quantity
    while True:
        try:
            quantity = int(input("Enter quantity: "))
            if quantity > 0:
                break
            else:
                print("Quantity must be greater than 0.")
        except ValueError:
            print("Please enter a valid integer.")

    price = stock_prices[stock_name]
    investment = price * quantity
    total_investment += investment

    stock_details.append([stock_name, quantity, price, investment])

# Display summary
print("\n========== Investment Summary ==========")
for stock in stock_details:
    print(f"{stock[0]} | Quantity: {stock[1]} | Price: ${stock[2]} | Investment: ${stock[3]}")

print("----------------------------------------")
print(f"Total Investment Value = ${total_investment}")

# Save report
choice = input("\nDo you want to save the report? (yes/no): ").lower()

if choice == "yes":

    file_type = input("Enter file type (txt/csv): ").lower()

    if file_type == "txt":
        with open("stock_report.txt", "w") as file:
            file.write("Stock Investment Report\n")
            file.write("========================\n\n")

            for stock in stock_details:
                file.write(f"Stock: {stock[0]}\n")
                file.write(f"Quantity: {stock[1]}\n")
                file.write(f"Price: ${stock[2]}\n")
                file.write(f"Investment: ${stock[3]}\n\n")

            file.write(f"Total Investment Value = ${total_investment}")

        print("\nReport saved successfully as 'stock_report.txt'")

    elif file_type == "csv":
        with open("stock_report.csv", "w") as file:
            file.write("Stock,Quantity,Price,Investment\n")

            for stock in stock_details:
                file.write(f"{stock[0]},{stock[1]},{stock[2]},{stock[3]}\n")

            file.write(f"Total,,,{total_investment}")

        print("\nReport saved successfully as 'stock_report.csv'")

    else:
        print("Invalid file type. Report not saved.")

else:
    print("Report not saved.")

print("\nProgram completed successfully!")
