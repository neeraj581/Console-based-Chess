/*
    PLEASE READ A USER GUIDE BEFORE RUNNING THIS PROGRAM 
    IT WILL HELP YOU TO RUN THIS PROGRAM SMOOTHLY 
    IF YOU HAVE ALREADY READ IT THEN YOU ARE GOOD TO GO.





               _____           ______   ______                  ____
    |      |  |       |       |        /      \   |\      /|   |
    |  /\  |  |_____  |       |        |      |   | \    / |   |____
    | /  \ |  |       |       |        |      |   |  \  /  |   | 
    |/    \|  |_____  |_____  |______   \____/    |   \/   |   |____
*/
#include <iostream>
using namespace std;
class Piece
{
public:
    Piece(char colour) : Colour(colour) {}
    ~Piece() {}
    virtual char GetPiece() = 0;
    char GetColor() {
        return Colour;
    }
    bool IsLegalMove(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) {
        Piece* piece = Board[endrow][endcol];
        if ((piece == 0) || (Colour != piece->GetColor())) {
            return AreSquaresLegal(startrow, startcol, endrow, endcol, Board);
        }
        return false;
    }
private:
    virtual bool AreSquaresLegal(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) = 0;
    char Colour;
};

class Pawn : public Piece
{
public:
    Pawn(char colour) : Piece(colour) {}
    ~Pawn() {}
private:
    virtual char GetPiece() {
        return 'P';
    }
    bool AreSquaresLegal(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) {
        Piece* piece = Board[endrow][endcol];
        if (piece == 0) {
            // Destination square is unoccupied
            if (startcol == endcol) {
                if (GetColor() == 'W') {
                    if (endrow == startrow + 1) {
                        return true;
                    }
                    else if (endrow == startrow + 2) {
                        return true;
                    }
                } else {
                    if (endrow == startrow - 1) {
                        return true;
                    }
                    else if (endrow == startrow - 2) {
                        return true;
                    }
                }
            }
        } else {
            // Dest holds piece of opposite color
            if ((startcol == endcol + 1) || (startcol == endcol - 1)) {
                if (GetColor() == 'W') {
                    if (endrow == startrow + 1) {
                        return true;
                    }
                } else {
                    if (endrow == startrow - 1) {
                        return true;
                    }
                }
            }
        }
        return false;
    }
};

class Knight : public Piece
{
public:
    Knight(char colour) : Piece(colour) {}
    ~Knight() {}
private:
    virtual char GetPiece() {
        return 'N';
    }
    bool AreSquaresLegal(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) {
        // Destination square is unoccupied or occupied by opposite color
        if ((startcol == endcol + 1) || (startcol == endcol - 1)) {
            if ((startrow == endrow + 2) || (startrow == endrow - 2)) {
                return true;
            }
        }
        if ((startcol == endcol + 2) || (startcol == endcol - 2)) {
            if ((startrow == endrow + 1) || (startrow == endrow - 1)) {
                return true;
            }
        }
        return false;
    }
};

class Bishop : public Piece
{
public:
    Bishop(char colour) : Piece(colour) {}
    ~Bishop() {}
private:
    virtual char GetPiece() {
        return 'B';
    }
    bool AreSquaresLegal(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) {
        if ((endcol - startcol == endrow - startrow) || (endcol - startcol == startrow - endrow)) {
            // Make sure that all   squares are empty
            int Rowoffset = (endrow - startrow > 0) ? 1 : -1;
            int Coloffset = (endcol - startcol > 0) ? 1 : -1;
            int CheckRow;
            int CheckCol;
            for (CheckRow = startrow + Rowoffset, CheckCol = startcol + Coloffset;
                 CheckRow !=  endrow;
                 CheckRow = CheckRow + Rowoffset, CheckCol = CheckCol + Coloffset)
            {
                if (Board[CheckRow][CheckCol] != 0) {
                    return false;
                }
            }
            return true;
        }
        return false;
    }
};

class Rook : public Piece
{
public:
    Rook(char colour) : Piece(colour) {}
    ~Rook() {}
private:
    virtual char GetPiece() {
        return 'R';
    }
    bool AreSquaresLegal(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) {
        if (startrow == endrow) {
            // Make sure that all   squares are empty
            int Coloffset = (endcol - startcol > 0) ? 1 : -1;
            for (int CheckCol = startcol + Coloffset; CheckCol !=  endcol; CheckCol = CheckCol + Coloffset) {
                if (Board[startrow][CheckCol] != 0) {
                    return false;
                }
            }
            return true;
        } else if (endcol == startcol) {
            // Make sure that all   squares are empty
            int Rowoffset = (endrow - startrow > 0) ? 1 : -1;
            for (int CheckRow = startrow + Rowoffset; CheckRow !=  endrow; CheckRow = CheckRow + Rowoffset) {
                if (Board[CheckRow][startcol] != 0) {
                    return false;
                }
            }
            return true;
        }
        return false;
    }
};

