import random
import string

def get_user_input():
    """Prompt the user for customization options."""
    print("Welcome to the Username Generator!")

    include_numbers = input("Do you want to include numbers? (yes/no): ").lower() == 'yes'
    include_special = input("Do you want to include special characters? (yes/no): ").lower() == 'yes'
    length = int(input("What length do you want the username to be? (min 10 characters): "))
    
    return include_numbers, include_special, length

def generate_username(include_numbers, include_special, length):
    """Generate a random username based on user preferences."""
    adjectives = ["Cool", "Happy", "Silent", "Brave", "Quick", "Fierce"]
    nouns = ["Tiger", "Dragon", "Wolf", "Phoenix", "Lion", "Eagle"]
    
    # Randomly choose an adjective and a noun
    adjective = random.choice(adjectives)
    noun = random.choice(nouns)
    
    # Optionally add numbers and/or special characters
    if include_numbers:
        adjective += str(random.randint(1, 99))
        noun += str(random.randint(1, 99))
    
    if include_special:
        special_char = random.choice(string.punctuation)
        adjective += special_char
        noun += special_char
    
    # Combine the adjective and noun and ensure the total length matches the user input
    username = adjective + noun
    
    if len(username) < length:
        username += ''.join(random.choices(string.ascii_letters + string.digits + string.punctuation, k=length - len(username)))
    
    return username[:length]  # Ensure the username doesn't exceed the specified length

def save_usernames(usernames):
    """Save the generated usernames to a file."""
    with open("usernames.txt", "w") as file:
        for username in usernames:
            file.write(username + "\n")
    print("Usernames saved to 'usernames.txt'.")

def main():
    # Get user input for customization options
    include_numbers, include_special, length = get_user_input()
    
    # Generate a list of usernames based on the user preferences
    usernames = [generate_username(include_numbers, include_special, length) for _ in range(10)]
    
    # Display the generated usernames
    print("\nGenerated Usernames:")
    for username in usernames:
        print(username)
    
    # Save usernames to a file
    save_usernames(usernames)

if __name__ == "__main__":
    main()
