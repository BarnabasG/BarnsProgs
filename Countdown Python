import random

pointsTot = 0


def dictionary_reader(filename: str, words: dict) -> dict:
    '''
    This function puts all the words from the text file of words in to a
    created dictionary called 'words'

    Arguments:
    filename - the name of the file to be read into the program
    words - a dictionary of all words that can possibly be made in this game
    '''
    f = open(filename, "r")
    for word in f.readlines():
        # \n signals a new line in the text file and must be removed
        word = word.replace("\n", "").lower()
        if not len(word) > 9:
            words[word] = '1'
    f.close()
    return words


def select_characters(conson: list, vowels: list, letters: list) -> list:
    '''
    This function allows the user to choose how many vowels and consonants
    they want out of 9 letters. The user entry is error trapped.

    Arguments:
    conson - a list of all consonants with weighted letter probability
    vowels - a list of all vowels with weighted letter probability
    letters - a list of the user's nine available letters
    '''
    for i in range(1, 10):
        while True:
            print('Enter "c" for consonant or "v" for vowel')
            charChoice = input('> ')
            if charChoice.lower() == "c":
                # Chooses a random item from the list of consonants
                newChar = random.choice(conson)
                break
            elif charChoice.lower() == "v":
                newChar = random.choice(vowels)
                break
        print(newChar)
        letters.append(newChar)
        print("===================================")
        print("CURRENT LETTERS : " + " ".join(letters))
        print("===================================")
    return letters


def word_lookup(words: dict, matches: list, letters: list, display: list) -> list:
    '''
    Finds the valid words from the dictionary

    This function compares the letters chosen by the user and the words in
    the dictionary and creates a list of all the words which can be made from
    those letters

    Arguments:
    words - a dictionary of all words that can possibly be made in this game
    matches - a list of all the words from the dictionary which can be made
    letters - a list of the user's nine available letters
    display - a list of only the valid words with the longest word length
    '''
    letInUse = []
    for word in words:
        wordlist = list(word)
        i = 0
        letInUse = letters.copy()
        while not i >= len(wordlist):
            char = wordlist[0]
            if char in letInUse:
                letInUse.remove(char)
                wordlist.remove(char)
                if len(wordlist) == 0:
                    matches.append(word)
            else:
                i += 1
    # This line sorts the list of possible words from longest to shortest
    matches.sort(key=len, reverse=True)
    # This loop is used to only display all words of the longest length
    for each in matches:
        if len(each) == len(matches[0]):
            display.append(each)
    return display


def user_input(matches: list, letters: list) -> int:
    '''
    Scores the user based on their input

    This function takes the user's guess/word and compares it to the
    previously created list of possible words given the nine available letters.
    If the user's word is valid then a number of points equal to the length
    of the word are awarded, else the user recieves 0 points.

    Arguments:
    matches - a list of all the words from the dictionary which can be made
    letters - a list of the user's nine available letters
    '''
    # letters is a list but this line will display the list is a more
    # readable format for the user
    print("Your letters are " + " / ".join(letters))
    userGuess = input("Enter the longest word you can make in 30 seconds\n")
    for each in matches:
        if each == userGuess:
            return len(userGuess)
    print("Invalid word")
    return 0


def play_game(pointsTot: int) -> int:
    '''
    Calls all other functions

    This function runs my program but calling all the other functions
    individually as well as passing them variables, meaning I dont need and
    global variables.
    This funtion also acts as an output of the rount and total score to the
    user after each round.

    Arguments:
    pointsTot - the total points earned from all rounds so far
    '''
    # words is a dictionary of all words in the text file
    words = {}
    # Lists are created for vowels and consonants with itterations to give
    # accurate letter probabilities
    vowels = list("a"*15+"e"*21+"io"*13+"u"*5)
    conson = list("bfh"*2+"cg"*3+"d"*6+"jk"+"l"*5+"mp"*4+"n"*8+"q"+"rst"*9 +
                  "vwxyz")
    letters = []
    matches = []
    display = []

    dictionary_reader("words.txt", words)
    letters = select_characters(conson, vowels, letters)
    word_lookup(words, matches, letters, display)

    points = user_input(matches, letters)
    pointsTot += points

    print("You scored " + str(points))
    print("The longest words for this round were " + str(display))
    print("with a length of " + str(len(matches[0])))
    print("Your total points are " + str(pointsTot) + "\n")

    return pointsTot

# The actual gameshow has 8 rounds so I gave my version the same amount
for i in range(8):
    # This line opens a file containing ascii text and prints it to the console
    f = open("Ascii.txt", "r")
    print(f.read())
    f.close()
    print('Welcome to countdown')
    print('Round ' + str(i + 1))
    pointsTot = play_game(pointsTot)
