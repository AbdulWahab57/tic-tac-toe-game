#include <iostream>
using namespace std;

char board[3][3] = {{'1', '2', '3'}, {'4', '5', '6'}, {'7', '8', '9'}};
char currentPlayer = 'X';
int choice;
bool gameOver = false;

void DrawBoard() {
    cout << "Player 1 [X]  -  Player 2 [O]" << endl << endl;
    cout << "     |     |     " << endl;
    cout << "  " << board[0][0] << "  |  " << board[0][1] << "  |  " << board[0][2] << endl;
    cout << "_____|_____|_____" << endl;
    cout << "     |     |     " << endl;
    cout << "  " << board[1][0] << "  |  " << board[1][1] << "  |  " << board[1][2] << endl;
    cout << "_____|_____|_____" << endl;
    cout << "     |     |     " << endl;
    cout << "  " << board[2][0] << "  |  " << board[2][1] << "  |  " << board[2][2] << endl;
    cout << "     |     |     " << endl << endl;
}

bool CheckWin() {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2])
            return true;
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i])
            return true;
    }

    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2])
        return true;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0])
        return true;

    return false;
}

bool CheckTie() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O') {
                return false;
            }
        }
    }
    return true;
}

void TakeTurn() {
    bool validMove = false;

    while (!validMove) {
        cout << "Player " << (currentPlayer == 'X' ? "1" : "2") << "'s turn (" << currentPlayer << "): ";
        cin >> choice;

        int row = (choice - 1) / 3;
        int col = (choice - 1) % 3;

        if (choice < 1 || choice > 9 || board[row][col] == 'X' || board[row][col] == 'O') {
            cout << "Invalid move, try again." << endl;
        } else {
            board[row][col] = currentPlayer;
            validMove = true;
        }
    }
}

void SwitchPlayer() {
    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
}

int main() {
    while (!gameOver) {
        DrawBoard();
        TakeTurn();
        if (CheckWin()) {
            DrawBoard();
            cout << "Player " << (currentPlayer == 'X' ? "1" : "2") << " wins!" << endl;
            gameOver = true;
        } else if (CheckTie()) {
            DrawBoard();
            cout << "It's a tie!" << endl;
            gameOver = true;
        } else {
            SwitchPlayer();
        }
    }
    return 0;
}

