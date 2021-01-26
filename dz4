import java.util.Scanner;

public class lesson4 {
    public static Scanner sc = new Scanner(System.in);

    private static char[][] gameMap;
    private static final char EMPTY_DOT = '●';
    private static final char X_DOT = 'X';
    private static final char O_DOT = '0';

    public static void main(String[] args) throws InterruptedException {
        StartGame();
    }

    private static void StartGame() throws InterruptedException {
        int size = 3;
        size = setSizeField();
        createGameMap(size);
        paintGameMap();
        int count = 0;
        while (true) {
            humanTurn();
            count++;
            paintGameMap();
            if (checkWinner(X_DOT)) {
                System.out.println("You win");
                break;
            }
            if (count == gameMap.length * gameMap[0].length) {
                System.out.println("Frendly Win");
                break;
            }
            System.out.println("---------");
            pcTurn();
            count++;
            paintGameMap();
            if (checkWinner(O_DOT)) {
                System.out.println("PC win");
                break;
            }
            if (count == gameMap.length * gameMap[0].length) {
                System.out.println("Frendly Win");
                break;
            }

        }
    }

    private static int setSizeField() {
        int size = 3;
        System.out.println("Введите ширину и высоту поля(по умолчанию поле 3х3)");
        Scanner sc = new Scanner(System.in);
        if (sc.hasNextInt()) {
            size = sc.nextInt();
        }
        return size;
    }

    private static void pcTurn() throws InterruptedException {
        try {
            Thread.sleep(700);
        } catch (Exception e) {

        }
        boolean turn = false;

        turn = turnHorizontalPC(X_DOT);
        if (!turn) {
            turn = turnVerticalPC(X_DOT);
        } else {
            turnDiagonalsPC(X_DOT);
        }
//        int x = 0;
//        int y = 0;
//        boolean checkCell;
//        Random rn = new Random();
//        do {
//            x = rn.nextInt(gameMap.length);
//            y = rn.nextInt(gameMap.length);
//            checkCell = isValidCell(x, y);
//        } while (!checkCell);
//        gameMap[x][y] = O_DOT;
    }

    private static void humanTurn() {
        int x = -1;
        int y = -1;
        boolean checkCell = false;
        do {
            System.out.println("Пожалуйста введите координаты в формате Y X");
            if (sc.hasNextInt()) {
                x = sc.nextInt() - 1;
            }
            if (sc.hasNextInt()) {
                y = sc.nextInt() - 1;
            }
            checkCell = isValidCell(x, y);
            sc.nextLine();
        } while (!checkCell);
        gameMap[x][y] = X_DOT;
    }

    private static boolean isValidCell(int x, int y) {
        if (x < 0 || y < 0 || x > gameMap.length || y > gameMap.length) {
            return false;
        }
        return gameMap[x][y] == EMPTY_DOT;
    }

    private static void paintGameMap() {
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                System.out.print("|");
                System.out.print(gameMap[i][j]);
            }
            System.out.println("|");
        }
    }

    private static void createGameMap(int size) {
        if (size < 3) {
            System.out.println("Маленькое поле");
            System.exit(1);
        }
        gameMap = new char[size][size];
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                gameMap[i][j] = EMPTY_DOT;
            }
        }
    }

    private static boolean checkWinner(char c) {
        return checkWinnerHorizontal(c) ||
                checkWinnerVertical(c) ||
                checkWinnerDiagonals(c);
    }

    private static boolean turnHorizontalPC(char c) {
        int x = 0;
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                if (gameMap[i][j] == c) {
                    x++;
                    if (x == gameMap.length - 1) {
                        if (hasTurnOfLine(i)) {
                            boolean turnTrue = false;
                            for (int k = 0; k < gameMap[j].length; k++) {
                                turnTrue = isValidCell(i, k);
                                if (turnTrue) {
                                    gameMap[i][k] = O_DOT;
                                    return true;
                                }
                            }
                        } else {
                            x = 0;
                        }
                    }
                }
            }
            x = 0;
        }
        return false;
    }

    private static boolean hasTurnOfLine(int line) {
        boolean turnTrue = false;
        for (int i = 0; i < gameMap.length; i++) {
            turnTrue = isValidCell(line, i);
            if (turnTrue)
                return turnTrue;
        }
        return turnTrue;
    }

    private static boolean turnVerticalPC(char c) {
        int x = 0;
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                if (gameMap[j][i] == c) {
                    x++;
                    if (x == gameMap.length - 1) {
                        if (hasTurnOfRow(i)) {
                            return true;
                        } else {
                            x = 0;
                        }
                    }
                }
            }
        }
        return false;
    }

    private static boolean hasTurnOfRow(int row) {
        boolean turnTrue = false;
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[row].length; j++) {
                if (i == row) {
                    turnTrue = isValidCell(j, i);
                    if (turnTrue) {
                        gameMap[j][i] = O_DOT;
                        return turnTrue;
                    } else {
                        continue;
                    }
                }
            }
        }
        return false;
    }

    private static boolean turnDiagonalsPC(char c) {
        int startPos = 0;
        int endPos = gameMap[0].length - 1;
        int x = 0;
        int y = 0;
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                if (j == startPos) {
                    if (gameMap[i][j] == c) {
                        x++;
                    }
                    if (x == gameMap.length - 1) {
                        //to do
                    }
                }
                if (j == endPos) {
                    if (gameMap[i][j] == c) {
                        if (startPos != endPos) {
                            y++;
                        }
                    }
                }
            }
            if (x == gameMap.length) {
                return true;
            }
            startPos++;
            endPos--;
        }
        return false;
    }

    private static boolean checkWinnerHorizontal(char c) {
        int x = 0;
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                if (gameMap[j][i] == c) {
                    x++;
                }
            }
            if (x == gameMap.length) {
                return true;
            } else {
                x = 0;
            }
        }
        return false;
    }

    private static boolean checkWinnerVertical(char c) {
        int x = 0;
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                if (gameMap[i][j] == c) {
                    x++;
                }
            }
            if (x == gameMap.length) {
                return true;
            } else {
                x = 0;
            }
        }
        return false;
    }

    private static boolean checkWinnerDiagonals(char c) {
        int startPos = 0;
        int endPos = gameMap[0].length - 1;
        int x = 0;
        int y = 0;
        for (int i = 0; i < gameMap.length; i++) {
            for (int j = 0; j < gameMap[i].length; j++) {
                if (j == startPos) {
                    if (gameMap[i][j] == c) {
                        x++;
                    }
                }
                if (j == endPos) {
                    if (gameMap[i][j] == c) {
                        y++;
                    }
                }
            }
            if (x == gameMap.length || y == gameMap.length) {
                return true;
            }
            startPos++;
            endPos--;
        }
        return false;
    }
}
