# futureintern_c-_task_03
#include <iostream>
#include <vector>
using namespace std;

// Function to display the Tic-Tac-Toe board
void displayBoard(vector<vector<char>>& board) {
    cout << "\nTic-Tac-Toe Board:\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << board[i][j];
            if (j < 2) cout << " | ";
        }
        cout << endl;
        if (i < 2) cout << "--|---|--" << endl;
    }
    cout << endl;
}

// Function to check for a win or draw
char checkWinner(vector<vector<char>>& board) {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return board[i][0];
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return board[0][i];
    }

    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return board[0][0];
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return board[0][2];

    // Check if the board is full (draw)
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            if (board[i][j] != 'X' && board[i][j] != 'O') return ' ';

    return 'D'; // Indicate draw
}

// Function to handle player moves
bool makeMove(vector<vector<char>>& board, int player) {
    int row, col;
    char symbol = (player == 1) ? 'X' : 'O';
    cout << "Player " << player << " (" << symbol << "), enter your move (row and column: 1-3): ";
    cin >> row >> col;

    if (row < 1 || row > 3 || col < 1 || col > 3 || board[row - 1][col - 1] == 'X' || board[row - 1][col - 1] == 'O') {
        cout << "Invalid move! Try again." << endl;
        return false;
    }

    board[row - 1][col - 1] = symbol;
    return true;
}

// Main function to play the game
int main() {
    char playAgain;

    do {
        // Initialize the board
        vector<vector<char>> board(3, vector<char>(3));
        char ch = '1';
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                board[i][j] = ch++;

        int currentPlayer = 1;
        char result = ' ';

        cout << "\nWelcome to Tic-Tac-Toe!" << endl;

        // Main game loop
        while (result == ' ') {
            displayBoard(board);

            // Handle player move
            if (makeMove(board, currentPlayer)) {
                result = checkWinner(board);
                if (result == ' ') {
                    currentPlayer = (currentPlayer == 1) ? 2 : 1; // Switch player
                }
            }
        }

        // Display final board and result
        displayBoard(board);
        if (result == 'D') {
            cout << "It's a draw!" << endl;
        } else {
            cout << "Player " << ((result == 'X') ? 1 : 2) << " (" << result << ") wins!" << endl;
        }

        // Ask if the players want to play again
        cout << "Do you want to play again? (y/n): ";
        cin >> playAgain;

    } while (playAgain == 'y' || playAgain == 'Y');

    cout << "Thanks for playing Tic-Tac-Toe!" << endl;
    return 0;
}
