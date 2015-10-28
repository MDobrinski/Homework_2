# Homework Number 2
## Problem 1.6 from chapter 1
This homework assignment consisted of three problems from the questions at the end of chapter 1 of “Introduction to Java Programming 10th Edition” by Y. Daniel Liang. The homework problems are 1.6, 1.9, and 1.12. Each of these problems required the writing of Java code to solve them. This paper will state the problem and discuss the solution to each of them as well as showing the program code and sample output for each solution.

The first problem is 1.6 which involves writing a program to find the summation of a series. The specific series is 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 which has a solution of 45. For the programming solution to this problem I chose to write the program so that it would not limit the user to just the stated series but it allows the user to start the series at any integer value and to also give the desired length of the series. The generic form of the series is:  *(X + (X+1) + (X+2) + .... (X+n-1) + (X+n))*, so the input from the user is the values of X and n. The program first gives the solution to the series specified in the problem statement then the program enters a menu driven loop that allows them to choose the action of the program from that point. I have included a section of comments at the beginning of the program listing below that provides a little more detail about the program.

## Code for Problem 1.6

```java
/**
 * @author Michael Dobrinski
 * COMSC 1033 Section 1411
 * Instructor: Dr. Evert
 * 31 August 2015
 */

/** Homework number 2
 * Problem 1.6 from Chapter 1
 *
 * Summation of a series - Write a program that displays the result of:
 * (X + (X+1) + (X+2) + .... (X+n-1) + (X+n)), where X=1 and n=8
 * for n greater than or equal to zero.
 *
 * Solution: The program is written to be more generic in nature allowing the 
 * user to input values for X and n to see the affect that it has in the series
 * total. X controls the starting point for the series and n controls how long
 * the series will run.
 * The program is menu driven giving the user the options of:
 *  1. Calculating the series with the specified values given in the problem.
 *  2. Calculate the series with values given by the user.
 *  3. End the program.
 * When the program is started it calculates the series with the values given
 * in the problem statement and displays the result and enters a DO-WHILE LOOP
 * which displays the menu that allows the user to determine how the program
 * proceeds from that point. The loop continues until the value of the
 * boolean variable continueProgram is changed from true to false.
 * Inside the DO-WHILE LOOP after the menu is printed the program waits for user
 * input. Once the user makes their selection the program enters a SWITCH 
 * program control statement with three cases corresponding to the menu prompt.
 * Inside case 2 the user is prompted to enter values for both X and n after 
 * which an IF statement is used to check that n is greater than or equal to 
 * zero. If n is valid then the series is calculated and the result is displayed
 * then the program returns to the start of the DO-WHILE LOOP.
 * Case 3 and the default case both cause the program to exit.
 * The program uses two methods:
 *  public static long seriesCalc(int xc, int nc) used to calculate the series
 * and
 *  public static void printMenu() used to display the menu.
 *
 * There is no check to make sure that the series total does not exceed the 
 * range of a long variable nor is there any checks to catch the exception if 
 * the user enters non-integer values for X or n.
 */


import java.util.Scanner;

public class COMSC_1033_HW_2_Chp_1_6 {

	/********************************************************
	 * 				START OF THE MAIN METHOD
	 ********************************************************/
	public static void main(String[] args) {
	int x = 1, n = 8, selection = 0; // declare the variables
	long seriesTotal = 0; // use a long for the total
	boolean continueProgram = true;

	// Tell the user what the program does.
	System.out.println("This program calculates the total for the series"
                + " (X + (X+1) + (X+2) + .... (X+n-1) + (X+n))");
	System.out.println("given X and n. The first time the series is "
                + "calculated it uses X=1 and n=8.\n");

	seriesTotal = seriesCalc(x, n);	// calculate the series for the first 
                                        //time using default values for X and n.

	// Output the results
	System.out.println("The series (X + (X+1) + (X+2) + .... (X+n-1) + "
                + "(X+n)) total is: " + seriesTotal + " for x=" + x
		+ " and n=" + n);

	Scanner input = new Scanner(System.in); // Open an input stream

	do { // This is the start of the program loop that is driven by the menu
			 // displayed by the method printMenu.

		printMenu();

		selection = input.nextInt(); // Get the users menu selection.
		switch (selection) {
		case 1: // Calc the series with the default values x=1 and n=8.
		x = 1; // Set the value for x to the default of 1.
		n = 8; // Set the value for n to the default of 8.
		seriesTotal = seriesCalc(x, n);
		// Output the results
		System.out.println("\nThe series (X + (X+1) + (X+2) + .... "
                        + "(X+n-1) + (X+n)) total is: " + seriesTotal
			+ " for x=" + x + " and n=" + n);
		continueProgram = true;
		break;

		case 2: // Calculate the series with a new x and n.
		System.out.print(
			"Enter new integer values for X and n in the series "
                                + "(X + (X+1) + (X+2) + .... (X+n-1) + (X+n)). "
                                + "(n must be >=0): ");
		x = input.nextInt();
		n = input.nextInt();
		// Test for a valid n (n>=0)
		if (n < 0) {
			System.out.print("\n*** ERROR: n must be greater than "
                                + "or equal to zero (0)! ***\n\n");
			continueProgram = true;
			break; // break out of this case and start the loop
		}
		seriesTotal = seriesCalc(x, n);
		// Output the results
		System.out.println("\nThe series (X + (X+1) + (X+2) + .... "
                        + "(X+n-1) + (X+n)) total is: " + seriesTotal
			+ " for x=" + x + " and n=" + n);
		continueProgram = true;
		break;

		case 3: // Exit the program.
		default: // Exit the program as the default.
		System.out.println("\nThe program has ended.");
		continueProgram = false; // Set the value to exit the program.
		break;
		}
	} while (continueProgram); // This is the end of the menu driven loop.
			// The program ends when continueProgram = false.
	}

	/************************************************************
	 * 				ND OF THE MAIN METHOD
	 ************************************************************/

	/*
	 * Method to calculate the series total for the following series where 
         * n is greater than or equal to zero. series: (X + (X+1) + (X+2) 
         * + .... (X+n-1) + (X+n))
	 *
	 */

	public static long seriesCalc(int xc, int nc) {
	int i;
	long result = 0;

	for (i = 0; i <= nc; i++) {
		result = result + xc + i;
	}
	return result;
	}

	/*
	 * Method to print a selection menu
	 */

	public static void printMenu() {
	System.out.print("\n\n");
	System.out.println("1. Calculate the series with the default values "
                + "x=1 and n=8.");
	System.out.println("2. Calculate the series with a new x and n.");
	System.out.println("3. Exit the program.");
	System.out.print("Select from menu items 1 through 3: ");
	return;
	}

}
```