class Queen : public Piece
{
public:
    Queen(char colour) : Piece(colour) {}
    ~Queen() {}
private:
    virtual char GetPiece() {
        return 'Q';
    }
    bool AreSquaresLegal(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) {
        if (startrow == endrow) {
            // Make sure that all   squares are empty
            int Coloffset = (endcol - startcol > 0) ? 1 : -1;
            for (int CheckCol = startcol + Coloffset; CheckCol !=  endcol; CheckCol = CheckCol + Coloffset) {
                if (Board[startrow][CheckCol] != 0) {
                    return false;
                }
            }
            return true;
        } else if (endcol == startcol) {
            // Make sure that all   squares are empty
            int Rowoffset = (endrow - startrow > 0) ? 1 : -1;
            for (int CheckRow = startrow + Rowoffset; CheckRow !=  endrow; CheckRow = CheckRow + Rowoffset) {
                if (Board[CheckRow][startcol] != 0) {
                    return false;
                }
            }
            return true;
        } else if ((endcol - startcol == endrow - startrow) || (endcol - startcol == startrow - endrow)) {
            // Make sure that all   squares are empty
            int Rowoffset = (endrow - startrow > 0) ? 1 : -1;
            int Coloffset = (endcol - startcol > 0) ? 1 : -1;
            int CheckRow;
            int CheckCol;
            for (CheckRow = startrow + Rowoffset, CheckCol = startcol + Coloffset;
                 CheckRow !=  endrow;
                 CheckRow = CheckRow + Rowoffset, CheckCol = CheckCol + Coloffset)
            {
                if (Board[CheckRow][CheckCol] != 0) {
                    return false;
                }
            }
            return true;
        }
        return false;
    }
};

class King : public Piece
{
public:
    King(char colour) : Piece(colour) {}
    ~King() {}
private:
    virtual char GetPiece() {
        return 'K';
    }
    bool AreSquaresLegal(int startrow, int startcol, int endrow, int endcol, Piece* Board[8][8]) {
        int rowDelta = endrow - startrow;
        int colDelta = endcol - startcol;
        if (((rowDelta >= -1) && (rowDelta <= 1)) &&
            ((colDelta >= -1) && (colDelta <= 1)))
        {
            return true;
        }
        return false;
    }
};

class Board
{
public:
    Board() {
        for (int row = 0; row < 8; ++row) {
            for (int col = 0; col < 8; ++col) {
                board[row][col] = 0;
            }
        }
        // Allocate and place black pieces
        for (int col = 0; col < 8; ++col) {
            board[6][col] = new Pawn('B');
        }
        board[7][0] = new Rook('B');
        board[7][1] = new Knight('B');
        board[7][2] = new Bishop('B');
        board[7][3] = new King('B');
        board[7][4] = new Queen('B');
        board[7][5] = new Bishop('B');
        board[7][6] = new Knight('B');
        board[7][7] = new Rook('B');
        // Allocate and place white pieces
        for (int col = 0; col < 8; ++col) {
            board[1][col] = new Pawn('W');
        }
        board[0][0] = new Rook('W');
        board[0][1] = new Knight('W');
        board[0][2] = new Bishop('W');
        board[0][3] = new King('W');
        board[0][4] = new Queen('W');
        board[0][5] = new Bishop('W');
        board[0][6] = new Knight('W');
        board[0][7] = new Rook('W');
    }
    ~Board() {
        for (int row = 0; row < 8; ++row) {
            for (int col = 0; col < 8; ++col) {
                delete board[row][col];
                board[row][col] = 0;
            }
        }
    }

    void Print() {
        using namespace std;
        const int SquareWidth = 4;
        const int SquareHeight = 3;
        for (int row = 0; row < 8*SquareHeight; ++row) {
            int Squarerow = row/SquareHeight;
            // Print side border with numbering
            if (row % 3 == 1) {
                cout << '-' << (char)('1' + 7 - Squarerow) << '-';
            } else {
                cout << "---";
            }
            // Print the chess board
            for (int col = 0; col < 8*SquareWidth; ++col) {
                int SquareCol = col/SquareWidth;
                if (((row % 3) == 1) && ((col % 4) == 1 || (col % 4) == 2) && board[7-Squarerow][SquareCol] != 0) {
                    if ((col % 4) == 1) {
                        cout << board[7-Squarerow][SquareCol]->GetColor();
                    } else {
                        cout << board[7-Squarerow][SquareCol]->GetPiece();
                    }
                } else {
                    if ((Squarerow + SquareCol) % 2 == 1) {
                        cout << '*';
                    } else {
                        cout << ' ';
                    }
                }
            }
            cout << endl;
        }
        // Print the bottom border with numbers
        for (int row = 0; row < SquareHeight; ++row) {
            if (row % 3 == 1) {
                cout << "---";
                for (int col = 0; col < 8*SquareWidth; ++col) {
                    int SquareCol = col/SquareWidth;
                    if ((col % 4) == 1) {
                        cout << (SquareCol + 1);
                    } else {
                        cout << '-';
                    }
                }
                cout << endl;
            } else {
                for (int col = 1; col < 9*SquareWidth; ++col) {
                    cout << '-';
                }
                cout << endl;
            }
        }
    }

