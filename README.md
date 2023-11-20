# hello-world-class PropertyOwner:
    def __init__(self, name, location, price, phone_number):
        self.name = name
        self.location = location
        self.price = price
        self.phone_number = phone_number

    def to_string(self):
        return f"Mwenye nyumba: {self.name}, Mahali: {self.location}, Bei: {self.price}, Mawasiliano: {self.phone_number}"

class RoomSeeker:
    def __init__(self, name, location, max_price):
        self.name = name
        self.location = location
        self.max_price = max_price

    def to_string(self):
        return f"Mpangaji: {self.name}, Mahali unapotaka: {self.location}, Bei unayoweza kulipa: {self.max_price}"

# Property owner listings
def list_property(owner_name, location, price, phone_number):
    with open('database.txt', 'a') as file:
        file.write(f"{PropertyOwner.__name__}, {owner_name}, {location}, {price}, {phone_number}\n")

# Room seekers
def list_room_seeker(name, location, max_price):
    with open('database.txt', 'a') as file:
        file.write(f"{RoomSeeker.__name__}, {name}, {location}, {max_price}\n")

# User interactions
def view_properties():
    with open('database.txt', 'r') as file:
        listings = file.readlines()
        for index, listing in enumerate(listings, start=1):
            listing_data = listing.strip().split(', ')
            user_type = listing_data[0]
            if user_type == "PropertyOwner":
                owner_name = listing_data[1]
                location = listing_data[2]
                price = listing_data[3]
                phone_number = listing_data[4] if len(listing_data) > 4 else "N/A"
                print(f"{index}. Mwenye nyumba: {owner_name}, Mahali: {location}, Bei: {price}, Mawasiliano: {phone_number}")
            elif user_type == "RoomSeeker":
                seeker_name = listing_data[1]
                location = listing_data[2]
                max_price = listing_data[3]
                print(f"{index}. Mpangaji: {seeker_name}, Mahali unapotaka: {location}, Bei ya Juu: {max_price}")

def main():
    while True:
        print("Kobesmart Portal")
        print("1. Weka Mali (Mwenye nyumba)")
        print("2. Tafuta Chumba (Mpangaji)")
        print("3. Tazama Mali na Watafuta Chumba")
        print("4. Weka Namba za Mmiliki au Mpangaji")
        print("5. Toka")

        choice = input("Ingiza chaguo lako: ")

        if choice == '1':
            # Weka mali kwenye orodha (Mwenye nyumba)
            print("Weka Mali (Mwenye nyumba)")
            owner_name = input("Jina la Mmiliki: ")
            location = input("Mahali: ")
            price = input("Bei: ")
            phone_number = input("Mawasiliano: ")
            list_property(owner_name, location, price, phone_number)
        elif choice == '2':
            # Tafuta chumba (Mpangaji)
            print("Tafuta Chumba (Mpangaji)")
            seeker_name = input("Jina la Mpangaji: ")
            location = input("Mahali unapotaka: ")
            max_price = input("Bei unayoweza kulipa: ")
            list_room_seeker(seeker_name, location, max_price)
        elif choice == '3':
            # Tazama Mali na Watafuta Chumba
            print("Tazama Mali na Watafuta Chumba")
            print("Orodha ya Mali na Watafuta Chumba:")
            view_properties()
            input("Bonyeza Enter kuendelea...")
        elif choice == '4':
            # Onyesha maelezo ya Mmiliki au Mpangaji
            try:
                selected_user = int(input("Ingiza namba ya Mmiliki au Mpangaji: ")) - 1
                with open('database.txt', 'r') as file:
                    listings = file.readlines()
                    if 0 <= selected_user < len(listings):
                        listing_data = listings[selected_user].strip().split(', ')
                        user_type = listing_data[0]
                        if user_type == "PropertyOwner":
                            owner_name = listing_data[1]
                            phone_number = listing_data[4] if len(listing_data) > 4 else "N/A"
                            print(f"Mwenye nyumba: {owner_name}, Mawasiliano: {phone_number}")
                        elif user_type == "RoomSeeker":
                            seeker_name = listing_data[1]
                            print(f"Mpangaji: {seeker_name}")
                    else:
                        print("Namba ya Mmiliki au Mpangaji haipo.")
                input("Bonyeza Enter kuendelea...")
            except ValueError:
                print("Ingiza namba halali ya Mmiliki au Mpangaji.")
        elif choice == '5':
            break

if __name__ == "__main__":
    main()