## Console Output for Problem 1.6

```
This program calculates the total for the series (X + (X+1) + (X+2) + .... (X+n-1) + (X+n))
given X and n. The first time the series is calculated it uses X=1 and n=8.

The series (X + (X+1) + (X+2) + .... (X+n-1) + (X+n)) total is: 45 for x=1 and n=8


1. Calculate the series with the default values x=1 and n=8.
2. Calculate the series with a new x and n.
3. Exit the program.
Select from menu items 1 through 3: 1

The series (X + (X+1) + (X+2) + .... (X+n-1) + (X+n)) total is: 45 for x=1 and n=8


1. Calculate the series with the default values x=1 and n=8.
2. Calculate the series with a new x and n.
3. Exit the program.
Select from menu items 1 through 3: 2
Enter new integer values for X and n in the series (X + (X+1) + (X+2) + .... (X+n-1) + (X+n)). (n must be >=0): 2 5

The series (X + (X+1) + (X+2) + .... (X+n-1) + (X+n)) total is: 27 for x=2 and n=5


1. Calculate the series with the default values x=1 and n=8.
2. Calculate the series with a new x and n.
3. Exit the program.
Select from menu items 1 through 3: 3

The program has ended.

```
When the user chooses to end the program from the menu it prints a simple statement to acknowledge that the program has ended. The program tries to take advantage of the computer by making it easy to change the parameters for the series without having to change the program and then recompile it. The program does do some simple checking and input verification but it could be made better with exception handling or error trapping. Some of the same techniques used in the solution of problem 1.6 were also used in the programs for problems 1.9 and 1.12.

Problem 1.9 is to calculate the perimeter and area of a rectangle given the width and height. Again the problem specified a specific width and height of 4.5 and 7.9 respectively. The program written to solve the problem was made a little more flexible in order to take advantage of the computer without having to modify the program each time the dimensions of the rectangle were changed. Also, the program prompts for the units of measure and displays the results with units. More program details are given in the comments of the program listing below.

