# number-game
import java.util.*;

public class numbergame {
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        int lowerBound = 1;
        int upperBound = 100;
        int maxAttempts = 5;
        int totalRounds = 0;
        int totalScore = 0;

        System.out.println("Welcome to the Number Guessing Game!");

        do {
            int randomNumber = generateRandomNumber(lowerBound, upperBound);
            int attempts = 0;

            System.out.println("\nRound " + (totalRounds + 1) + ":");
            System.out.println("Guess the number between " + lowerBound + " and " + upperBound);

            while (attempts < maxAttempts) {
                int userGuess = getUserGuess(scanner);

                if (userGuess == randomNumber) {
                    System.out.println("Congratulations! Your guess is correct.");
                    int roundScore = maxAttempts - attempts;
                    totalScore += roundScore;
                    System.out.println("Round Score: " + roundScore);
                    break;
                } else {
                    displayFeedback(userGuess, randomNumber);
                    attempts++;
                    if (attempts < maxAttempts) {
                        System.out.println("Attempts left: " + (maxAttempts - attempts));
                    }
                }
            }

            totalRounds++;

        } while (playAgain(scanner));

        System.out.println("\nGame Over!");
        System.out.println("Total Rounds Played: " + totalRounds);
        System.out.println("Total Score: " + totalScore);

        scanner.close();
    }

    private static int generateRandomNumber(int lowerBound, int upperBound) {
        return new Random().nextInt(upperBound - lowerBound + 1) + lowerBound;
    }

    private static int getUserGuess(Scanner scanner) {
        System.out.print("Enter your guess: ");
        return scanner.nextInt();
    }

    private static void displayFeedback(int userGuess, int randomNumber) {
        if (userGuess < randomNumber) {
            System.out.println("Too low! Try again.");
        } else {
            System.out.println("Too high! Try again.");
        }
    }

    private static boolean playAgain(Scanner scanner) {
        System.out.print("Do you want to play again? (yes/no): ");
        String choice = scanner.next().toLowerCase();
        return choice.equals("yes");
    }
}
