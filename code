   #include <iostream>
using namespace std;

// Abstract base class representing a generic game
class Game {
public:
    virtual void startGame() = 0; // Pure virtual function
    virtual void drawBoard() const = 0;
    virtual bool isGameOver() const = 0;
    virtual void printResult() const = 0;
    virtual ~Game() {} // Virtual destructor for proper cleanup of derived objects
};

// Derived class representing a TicTacToe game
class TicTacToe : public Game {
private:
    char board[3][3];
    char currentPlayer;

protected:
    // Helper function to check if a player has won
    bool checkWin(char player) const {
        // Check rows and columns
        for (int i = 0; i < 3; i++) {
            if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
                (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
                return true;
            }
        }
        // Check diagonals
        if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
            (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
            return true;
        }
        return false;
    }

public:
    // Constructor to initialize the game
    TicTacToe() : currentPlayer('X') {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
    }

    // Implementation of abstract methods from Game class
    void drawBoard() const override {
        cout << "-------------\n";
        for (int i = 0; i < 3; i++) {
            cout << "| ";
            for (int j = 0; j < 3; j++) {
                cout << board[i][j] << " | ";
            }
            cout << "\n-------------\n";
        }
    }

    bool makeMove(int row, int col) {
        if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
            return false;
        }
        board[row][col] = currentPlayer;
        return true;
    }

    void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    bool isGameOver() const override {
        if (checkWin('X') || checkWin('O')) {
            return true;
        }
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == ' ') {
                    return false;
                }
            }
        }
        return true; // Draw
    }

    void printResult() const override {
        drawBoard();
        if (checkWin('X')) {
            cout << "Player X wins!\n";
        } else if (checkWin('O')) {
            cout << "Player O wins!\n";
        } else {
            cout << "It's a draw!\n";
        }
    }

    void startGame() override {
        int row, col;
        while (!isGameOver()) {
            drawBoard();
            cout << "Player " << currentPlayer << ", enter row (0-2) and column (0-2): ";
            cin >> row >> col;
            if (makeMove(row, col)) {
                if (isGameOver()) {
                    break;
                }
                switchPlayer();
            } else {
                cout << "Invalid move. Try again.\n";
            }
        }
        printResult();
    }
};

int main() {
    Game* game = new TicTacToe();
    game->startGame();
    delete game; // Clean up memory
    return 0;
}