## Code for Problem 1.9

```java
/** @author Michael Dobrinski
 * COMSC 1033 Section 1411
 * Instructor: Dr. Evert
 * 01 September 2015
 */

/** Homework number 2
 * Problem 1.9 from Chapter 1
 * (Area and perimeter of a rectangle) Write a program that displays the area and perimeter of a rectangle. The default width is 4.5 and
 * the default height is 7.9.
 * 					AREA = width X height
 * 					PERIMETER = 2 X (width + height)
 *
 * Solution: The program is written to be more generic in nature allowing the user to input
 * values for the width and height of the rectangle as well as units for those measurements.
 * The program is menu driven giving the user the options of:
 * 	1. Calculating the perimeter and area with the specified values given in the problem.
 * 	2. Calculate the perimeter and area with values given by the user.
 * 	3. End the program.
 * When the program is started it prompts the user for the units of the default measurements and then it calculates
 * the perimeter and area with the values given in the problem statement and displays the result.
 * The program then enters a DO-WHILE LOOP which displays the menu that allows the user
 * to determine how the program proceeds from that point. The loop continues until the value of the
 * boolean variable continueProgram is changed from true to false.
 * Inside the DO-WHILE LOOP after the menu is printed the program waits for user input. Once the user
 * makes their selection the program enters a SWITCH program control statement with three cases corresponding
 * to the menu prompt.
 * Inside case 2 the user is prompted to enter values for both width and height of a rectangle as well as the units for those
 * measurements after which an IF statement is used to check that both the width and height measurements are greater than zero.
 * If both the width and height are valid then the perimeter and area are calculated and the result is displayed then the
 * program returns to the start of the DO-WHILE LOOP.
 * Case 3 and the default case both cause the program to exit.
 * The program uses three methods:
 * 		public static double areaCalc (double wc, double hc) - to calculate the ares
 * 		public static double perimeterCalc (double wc, double hc) - to calculate the perimeter
 * 		public static void printMenuRec() - to print the menu at the start of each iteration of the loop.
 *
 * There is no check to make sure that the perimeter or area results do not exceed the range of a double variable nor is
 * there any check to catch the exception if the user enters a non-valid input for the width or height. The string entered for the
 * units variable is not checked to make sure it is valid either.
 */

import java.util.Scanner;		// Get set up to read user input.

public class COMSC_1033_HW_2_Chp_1_9 {


/********************************************************* Start of MAIN method ***********************************************************/
	public static void main(String[] args) {
		boolean continueProgram = true;
		int selection=0;
		double w=4.5d, h=7.9d, area=0, perimeter=0;
		String units;

		Scanner input=new Scanner(System.in);	// Open an input stream.
		// Get the units for the default rectangle measurements.
		System.out.print("\nEnter the units of measure for the rectangle measurements: ");
		units=input.nextLine();

		area=areaCalc(w, h);
		perimeter=perimeterCalc(w, h);

		// Output the results
		System.out.printf("\nThe perimeter of a rectangle that is %1.5f %2s by %1.5f %2s is: %1.5f %2s.", w, units, h, units, perimeter, units);
		System.out.printf("\nThe area of a rectangle that is %1.5f %2s by %1.5f %2s is: %1.5f square %2s.", w, units, h, units, area, units);

		do{			// This is the start of the program loop that is driven by the menu displayed by the method printMenu.

			printMenuRec();

			selection=input.nextInt();				// Get the users menu selection.
			switch(selection){
				case 1:		// Calculate the area and perimeter with the default values for the width and height.
					w=4.5d;	// Set the value for w to the default of 4.5.
					h=7.9d;	// Set the value for h to the default of 7.9.

					area=areaCalc(w, h);
					perimeter=perimeterCalc(w, h);

					input.nextLine();						// Attempt to clear the buffer.

					// Get the units for the default rectangle measurements.
					System.out.print("\nEnter the units of measure for the rectangle measurements: ");
					units=input.nextLine();

					// Output the results. The output is formatted to 5 decimal places.
					System.out.printf("\nThe perimeter of a rectangle that is %1.5f %2s by %1.5f %2s is: %1.5f %2s.", w, units, h, units, perimeter, units);
					System.out.printf("\nThe area of a rectangle that is %1.5f %2s by %1.5f %2s is: %1.5f square %2s.", w, units, h, units, area, units);
					continueProgram=true;
					break;

				case 2:		// Calculate the area and perimeter with a new width and height.

					input.nextLine();						// Attempt to clear the buffer.

					System.out.print("Enter new values for the width and height of the rectangle: ");
					w=input.nextDouble();
					h=input.nextDouble();

					// Test for valid input both w and h must be >=0
					if (w<0 || h<0){
						System.out.print("\n*** ERROR: all measurements must be greater than zero (0)! ***\n\n");
						continueProgram=true;
						break; 				// break out of this case and restart the loop
					}

					input.nextLine();						// Attempt to clear the buffer.

					// Get the units for the default rectangle measurements.
					System.out.print("\nEnter the units of measure for the rectangle measurements: ");
					units=input.nextLine();

					area=areaCalc(w, h);
					perimeter=perimeterCalc(w, h);

					// Output the results
					System.out.printf("\nThe perimeter of a rectangle that is %1.5f %2s by %1.5f %2s is: %1.5f %2s.", w, units, h, units, perimeter, units);
					System.out.printf("\nThe area of a rectangle that is %1.5f %2s by %1.5f %2s is: %1.5f square %2s.", w, units, h, units, area, units);

					continueProgram=true;
					break;

				case 3:		// Exit the program.
				default:	// Exit the program as the default.
					System.out.println("\nThe program has ended.");
					continueProgram=false;		// Set the value to exit the program.
					break;
			}
		}while (continueProgram);	// This is the end of the menu driven loop. The program ends when continueProgram = false.

	}
/********************************************************** End of MAIN method ************************************************************/

	/*
	 *  Method to calculate the perimeter of a rectangle.
	 */
	public static double perimeterCalc (double wc, double hc){
		double result=0;
		result = 2.0d * (wc + hc);
		return result;
	}

	/*
	 *  Method to calculate the area of a rectangle.
	 */

	public static double areaCalc (double wc, double hc){
		double result=0;
		result = wc * hc;
		return result;
	}

	/*
	 *  Method to print a selection menu
	 */

		public static void printMenuRec(){
			System.out.print("\n\n\n");
			System.out.println("1. Calculate the Area and Perimeter of a rectangle with the default values Width=4.5 and Height=7.9.");
			System.out.println("2. Calculate the Area and Perimeter of a rectangle with a new Width and Height.");
			System.out.println("3. Exit the program.");
			System.out.print("Select from menu items 1 through 3: ");
			return;
		}
}
```
## Console Output for Problem 1.9

