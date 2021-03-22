# HANGMAN-GAME


import random 
import time 

#initial steps

print("\n-----Welcome to hangman game-----")
name = input("ENTER YOUR NAME : ")
print("\nHello " + name + " ! \n Best of luck !!")
time.sleep(1)
print("\nThe game is about to start ! \n Let's play Hangman !")
time.sleep(2)

def main():
    #global variables 
    global count
    global display
    global word 
    global already_guessed
    global length 
    global play_game
    global original_word
    
    words_to_guess = ["january","border","image","film","promise","kids","lungs","doll","damage","plants"]
    word = random.choice(words_to_guess)
    original_word = word
    length = len(word)
    count = 0
    display = "_" * length
    already_guessed = []
    play_game = " "
    

#LOOP TO EXECUTE THE GAME WHEN THE FIRST ROUND ENDS 

def play_loop() :
    global play_game 
    play_game = input("Do you want to play again?\n YES \n NO :\n ").lower()
    while play_game not in ["yes","no"] :
        play_game = input("Do you want to play again?\n YES \n NO :\n ").lower()
    if play_game == "yes" :
        main()
    elif play_game == "no" :
        print("THANKS FOR PLAYING !!")
        
    
        
        
#INITTIALIZING ALL THE CONDITIONS REQUIRED FOR THE GAME 

def hangman() :
    global count
    global display
    global word
    global already_guessed
    global play_game
    global original_word
    
    limit = 5
    print("THIS IS THE HANGMAN WORD : " + display)
    guess = input("Enter your guess : ").rstrip().lower()
    ## confusing code below
    if len(guess) == 0 or len(guess) >= 2 or guess <= "9" :
        print("INVALID INPUT ")
        hangman()
    
    elif guess in word :
        already_guessed.extend([guess])
        index = word.find(guess)
        word = word[:index] + "_" + word[index+1 :]
        display = display[:index] + guess + display[index+1 :]
        print(display + "\n")
        
    elif guess in already_guessed :
        print("Try another letter . \n")
        
    else :
        count += 1
        if count == 1:
            time.sleep(1)
            print("   _______\n"
                  "  |       \n"
                  "  |       \n"
                  "  |       \n"
                  "  |       \n"
                  "  |       \n"
                  "  |       \n"
                  "__|__     \n")
            
            print("Wrong answer.\n" + str(limit-count) + " guesses remaining\n")
            
        elif count == 2 :
            time.sleep(1)
            print("   _______\n"
                  "  |      |\n"
                  "  |      |\n"
                  "  |       \n"
                  "  |       \n"
                  "  |       \n"
                  "  |       \n"
                  "__|__     \n")
            print("Wrong guess.\n" + str(limit-count) + " guesses remaining\n")
            
        elif count == 3 :
            time.sleep(1)
            print("   _______\n"
                  "  |      |\n"
                  "  |      |\n"
                  "  |      |\n"
                  "  |       \n"
                  "  |       \n"
                  "  |       \n"
                  "__|__     \n")
            print("Wrong guess.\n" + str(limit-count) + " guesses remaining\n")
            
        elif count == 4 :
            time.sleep(1)
            print("   _______\n"
                  "  |      |\n"
                  "  |      |\n"
                  "  |      |\n"
                  "  |      O\n"
                  "  |       \n"
                  "  |       \n"
                  "__|__     \n")
            print("Wrong guess.\n" + str(limit-count) + " guesses remaining\n")
            
        elif count == 5 :
            time.sleep(1)
            print("   _______  \n"
                  "  |      |  \n"
                  "  |      |  \n"
                  "  |      |  \n"
                  "  |      O   \n"
                  "  |     /|\   \n"
                  "  |     / \    \n"
                  "__|__       \n")
            print("Wrong guess.\n YOU ARE HANGED !! \n" )
            print("The word was : " ,original_word)
            play_loop()
            
    #loop ends
    
    if word == '_' * length :
        print("CONGRATULATIONS ! YOU HAVE GUESSED THE WORD CORRECTLY !")
        play_loop()
        
    elif count != limit :
        hangman()

        
main()
hangman()
    
   
    
