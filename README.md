import random

def get_word():
    # You can expand this list as you like
    words = ["python", "hangman", "developer", "challenge", "keyboard", "programming"]
    return random.choice(words)

def display_hangman(tries):
    stages = [
        """
           --------
           |      |
           |      O
           |     \\|/
           |      |
           |     / \\
           -
        """,
        """
           --------
           |      |
           |      O
           |     \\|/
           |      |
           |     / 
           -
        """,
        """
           --------
           |      |
           |      O
           |     \\|/
           |      |
           |      
           -
        """,
        """
           --------
           |      |
           |      O
           |     \\|
           |      |
           |     
           -
        """,
        """
           --------
           |      |
           |      O
           |      |
           |      |
           |     
           -
        """,
        """
           --------
           |      |
           |      O
           |    
           |      
           |     
           -
        """,
        """
           --------
           |      |
           |      
           |    
           |      
           |     
           -
        """
    ]
    return stages[tries]

def play():
    word = get_word()
    word_letters = set(word)
    guessed_letters = set()
    tries = 6
    print("🎮 Welcome to Hangman!")
    
    while tries > 0 and word_letters:
        print(display_hangman(tries))
        print("Word: ", ' '.join([letter if letter in guessed_letters else '_' for letter in word]))
        print(f"Guessed letters: {', '.join(guessed_letters)}")

        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("❗ Please enter a single alphabetic character.")
            continue

        if guess in guessed_letters:
            print("⚠️ You already guessed that letter.")
            continue

        guessed_letters.add(guess)

        if guess in word_letters:
            word_letters.remove(guess)
            print("✅ Good guess!")
        else:
            tries -= 1
            print("❌ Wrong guess!")

    if not word_letters:
        print(f"\n🎉 Congratulations! You guessed the word: **{word}**")
    else:
        print(display_hangman(tries))
        print(f"\n💀 Game Over! The word was: **{word}**")

# Run the game
if __name__ == "__main__":
    play()