```
Enter the units of measure for the rectangle measurements: feet

The perimeter of a rectangle that is 4.50000 feet by 7.90000 feet is: 24.80000 feet.
The area of a rectangle that is 4.50000 feet by 7.90000 feet is: 35.55000 square feet.


1. Calculate the Area and Perimeter of a rectangle with the default values Width=4.5 and Height=7.9.
2. Calculate the Area and Perimeter of a rectangle with a new Width and Height.
3. Exit the program.
Select from menu items 1 through 3: 1

Enter the units of measure for the rectangle measurements: inches

The perimeter of a rectangle that is 4.50000 inches by 7.90000 inches is: 24.80000 inches.
The area of a rectangle that is 4.50000 inches by 7.90000 inches is: 35.55000 square inches.


1. Calculate the Area and Perimeter of a rectangle with the default values Width=4.5 and Height=7.9.
2. Calculate the Area and Perimeter of a rectangle with a new Width and Height.
3. Exit the program.
Select from menu items 1 through 3: 2
Enter new values for the width and height of the rectangle: 21.95 543.6

Enter the units of measure for the rectangle measurements: yards

The perimeter of a rectangle that is 21.95000 yards by 543.60000 yards is: 1131.10000 yards.
The area of a rectangle that is 21.95000 yards by 543.60000 yards is: 11932.02000 square yards.


1. Calculate the Area and Perimeter of a rectangle with the default values Width=4.5 and Height=7.9.
2. Calculate the Area and Perimeter of a rectangle with a new Width and Height.
3. Exit the program.
Select from menu items 1 through 3: 3

The program has ended.
```
The program prints a simple message to indicate that it has ended. The user input is checked to make sure that it is greater than zero but there is no error trapping or exception handling in the program. Also, the input for the units variable is not checked so it is depending on the user to give sensible input. The final problem is 1.12.

