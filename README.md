# SOLVING-SUDOKO-USING-BACKTRACKING
#Algorithm:
Start from any cell and do the following steps recursively:
1. If the cell is empty, add a number that is not constrained. 
       a) If it is impossible to add a number due to constraints, report failure. 
       b) Else start a new thread on a new cell, starting from step 2. 
              i. If this thread reports a failure, repeat step 2 with a new number (and     
                 exhaust the old number)
              ii. If this thread reports success, report success, since we can assume that      
                  the last cell has been successfully filled. 

2. If the cell is filled, then skip this cell and start a new thread on a new cell,  
     starting from step 2. 
3. If the algorithm has managed to move beyond the bounds of the board, report  
    success. 
#PSEUDOCODE
//Utility Function
bool solve(char[][] board) {
    for (int r = 0 to r < 9) {
        for (int c = 0 to c < 9) {
            if (board[r][c] == '.') {
                for (char d = '1'; d <= '9'; d++) {
                    if (isSafe(board, r, c, d)) {
                        board[r][c] = d
                        if (solve(board)) 
                            return true
                        board[r][c] = '.'
                    }
                }
                return false
            }
        } 
    }
    return true
}

bool isSafe(char[][] board, int r, int c, char d) {
    for (int row = 0 to row < 9)
        if (board[row][c] == d) 
            return false
    for (int col = 0 to col < 9)
        if (board[r][col] == d)
            return false;
    for (int row = (r / 3) * 3 to row < (r / 3 + 1) * 3)
        for (int col = (c / 3) * 3 to col < (c / 3 + 1) * 3)
            if (board[row][col] == d) 
                return false
    return true
}

 
