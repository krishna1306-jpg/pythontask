import random

def show_menu():
    print("\n=== Number Guessing Game ===")
    print("1. Play Game")
    print("2. View High Score")
    print("3. Exit")
    print("===========================")

def get_player_guess():
    while True:
        user_input = input("Enter your guess (1-100), or 'exit' to quit: ").strip()
        if user_input.lower() == 'exit':
            return 'exit'
        try:
            guess = int(user_input)
            if 1 <= guess <= 100:
                return guess
            else:
                print("Please enter a number between 1 and 100.")
        except ValueError:
            print("Invalid input. Enter an integer between 1 and 100 or 'exit'.")

def play_game():
    target = random.randint(1, 100)
    attempts = 0
    while True:
        guess = get_player_guess()
        if guess == 'exit':
            print("Exiting the game. The number was {}.".format(target))
            return None
        attempts += 1
        if guess < target:
            print("Too Low!")
        elif guess > target:
            print("Too High!")
        else:
            print(f"Congratulations! You guessed the number {target} in {attempts} tries.")
            return attempts

def main():
    high_score = None
    while True:
        show_menu()
        choice = input("Choose an option (1/2/3): ").strip()
        if choice == '1':
            print("\nI'm thinking of a number between 1 and 100.")
            score = play_game()
            if score:
                if (high_score is None) or (score < high_score):
                    high_score = score
                    print(f"New high score: {high_score} attempt(s)!")
        elif choice == '2':
            if high_score is None:
                print("No high score yet. Play a game first!")
            else:
                print(f"Current high score: {high_score} attempt(s).")
        elif choice == '3':
            print("Thanks for playing! Goodbye!")
            break
        else:
            print("Invalid choice. Please pick 1, 2, or 3.")

if __name__ == "__main__":
    main()