Problem 1.12 is to calculate the average speed to run a race given the distance of the race in miles and the time it takes to finish the race in hours, minutes, and seconds. The average speed is to be output in kilometers per hour and the stated conversion factor of 1.6 kilometers per mile is to be used. The program has much of the same format as the previous two programs with a menu given so the user can run the program with the default values given in the problem statement or with user supplied values. The program listing and sample output are given below with more program details in the comments of the program.

## Code for Problem 1.12

```java
/**
 * @author Michael Dobrinski
 * COMSC 1033 Section 1411
 * Instructor: Dr. Evert
 * 01 September 2015
 */

/** Homework number 2
 * Problem 1.12 from Chapter 1
 * (Average speed in kilometers per hour) Write a program that displays the average speed of a runner in kilometers per hour (kph).
 * 	Inputs: Distance of race
 * 			Time in hours, minutes, seconds to run the race.
 *
 * Methods used:
 * 		public static double calcTime( int tH, int tM, int tS)	- returns the time in decimal hours.
 * 		public static double calcAvgSpeed(double dist, double decH) - calculate the average speed in distance units per hour.
 * 		public static void printMenuSpeed()
 *
 * Solution: The program is written to be more generic in nature allowing the user to input
 * values for the distance of the race and for the finish time.
 * The program is menu driven giving the user the options of:
 * 	1. Calculating the average speed with the specified values given in the problem.
 * 	2. Calculate the average speed with values given by the user.
 * 	3. End the program.
 * When the program is started it calculates the average speed with the default distance and time.
 * The program then enters a DO-WHILE LOOP which displays the menu that allows the user
 * to determine how the program proceeds from that point. The loop continues until the value of the
 * boolean variable continueProgram is changed from true to false.
 * Inside the DO-WHILE LOOP after the menu is printed the program waits for user input. Once the user
 * makes their selection the program enters a SWITCH program control statement with three cases corresponding
 * to the menu prompt.
 * Inside case 2 the user is prompted to enter values for both distance and time. The time is entered using separate prompts
 * for hours, minutes and seconds after which the all of the entries are checked to make sure they are greater than zero.
 * If all of the entries are valid then the average speed is calculated and the result is displayed then the
 * program returns to the start of the DO-WHILE LOOP.
 * Case 3 and the default case both cause the program to exit.
 *
 * The input is for the distance is in miles and the conversion to kilometers is made in the output statement by
 * multiplying the average speed by 1.6.
 *
 * There is no exception handling in this program so if the user enters the wrong type for the variable the
 * program halts.
 */
import java.util.Scanner;		// Get setup to read user input.

public class COMSC_1033_HW_2_Chp_1_12 {



/**************************************************** Start of MAIN method ******************************************************/
	public static void main(String[] args) {
		boolean continueProgram = true;
		int selection, tHours=0, tMinutes=0, tSeconds=0;
		double distance=0, decHours=0, avgSpeed=0;

	Scanner input=new Scanner(System.in);

	distance=24.0; 	// default distance in miles
	tHours=1;		// default time - hours
	tMinutes=40;	// default time - minutes
	tSeconds=35;	// default time - seconds

	decHours=calcTime( tHours, tMinutes, tSeconds);
	avgSpeed=calcAvgSpeed(distance, decHours);


	// Output the results
	System.out.printf("\nThe average speed is %1.5f kilometers per hour for a %1.3f mile race run in a time of %d:%d:%d (hh:mm:ss).", +
			avgSpeed*1.6, distance, tHours, tMinutes, tSeconds);


		do{			// This is the start of the program loop that is driven by the menu displayed by the method printMenu.

			printMenuSpeed();

			selection=input.nextInt();				// Get the users menu selection.
			switch(selection){
				case 1:		// Calculate the average speed with the default values for distance and time.
					distance=24.0; 	// default distance in miles
					tHours=1;		// default time - hours
					tMinutes=40;	// default time - minutes
					tSeconds=35;	// default time - seconds

					decHours=calcTime( tHours, tMinutes, tSeconds);
					avgSpeed=calcAvgSpeed(distance, decHours);

					// Output the results
					System.out.printf("\nThe average speed is %1.5f kilometers per hour for a %1.3f mile race run in a time of %d:%d:%d (hh:mm:ss).", +
							avgSpeed*1.6, distance, tHours, tMinutes, tSeconds);

					continueProgram=true;
					break;

				case 2:		// Calculate the average speed using a new distance and time.

					input.nextLine();						// Attempt to clear the buffer.

					System.out.print("Enter the distance of the race in miles: ");
					distance=input.nextDouble();

					input.nextLine();						// Attempt to clear the buffer.
					System.out.print("Enter the time - number of hours (integer): ");
					tHours=input.nextInt();

					input.nextLine();						// Attempt to clear the buffer.
					System.out.print("Enter the time - number of minutes (integer): ");
					tMinutes=input.nextInt();

					input.nextLine();						// Attempt to clear the buffer.
					System.out.print("Enter the time - number of seconds (integer): ");
					tSeconds=input.nextInt();


					// Test for valid input, distance and time must be positive.
					if (distance<0 || tHours<0 || tMinutes<0 || tSeconds<0){
						System.out.print("\n*** ERROR: All times and distances must be positive! ***\n\n");
						continueProgram=true;
						break; 				// break out of this case and restart the loop
					}

					decHours=calcTime( tHours, tMinutes, tSeconds);
				// Test to make sure the time is not equal to zero.
					if (decHours == 0){
						System.out.print("\n*** ERROR: The time cannot be zero! ***\n\n");
						continueProgram=true;
						break; 				// break out of this case and restart the loop
					}
					avgSpeed=calcAvgSpeed(distance, decHours);

					// Output the results
					System.out.printf("\nThe average speed is %1.5f kilometers per hour for a %1.3f mile race run in a time of %d:%d:%d (hh:mm:ss).", +
							avgSpeed*1.6, distance, tHours, tMinutes, tSeconds);

					continueProgram=true;
					break;

				case 3:		// Exit the program.
				default:	// Exit the program as the default.
					System.out.println("\nThe program has ended.");
					continueProgram=false;		// Set the value to exit the program.
					break;
			}
		}while (continueProgram);	// This is the end of the menu driven loop. The program ends when continueProgram = false.

	}
/***************************************************** End of MAIN method *******************************************************/

	/*
	 *  Method to calculate the average speed in distance units per hour.
	 */

	public static double calcAvgSpeed(double dist, double decH){
		double result=0;
		result=dist/decH;
		return result;
	}

	/*
	 *  Method to calculate the time in decimal hours.
	 */

	public static double calcTime( int tH, int tM, int tS){
		double result=0;
		result = tH/1.0 + tM/60.0 + tS/3600.0;
		return result;
	}

	/*
	 *  Method to print a selection menu
	 */

		public static void printMenuSpeed(){
			System.out.print("\n\n\n**********************************************************************************************\n");
			System.out.println("1. Calculate the average speed for the default distance of 24 miles and time of 1:40:35");
			System.out.println("2. Calculate the average speed for new distance and time.");
			System.out.println("3. Exit the program.");
			System.out.print("Select from menu items 1 through 3: ");
			return;
		}
}
```

