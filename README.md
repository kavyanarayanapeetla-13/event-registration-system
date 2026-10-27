# event-registration-system
to manage events effortlessly

# Event Registration System in Python

events = {
    1: {
        "name": "Python Workshop",
        "date": "2026-11-10",
        "capacity": 3,
        "participants": []
    },
    2: {
        "name": "Web Development Seminar",
        "date": "2026-11-15",
        "capacity": 2,
        "participants": []
    },
    3: {
        "name": "AI and Machine Learning",
        "date": "2026-11-20",
        "capacity": 5,
        "participants": []
    }
}


def display_events():
    print("\n===== AVAILABLE EVENTS =====")

    for event_id, event in events.items():
        available = event["capacity"] - len(event["participants"])

        print(f"\nEvent ID: {event_id}")
        print(f"Name: {event['name']}")
        print(f"Date: {event['date']}")
        print(f"Available Seats: {available}")


def register_event():
    display_events()

    try:
        event_id = int(input("\nEnter Event ID: "))

        if event_id not in events:
            print("Invalid Event ID!")
            return

        name = input("Enter your name: ").strip()
        email = input("Enter your email: ").strip().lower()

        if not name or not email or "@" not in email:
            print("Please enter a valid name and email.")
            return

        event = events[event_id]

        # Check duplicate registration
        for participant in event["participants"]:
            if participant["email"] == email:
                print("You are already registered for this event!")
                return

        # Check seat availability
        if len(event["participants"]) >= event["capacity"]:
            print("Sorry! This event is fully booked.")
            return

        participant = {
            "name": name,
            "email": email
        }

        event["participants"].append(participant)

        print("\nRegistration successful!")
        print(f"Event: {event['name']}")
        print(f"Participant: {name}")

    except ValueError:
        print("Please enter a valid number.")


def view_registrations():
    try:
        event_id = int(input("Enter Event ID: "))

        if event_id not in events:
            print("Invalid Event ID!")
            return

        event = events[event_id]

        print(f"\nRegistrations for {event['name']}")

        if not event["participants"]:
            print("No participants registered yet.")
            return

        for index, participant in enumerate(
            event["participants"], start=1
        ):
            print(f"\nParticipant {index}")
            print(f"Name: {participant['name']}")
            print(f"Email: {participant['email']}")

    except ValueError:
        print("Please enter a valid number.")


def main():
    while True:
        print("\n===== EVENT REGISTRATION SYSTEM =====")
        print("1. View Events")
        print("2. Register for an Event")
        print("3. View Registrations")
        print("4. Exit")

        choice = input("Enter your choice: ").strip()

        if choice == "1":
            display_events()

        elif choice == "2":
            register_event()

        elif choice == "3":
            view_registrations()

        elif choice == "4":
            print("Thank you for using the system!")
            break

        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()
