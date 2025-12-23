import mysql.connector

# -------- DATABASE CONNECTION --------
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="yashu3047a",
    database="Project_Gladiator"
)

cursor = conn.cursor()

# -------- FUNCTIONS --------

def view_bus_details():
    print("\n--- BUS DETAILS ---")
    cursor.execute("SELECT * FROM bus_details")
    data = cursor.fetchall()
    for row in data:
        print(row)

def view_passenger_details():
    print("\n--- PASSENGER DETAILS ---")
    cursor.execute("SELECT * FROM passenger_count")
    data = cursor.fetchall()
    for row in data:
        print(row)

def check_overcrowded_buses():
    print("\n--- OVERCROWDED BUSES ---")
    cursor.execute("""
    SELECT b.bus_id, b.capacity, p.passengers
    FROM bus_details b, passenger_count p
    WHERE b.bus_id = p.bus_id AND p.passengers > b.capacity
    """)
    data = cursor.fetchall()
    if data:
        for row in data:
            print("Bus ID:", row[0], "| Capacity:", row[1], "| Passengers:", row[2])
    else:
        print("No overcrowded buses found")

def view_bus_schedule():
    print("\n--- BUS SCHEDULE ---")
    cursor.execute("SELECT * FROM schedule")
    data = cursor.fetchall()
    for row in data:
        print(row)

# -------- MAIN MENU --------

while True:
    print("\n===== PUBLIC BUS MANAGEMENT SYSTEM =====")
    print("1. View Bus Details")
    print("2. View Passenger Details")
    print("3. Check Overcrowded Buses")
    print("4. View Bus Schedule")
    print("5. Exit")

    choice = int(input("Enter choice: "))

    if choice == 1:
        view_bus_details()

    elif choice == 2:
        view_passenger_details()

    elif choice == 3:
        check_overcrowded_buses()

    elif choice == 4:
        view_bus_schedule()

    elif choice == 5:
        print("Exiting program...")
        conn.close()
        break

    else:
        print("Invalid choice. Try again.")
