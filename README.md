import json
from datetime import datetime
import os

DATA_FILE = "zwayam_clients.json"

def load_clients():
    if os.path.exists(DATA_FILE):
        with open(DATA_FILE, "r") as file:
            return json.load(file)
    return []

def save_clients(clients):
    with open(DATA_FILE, "w") as file:
        json.dump(clients, file, indent=4)

def create_new_client():
    print("\n--- New Client Entry ---")
    client = {
        "client_name": input("Client Name: "),
        "company": input("Company Name: "),
        "email": input("Client Email: "),
        "phone": input("Contact Number: "),
        "project_title": input("Project Title: "),
        "project_description": input("Project Description: "),
        "offered_by": "Zwayam Team",
        "status": "Offered",
        "date": datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    }
    return client

def display_clients(clients):
    print("\n--- All Clients ---")
    for idx, client in enumerate(clients, 1):
        print(f"{idx}. {client['client_name']} | {client['company']} | {client['project_title']} | Status: {client['status']}")

def main():
    clients = load_clients()

    while True:
        print("\nZWAYAM CLIENT ENGAGEMENT SYSTEM")
        print("1. Add New Client")
        print("2. View All Clients")
        print("3. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            client = create_new_client()
            clients.append(client)
            save_clients(clients)
            print("✅ Client and project info saved successfully!")
        elif choice == "2":
            display_clients(clients)
        elif choice == "3":
            print("Exiting... 💼")
            break
        else:
            print("Invalid choice. Try again!")

if __name__ == "__main__":
    main()
