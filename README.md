# Java-Calculator-with-History
A calculator that takes the input from the user (what operation to perform, what numbers to work with and what he wants to do after each operation (history, etc.))

##  Main.java file

In our Main.java file we create an instance of the class that I have initialized as InputHandler and call our *start* method which as the method's name suggests, we start our program. Our whole program is written in our InputHandler class.

## InputHandler.java file

In this file, is where all the fun and all the code is. First off, we import our libraries that we will be using. In this case, we will be using vectors and user input, therefore `import java.util.Scanner;` and `import java.util.Vector;`

In the next few lines, we initialize our variables that we will be using:
```
private Scanner userInput = new Scanner(System.in);
private boolean keepOn = true;
private String yesOrNo;
public Vector<Double> calculations = new Vector<>();
```

Let's see what each variable will be for. 

Our first variable `private Scanner userInput = new Scanner(System.in);` will be our, you gussed it, user input variable. First we make it *private*, so it can't be accessed directly to other instances of our InputHandler class. This variable is **encapsulated**. Even if you do not want it necessarily private, it is always a good practice making it so. 

Our second variable `private boolean keepOn = true` will be a variable that will keep the looping going on until the user decides to exit the program. When the exit choice has been activated, keepOn's value will be false, therefore breaking the main loop. We will see that later in the code. Again, this variable is **encapsulated**.

The third variable will keep track of whether the user has chosen to perform another operation, to choose to show the history of the operations that have been performed, or to simply exit the program. Again, we will see that later in the documentation. Once again, it has been **encapsulated**, just for a good practice.

Then finally, our fourth variable `public Vector<Double> calculations = new Vector<>();` will be our vector that will store the results that we will later show as a *history*. We choose to use vector here, because it is more effiecient and it is easier since Java gives us the  option to use the **addElement()** method. 

The next couple of lines are: 

```
public void start() {
    System.out.println("Welcome to my calculator!");
    while(keepOn == true) {
        calculate();
    }
}
```
This basically says: "Hey, start the calculator with a message 'Welcome to my calculator!' and keep calculating until the user hasn't chosen to exit from our program.". The **calculate()** method we are using here has not yet been intialized, but we will initialize it soon enough.

