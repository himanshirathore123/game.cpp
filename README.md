#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <ctime>
#include <cctype>

using namespace std;

int main()
{
    const int MAX_WRONG = 8;

    vector<pair<string, string>> words = {
        {"GUESS", "A word meaning to estimate or suppose"},
        {"HANGMAN", "A classic word-guessing game"},
        {"DIFFICULT", "A word meaning hard or challenging"},
        {"APPLE", "A common fruit that is often red, green, or yellow"},
        {"COMPUTE", "To calculate or reckon a figure"},
        {"EXAMPLE", "A representative form or pattern"},
        {"FREEDOM", "The power or right to act, speak, or think as one wants"},
        {"HISTORY", "The study of past events"},
        {"LIBRARY", "A place where books are kept"},
        {"MORNING", "The early part of the day"},
        {"NETWORK", "A group of interconnected people or things"},
        {"OFFICER", "A person holding a position of authority"},
        {"PACKAGE", "A wrapped or boxed item"},
        {"QUALITY", "The standard of something as measured against other things"},
        {"REQUEST", "An act of asking politely or formally for something"},
        {"SUPPORT", "To bear all or part of the weight of something"},
        {"TEACHER", "A person who teaches, especially in a school"},
        {"TOMORROW", "The day after today"},
        {"UNIVERSAL", "Applicable to all cases"},
        {"VACATION", "An extended period of leisure and recreation"}
    };


    srand(static_cast<unsigned int>(time(0)));
    random_shuffle(words.begin(), words.end());
    const string THE_WORD = words[0].first;
    const string HINT = words[0].second;

    int wrong = 0;
    string soFar(THE_WORD.size(), '_');
    string used = "";

    cout << "Welcome to Hangman. Good luck!\n";
    cout << "Hint: " << HINT << "\n";

    while ((wrong < MAX_WRONG) && (soFar != THE_WORD))
    {
        cout << "\nYou have " << (MAX_WRONG - wrong) << " incorrect guesses left.\n";
        cout << "\nYou've used the following letters:\n" << used << endl;
        cout << "\nSo far, the word is:\n" << soFar << endl;

        char guess;
        cout << "\nEnter your guess: ";
        cin >> guess;

        guess = toupper(guess);

        while (used.find(guess) != string::npos)
        {
            cout << "\nYou have already guessed " << guess << endl;
            cout << "Enter your guess: ";
            cin >> guess;

            guess = toupper(guess);
        }

        used += guess;

        if (THE_WORD.find(guess) != string::npos)
        {
            cout << "That's right! " << guess << " is in the word.\n";

            for (int i = 0; i < THE_WORD.length(); ++i)
                if (THE_WORD[i] == guess)
                    soFar[i] = guess;
        }
        else
        {
            cout << "Sorry, " << guess << " isn't in the word.\n";
            ++wrong;
        }
    }

    if (wrong == MAX_WRONG)
        cout << "\nYou've been hanged.";
    else
        cout << "\nYou guessed it!";

    cout << "\nThe word was " << THE_WORD << endl;

    return 0;
}# game.cpp
