---
layout: post
title: Rock Paper Scissors Lizard Spock
---
***Solution to RPSLS***

Main Class
```java

public class Match {
	public static void main (String[] args) {

		Game newGame = new Game();

		System.out.println("Rock-Paper-Scissors-Lizard-Spock was created by"
		+ "\ninternet pioneer Sam Kass as an improvement on the classic game Rock-Paper-Scissors\n"
		+ "All hail Sam Kass.\n");
		System.out.print("Scissors cuts paper\n"
				+ "paper covers rock\n"
				+"rock crushes lizard\n"
				+"lizard poisons spock\n"
				+"Spock smashes scissors\n"
				+"Scissors decapitates lizard\n"
				+"lizard eats paper\n"
				+"paper disproves spock\n"
				+"Spock vaporizes rock\n"
				+"(and as it always has) rock crushes scissors\n\n");


	while(newGame.isDone() == false) {
				newGame.makeChoice();
				newGame.getChoiceFromUser();
				newGame.displayRoundResult();
		}//Loop to 5 wins;

				newGame.displayGameResults();
	}//Display results;
}
```
Random Pairing
```java
import java.util.Random;

public class HandPosition {

	private int choice;
	private Random rnd;
//---------------------
	//Default Constructor;
	public HandPosition() {
		choice = 0;
		rnd = new Random();
	}

	public void randomChoice() {

		choice = rnd.nextInt(5);

	}//END randomChoice;

	public boolean setChoice(String set) {

		switch(set) {
		case "rock":
			choice = 0;
			return true;

		case "paper":
			choice = 1;
			return true;

		case "scissors":
			choice = 2;
			return true;

		case "spock":
			choice = 3;
			return true;

		case "lizard":
			choice = 4;
			return true;

		case "quit":
			choice = 99;
			return false;

		default:
			return false;

		}
	}// End setChoice;

	public String choices() {
		return "Rock, Paper, Scissors, Lizard, Spock";
	}//END choices;

	public int compare(HandPosition op) {
		int m = ( 5 + this.choice - op.choice) % 5;

		if(this.choice == 99){
			return 99;

		} else if ( m == 1 || m == 3) {
			return 1;

		} else if (m == 2 || m == 4) {
			return -1;

		} else if (m == 0) {
			return 0;

		} else return 0;

	}//END compare;

	public String getName() {
		switch(choice) {
		case 0:
			return "rock";
		case 1:
			return "paper";
		case 2:
			return "scissors";
		case 3:
			return "spock";
		case 4:
			return "lizard";
		case 99:
			return " ";
		default:
			return "unknown";
		}
	}//END getName;
}
```
Match
```java
import java.util.Scanner;
public class Game {

	private int computerWins;
	private int userWins;
	private boolean userQuits;
	private HandPosition computer;
	private HandPosition user;
	private Scanner input = new Scanner(System.in);

//-------------------------------------------------
	//Default Constructor;
	public Game() {
		user = new HandPosition();
		computer = new HandPosition();
		computerWins = 0;
		userWins = 0;
		userQuits = false;

	}

	public boolean isDone() {
		if (userWins == 5||computerWins == 5||userQuits == true) {
			return true;

		} else return false;
	}//End isDone;

	public void makeChoice() {
		computer.randomChoice();

	}//END makeChoice;

	public void getChoiceFromUser() {
		System.out.print("\nWhat is your choice? ");


		if (user.setChoice(input.next()) == false) {
			userQuits = true;
		}else userQuits = false;

	}//END getChoiceFromUser;

	public void displayRoundResult() {

		switch(user.compare(computer)) {
		case 1:
			System.out.println("You win: " + user.getName() + " beats " + computer.getName());
			userWins++;
			break;
		case 0:
			System.out.println("Tie: both choose " + user.getName());
			break;
		case -1:
			System.out.println("You lose: " + computer.getName() + " beats " + user.getName());
			computerWins++;
			break;
		case 99:
			System.out.println("Thanks for playing!");
			break;
		default:
				System.out.print("Error");
		}

	}//END displayRoundResult;

	public void displayGameResults() {
		if(userWins == 5) {
			System.out.print("\nYou win the game, " + userWins + " to " + computerWins);
		}

		if(computerWins == 5) {
			System.out.print("\nYou lose the game, " + computerWins + " to " + userWins);
		}
	}//END displayGameResults;

}//END Game;
```
