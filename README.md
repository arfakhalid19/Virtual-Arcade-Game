# Virtual-Arcade-Game
Developed a Virtual Arcade Game in C++, featuring Tic-Tac-Toe, Rock-Paper-Scissors, Number Guessing, and a Quiz Game. Implemented a menu-driven system, randomization, and input validation to enhance gameplay. This project showcases C++ programming skills, problem-solving abilities, and game logic implementation.





#include <iostream>
#include<conio.h>
#include <ctime>
using namespace std;

//TIC-TAC-TOE GAME
// Function to display the board
void drawBoard(char board[3][3])
{
    cout << "-------------\n";
    for (int i = 0; i < 3; i++)
    {	
        cout << "| ";
        for (int j = 0; j < 3; j++)
        {
            cout << board[i][j] << " | ";
        }
        cout << "\n-------------\n";
    }
}

// Function to check if a player has won
bool checkWin(char board[3][3], char player)
{
    // Check rows and columns
    for (int i = 0; i < 3; i++)
    {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) || // Row
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) // Column
        {
            return true;
        }
    }

    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) || // Main diagonal
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) // Opposite diagonal
    {
        return true;
    }

    return false;
}

//ROCK PAPER SCISSORS GAME
int determineWinner(char userChoice, char compChoice) {
    if (userChoice == compChoice)
        return 0; // Draw
    else if ((userChoice == 'r' && compChoice == 's') ||
             (userChoice == 'p' && compChoice == 'r') ||
             (userChoice == 's' && compChoice == 'p'))
        return 1; // User wins
    else
        return -1;}


char generateCOMPChoice() {
    int randomValue = rand() % 3; // Generate a number between 0 and 2
    switch (randomValue) {
        case 0: return 'r'; // Rock
        case 1: return 'p'; // Paper
        case 2: return 's'; // Scissors
    }
    return 'r';
}
    
