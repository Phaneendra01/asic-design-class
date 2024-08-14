# 🎮 Task 4: Tic-Tac-Toe Game Compilation and RISC-V Execution

## 1. 🖥️ C Program: tiktaktoe.c

```c
#include <stdio.h>

#define SIZE 3

void printBoard(char board[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf(" %c ", board[i][j]);
            if (j < SIZE - 1) printf("|");
        }
        printf("\n");
        if (i < SIZE - 1) printf("---|---|---\n");
    }
    printf("\n");
}

int checkWin(char board[SIZE][SIZE], char player) {
    // Check rows and columns
    for (int i = 0; i < SIZE; i++) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player) return 1;
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player) return 1;
    }
    // Check diagonals
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player) return 1;
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player) return 1;

    return 0;
}

int checkDraw(char board[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O') {
                return 0;
            }
        }
    }
    return 1;
}

void makeMove(char board[SIZE][SIZE], char player) {
    int row, col;
    while (1) {
        printf("Player %c, enter row (1-3) and column (1-3): ", player);
        scanf("%d %d", &row, &col);
        row--; col--;  // Convert to 0-indexed
        if (row >= 0 && row < SIZE && col >= 0 && col < SIZE && board[row][col] == ' ') {
            board[row][col] = player;
            break;
        } else {
            printf("Invalid move, try again.\n");
        }
    }
}

int main() {
    char board[SIZE][SIZE] = { {' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '} };
    char currentPlayer = 'X';

    printf("Welcome to Tic-Tac-Toe!\n\n");

    while (1) {
        printBoard(board);
        makeMove(board, currentPlayer);

        if (checkWin(board, currentPlayer)) {
            printBoard(board);
            printf("Player %c wins!\n", currentPlayer);
            break;
        } else if (checkDraw(board)) {
            printBoard(board);
            printf("It's a draw!\n");
            break;
        }

        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    return 0;
}
```

> 💡 This C program implements a simple Tic-Tac-Toe game for two players.

![C Code Snippet](https://github.com/user-attachments/assets/d1a03a24-e12f-41ae-80cf-0fc72cd48143)

## 2. 🚀 GCC Compilation Output

```bash
$ gcc tiktaktoe.c
$ ./a.out
Welcome to Tic-Tac-Toe!
# Game output follows...
```

![GCC Compilation Output](https://github.com/user-attachments/assets/736cb9a2-001c-4072-a2d4-e872f7e90ef7)

> ✅ Successful compilation and execution on a standard system.

## 3. 🔧 RISC-V GCC Compilation and Spike Execution

```bash
$ riscv64-unknown-elf-gcc -o tiktaktoe.o tiktaktoe.c
$ spike pk tiktaktoe.o
Welcome to Tic-Tac-Toe!
# Game output would appear here
```

![RISC-V Compilation](https://github.com/user-attachments/assets/67a03bac-ea6b-499e-844d-3efaf2e8d1d9)

> 🏗️ Compiling for RISC-V architecture and running in the Spike simulator.

## 4. 🔬 RISC-V GCC Compilation with -O1 Optimization

```bash
$ riscv64-unknown-elf-gcc -O1 -o tiktaktoe.o tiktaktoe.c
$ spike pk tiktaktoe.o
Welcome to Tic-Tac-Toe!
# Game output would appear here
```

![O1 Optimization](https://github.com/user-attachments/assets/6e8436a8-4e89-4b06-8f92-66dfc2b56ec5)

> 🚀 Level 1 optimization applied for improved performance.

## 5. ⚡ RISC-V GCC Compilation with -Ofast Optimization

```bash
$ riscv64-unknown-elf-gcc -Ofast -o tiktaktoe.o tiktaktoe.c
$ spike pk tiktaktoe.o
Welcome to Tic-Tac-Toe!
# Game output would appear here
```

![Ofast Optimization](https://github.com/user-attachments/assets/ff27c556-d113-43f8-b699-c20a6932a90c)

> 🏎️ Fastest optimization level applied for maximum speed.

---

### 📊 Comparison Table

| Compilation Method | Optimization | Purpose |
|--------------------|--------------|---------|
| Standard GCC       | None         | 🏁 Baseline compilation |
| RISC-V GCC         | None         | 🎯 RISC-V architecture targeting |
| RISC-V GCC         | -O1          | 🔨 Basic optimizations |
| RISC-V GCC         | -Ofast       | 🚀 Aggressive optimizations |

---

> 🎉 **Note:** As the GCC output matches with the Spike output for all optimization levels, no debugging is required. The game runs successfully on both standard and RISC-V architectures!

---

👨‍💻 Author Information
Name: Phaneendra M V
Roll Number: MT2024526

🎓 This project was completed by Phaneendra M V as part of the coursework.