## Console Output for Problem 1.12

```
The average speed is 22.90638 kilometers per hour for a 24.000 mile race run in a time of 1:40:35 (hh:mm:ss).


**********************************************************************************************
1. Calculate the average speed for the default distance of 24 miles and time of 1:40:35
2. Calculate the average speed for new distance and time.
3. Exit the program.
Select from menu items 1 through 3: 1

The average speed is 22.90638 kilometers per hour for a 24.000 mile race run in a time of 1:40:35 (hh:mm:ss).


**********************************************************************************************
1. Calculate the average speed for the default distance of 24 miles and time of 1:40:35
2. Calculate the average speed for new distance and time.
3. Exit the program.
Select from menu items 1 through 3: 2
Enter the distance of the race in miles: 26.5
Enter the time - number of hours (integer): 1
Enter the time - number of minutes (integer): 21
Enter the time - number of seconds (integer): 45

The average speed is 31.11927 kilometers per hour for a 26.500 mile race run in a time of 1:21:45 (hh:mm:ss).


**********************************************************************************************
1. Calculate the average speed for the default distance of 24 miles and time of 1:40:35
2. Calculate the average speed for new distance and time.
3. Exit the program.
Select from menu items 1 through 3: 3

The program has ended.
```

## Summary
There is minimal error checking done in the program with only the input being checked to make sure that the distances and times are positive and that the time does not equal zero.

I know these programs are much longer than needed but I tried to add some features mentioned above to make the programs more usable.