// Function to get a valid answer
char ValidAnswer() {
    char answer;
    while (true) { // Keep looping until valid input
        cin >> answer;              // Read input
        answer = toupper(answer);   // Convert to uppercase
        if (answer == 'A' || answer == 'B' || answer == 'C' || answer == 'D') {
            return answer;          // Return valid input
        } else {
            cout << "Invalid input! Please enter A, B, C, or D: ";
        }
}
}
int main() 
{
    int choice;
    char playAgain;

    while (true) 
    {
        cout << "\n--------------- Welcome to our VIRTUAL ARCADE ^_^ ---------------"<<endl;
        cout << "\nGame Menu (Select 1-4) press 0 to exit:";
        cout << "\n1. Number Guessing Game";
        cout << "\n2. Tic-Tac-Toe Game";
        cout << "\n3. Rock Paper Scissors";
        cout << "\n4. Quiz Game";
        cout << "\n0. Exit"<<endl;
        cout << "\nEnter your choice: "<<endl;
        cin >> choice;

        switch (choice) 
        {
            case 1:
               { srand(time(0)); //random number generator
    int secretNumber = rand() % 10 + 1; // Random number between 1 and 10
    int userGuess, guessCount;

    cout << "\n----------Welcome to the Number Guessing Game!----------" << endl;
    cout << "I have chosen a number between 1 and 10." << endl;
    cout << "Can you guess what it is?" << endl;

    while (userGuess != secretNumber) {
        cout << "Enter your guess: "<<endl;
        cin >> userGuess;
        guessCount++;

        if (userGuess < secretNumber) {
            cout << "Too low! Try again." << endl;
        } else if (userGuess > secretNumber) {
            cout << "Too high! Try again." << endl;
        } else {
            cout << "Congratulations! You guessed the number in " << guessCount << " attempts." << endl;
        }
    }
                break;}
    case 2:   
            {
                // Start Tic-Tac-Toe game
                cout << "\nYou selected Tic-Tac-Toe Game"<<endl;
                
                char board[3][3] = { {' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '} }; // Empty board
                char currentPlayer = 'X'; // Player 'X' starts
                int row, col; // To store player moves
                bool gameWon = false; // Flag to check win condition

                cout << "\n----------Welcome to Tic-Tac-Toe!----------"<<endl;

                
                for (int turn = 1; turn <= 9; turn++) 
                {
                    drawBoard(board);

                    // Ask the current player for their move
                    while (true) 
                    {
                        cout << "Player " << currentPlayer << ", enter your move (row and column, 0-2): ";
                        cin >> row >> col;

                        // Validate the move
                        if (row < 0 || row > 2 || col < 0 || col > 2) 
                        {
                            cout << "\nInvalid input! Please enter values between 0 and 2.";
                        } 
                        else if (board[row][col] != ' ') 
                        {
                            cout << "\nCell already occupied! Try another cell.";
                        } 
                        else 
                        {
                            break; // Valid move
                        }
                    }

                    // Update the board
                    board[row][col] = currentPlayer;

                    // Check if the current player has won
                    if (checkWin(board, currentPlayer)) 
                    {
                        drawBoard(board);
                        cout << "Player " << currentPlayer << " wins!\n";
                        gameWon = true;
                        break;
                    }

                    // Switch player (toggle between 'X' and 'O')
                    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
                }

                // If no one wins after 9 turns, it's a draw
                if (!gameWon) 
                {
                    drawBoard(board);
                    cout << "It's a draw!\n";
                }
                break;
            }
case 3:
{
    char userChoice1, userChoice2, compChoice;
    int gameMode;

    cout << "---------- Welcome to Rock-Paper-Scissors!! ----------"<<endl;
    cout << "\nSelect Game Mode:"<<endl;
    cout << "1. Play with Computer\n";
    cout << "2. Play with Another Player\n"<<endl;
    cout << "Enter your choice (1 or 2): "<<endl;
    cin >> gameMode;

    switch (gameMode) {
        case 1: // Play with Computer
        {
            srand(time(0)); // Seed random number generator

            cout << "Enter 'r' for Rock, 'p' for Paper, and 's' for Scissors.\n";

            while (true) {
                // Get user's choice
                while (true) {
                    cout << "\nYour choice: ";
                    cin >> userChoice1;
                    if (userChoice1 == 'r' || userChoice1 == 'p' || userChoice1 == 's')
                        break;
                    else
                        cout << "Invalid choice! Please enter 'r', 'p', or 's'.\n";
                }

                // Generate computer's choice
                compChoice = generateCOMPChoice();
                string compChoiceName = (compChoice == 'r') ? "Rock" : (compChoice == 'p') ? "Paper" : "Scissors";
                cout << "Computer's choice: " << compChoiceName << endl;

                // Determine the result
                int gameResult = determineWinner(userChoice1, compChoice);
                if (gameResult == 0)
                    cout << "It's a draw!\n";
                else if (gameResult == 1)
                    cout << "You win!\n";
                else
                    cout << "Computer wins!\n";

                break; // End game loop for single-player mode
            }
            break;
        }
        case 2: // Play with Another Player
        {
            cout << "Player 1, it's your turn. Enter 'r' for Rock, 'p' for Paper, and 's' for Scissors.\n"<<endl; 
            cout << "Player 1, Enter your choice: "<<endl;
            userChoice1 = _getch(); // Read without showing input
            cout<<"*"<<endl;
            
            cout << "Player 2, Enter your choice:"<<endl;
            userChoice2 = _getch();
            cout<<"*"<<endl;

            // Reveal choices and determine the result
            cout << "Player 1 chose: " << userChoice1 << "\n";
            cout << "Player 2 chose: " << userChoice2 << "\n"<<endl;

            // Determine the result
            int gameResult = determineWinner(userChoice1, userChoice2);
            if (gameResult == 0)
                cout << "It's a draw!\n";
            else if (gameResult == 1)
                cout << "Player 1 wins!\n";
            else
                cout << "Player 2 wins!\n";

            break; // End game loop for multiplayer mode
        }
        default:
            cout << "Invalid choice! Returning to the main menu.\n";
            break;
    }

    break;
}
        case 4:
    {
   cout << "----------Welcome to the Quiz Game!!----------" << endl;
    cout << "Answer the following questions by typing A, B, C, or D.\n";
    cout << "--------------------------------------------\n\n";

    int score = 0;

    // Store questions, options, and answers in arrays
    string questions[] = {
        "1. What is the capital of Pakistan?",
        "2. Which planet is known as the Red Planet?",
        "3. What is the boiling point of water?"
    };

    string options[][4] = {
        {"A. Lahore", "B. Karachi", "C. Islamabad", "D. Peshawar"},
        {"A. Earth", "B. Mars", "C. Jupiter", "D. Venus"},
        {"A. 90 degrees Celsius", "B. 100 degrees Celsius", "C. 120 degrees Celsius", "D. 80 degrees Celsius"}
    };

    char correctAnswers[] = {'C', 'B', 'B'}; // Correct answers for each question

    // Loop through all questions
    for (int i = 0; i < 3; i++) {
        cout << questions[i] << endl;
        for (int j = 0; j < 4; j++) {
            cout << options[i][j] << endl; // Print each option
        }
        cout << "Your answer: ";
        char userAnswer = ValidAnswer(); // Get user input
        if (userAnswer == correctAnswers[i]) {
            cout << "Correct!\n";
            score++;
        } else {
            cout << "Wrong! The correct answer is " << correctAnswers[i] << ".\n";
        }
        cout << "--------------------------------------------\n";
    }

    // Display final score
    cout << "Quiz Over! Your final score is: " << score << " / 3\n";

    if (score == 3) {
        cout << "Excellent! You got a perfect score!" << endl;
    } else if (score >= 2) {
        cout << "Good job! Keep improving!" << endl;
    } else {
        cout << "Better luck next time! Keep practicing!" << endl;
    }

    break;}


 
            case 0:
                cout << "Exiting the program. Goodbye!\n";
                return 0; // Exit the program
            default:
                cout << "Invalid choice. Please try again.\n";
        }
        cout<<endl;
        // Ask if the user wants to play again
        cout << "Do you want to play again? (y/n): ";
        cin >> playAgain;

        // If user chooses 'n' or 'N', exit the program
        if (playAgain == 'n' || playAgain == 'N') 
        {
            cout << "Exiting the program. Goodbye!\n";
            break; // Exit the while loop
        } 
        else if (playAgain != 'y' && playAgain != 'Y') 
        {
            cout << "Invalid input. Exiting the program.\n";
            break; // Exit the loop in case of invalid input
        }
    
    }

    return 0;
}

