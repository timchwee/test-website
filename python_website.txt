import random

word_list = ["aadrvark", "baboon", "camel"]

# Randomly choose a word
chosen_word = random.choice(word_list)
word_length = len(chosen_word)

# Initialize display with underscores
display = ["_" for _ in range(word_length)]

# Counter for wrong guesses
wrong_guesses = 0
max_wrong_guesses = 5

# Game loop
while "_" in display and wrong_guesses <= max_wrong_guesses:
    guess = input("Guess a letter: ").lower()

    # Input validation
    if len(guess) != 1 or not guess.isalpha():
        wrong_guesses += 1
        print(f"Invalid input! Please enter a single letter. You have {max_wrong_guesses - wrong_guesses + 1} chances left.")
        print(" ".join(display))
        continue

    # Check if guess is in the word
    if guess in chosen_word:
        for position in range(word_length):
            if chosen_word[position] == guess:
                display[position] = guess
    else:
        wrong_guesses += 1
        print(f"Wrong guess! You have {max_wrong_guesses - wrong_guesses + 1} chances left.")

    # Show current progress
    print(" ".join(display))

    # Check for game over
    if wrong_guesses > max_wrong_guesses:
        print("Game Over, You Lose!")
        print("The word was:", chosen_word)
        break

# Win condition
if "_" not in display:
    print("Congratulations! You guessed the word:", chosen_word)