    bool IsInCheck(char colour) {
        // Find the king
        int iKingRow;
        int iKingCol;
        for (int row = 0; row < 8; ++row) {
            for (int col = 0; col < 8; ++col) {
                if (board[row][col] != 0) {
                    if (board[row][col]->GetColor() == colour) {
                        if (board[row][col]->GetPiece() == 'K') {
                            iKingRow = row;
                            iKingCol = col;
                        }
                    }
                }
            }
        }
        // Run through the opponent's pieces and see if any can take the king
        for (int row = 0; row < 8; ++row) {
            for (int col = 0; col < 8; ++col) {
                if (board[row][col] != 0) {
                    if (board[row][col]->GetColor() != colour) {
                        if (board[row][col]->IsLegalMove(row, col, iKingRow, iKingCol, board)) {
                            return true;
                        }
                    }
                }
            }
        }

        return false;
    }

    bool CanMove(char colour) {
        // Run through all pieces
        for (int row = 0; row < 8; ++row) {
            for (int col = 0; col < 8; ++col) {
                if (board[row][col] != 0) {
                    // If it is a piece of the current player, see if it has a legal move
                    if (board[row][col]->GetColor() == colour) {
                        for (int iMoveRow = 0; iMoveRow < 8; ++iMoveRow) {
                            for (int iMoveCol = 0; iMoveCol < 8; ++iMoveCol) {
                                if (board[row][col]->IsLegalMove(row, col, iMoveRow, iMoveCol, board)) {
                                    // Make move and check whether king is in check
                                    Piece* qpTemp					= board[iMoveRow][iMoveCol];
                                    board[iMoveRow][iMoveCol]	= board[row][col];
                                    board[row][col]			= 0;
                                    bool bCanMove = !IsInCheck(colour);
                                    // Undo the move
                                    board[row][col]			= board[iMoveRow][iMoveCol];
                                    board[iMoveRow][iMoveCol]	= qpTemp;
                                    if (bCanMove) {
                                        return true;
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
        return false;
    }

    Piece* board[8][8];
};

class Chess
{
public:
    Chess() : mcPlayerTurn('W') {}
    ~Chess() {}

    void Start() {
        do {
            GetNextMove(mqGameBoard.board);
            AlternateTurn();
        } while (!IsGameOver());
        mqGameBoard.Print();
    }
    void GetNextMove(Piece* Board[8][8]) {
        using namespace std;
        bool bValidMove		= false;
        do {
            mqGameBoard.Print();

            // Get input and convert to coordinates
            cout << mcPlayerTurn << "'s Move: ";
            int iStartMove;
            cin >> iStartMove;
            int iStartRow = (iStartMove / 10) - 1;
            int iStartCol = (iStartMove % 10) - 1;

            cout << "To: ";
            int iEndMove;
            cin >> iEndMove;
            int iEndRow = (iEndMove / 10) - 1;
            int iEndCol = (iEndMove % 10) - 1;

            // Check that the indices are in range
            // and that the source and destination are different
            if ((iStartRow >= 0 && iStartRow <= 7) &&
                (iStartCol >= 0 && iStartCol <= 7) &&
                (iEndRow >= 0 && iEndRow <= 7) &&
                (iEndCol >= 0 && iEndCol <= 7)) {
                // Additional checks in here
                Piece* qpCurrPiece = Board[iStartRow][iStartCol];
                // Check that the piece is the correct color
                if ((qpCurrPiece != 0) && (qpCurrPiece->GetColor() == mcPlayerTurn)) {
                    // Check that the destination is a valid destination
                    if (qpCurrPiece->IsLegalMove(iStartRow, iStartCol, iEndRow, iEndCol, Board)) {
                        // Make the move
                        Piece* qpTemp					= Board[iEndRow][iEndCol];
                        Board[iEndRow][iEndCol]		    = Board[iStartRow][iStartCol];
                        Board[iStartRow][iStartCol]	    = 0;
                        // Make sure that the current player is not in check
                        if (!mqGameBoard.IsInCheck(mcPlayerTurn)) {
                            delete qpTemp;
                            bValidMove = true;
                        } else { // Undo the last move
                            Board[iStartRow][iStartCol] = Board[iEndRow][iEndCol];
                            Board[iEndRow][iEndCol]		= qpTemp;
                        }
                    }
                }
            }
            if (!bValidMove) {
                cout << "Invalid Move!" << endl;
            }
        } while (!bValidMove);
    }

    void AlternateTurn() {
        mcPlayerTurn = (mcPlayerTurn == 'W') ? 'B' : 'W';
    }

    bool IsGameOver() {
        // Check that the current player can move
        // If not, we have a stalemate or checkmate
        bool bCanMove(false);
        bCanMove = mqGameBoard.CanMove(mcPlayerTurn);
        if (!bCanMove) {
            if (mqGameBoard.IsInCheck(mcPlayerTurn)) {
                AlternateTurn();
                std::cout << "Checkmate, " << mcPlayerTurn << " Wins!" << std::endl;
            } else {
                std::cout << "Stalemate!" << std::endl;
            }
        }
        return !bCanMove;
    }
private:
    Board mqGameBoard;
    char mcPlayerTurn;
};

int main() {
    Chess Game;
    Game.Start();
    return 0;
}
