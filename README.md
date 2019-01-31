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

After starting our program, we ask the user what operation he wants our calculator to perform (*addition, multiplication, subtraction, division*). Then we are return what the user has given us so we can store the value later on to a local variable which we will be able to manipulate.

```
public String chooseOperator() {
    System.out.println("What to do?" +
            "\n + for add" +
            "\n - for minus" +
            "\n * for multiply" +
            "\n / for divide");

    String operator = userInput.next();
    
    return operator;
}
```

After asking the user for what operation he wants to perform, the next thing we do is creating `getFirstNumber()` and `getSecondNumber()` methods. What these methods do, is basically asking the user to input his first and second number and then we are returning this particular value so we can assign it to a variable which will help us to manipulate this value later on.

```
public double getFirstNumber() {
    System.out.println("Input the 1st number");
    return userInput.nextDouble();
}

public double getSecondNumber() {
    System.out.println("Input the 2nd number");
    return userInput.nextDouble();
}
```

After this, we are creating all of the operations our Calculator will be performing -- *addition, multiplication, subtraction, division*. 

```
public void addition(double a, double b){
    calculations.addElement(a + b);
    System.out.println("The Num is: " + (a + b));
}

public void division(double a, double b){
    calculations.addElement(a / b);
    System.out.println("The Num is: " + (a / b));
}

public void mult(double a, double b){
    calculations.addElement(a * b);
    System.out.println("The Num is: " + (a * b));
}

public void sub(double a, double b){
    calculations.addElement(a - b);
    System.out.println("The Num is: " + (a - b));
}
```
Each method will take 2 parameters. These parameters will be the values that the user has chosen. We will see how to do it later in our `calculate()` method later in the program. But what essentially these methods do is just take 2 numbers adding the result from them to our vector `calculations` and then just printing the result. 

The following method `showMenu()` will show us the menu that will be displayed after the user has performed an operation. It will ask the user whether he wants to perform another operation, to load the history, or to exit the program. If the user has given **1** then we will invoke our `calculate()` method which will ask the user for the two numbers and then give the result and add the result to our vector. If he has given us **3**, then in that case we will make our `keepOn` variable to `false` because that way we will stop our `start()` method which means our program will stop. We are also calling `exitMessage()` method that we will initialize shortly. And finally, if the user has given us **2**, that means he wants us to show his history of results he has gotten so far. So we call our function `loadHistory()`, which we will initialize shortly. 

```
 public void showMenu() {
    int z = 0;
    while (z != 1){ 
      System.out.println("Please press the corresponding number for the operation you wish to perform.");
      System.out.println("1. Another operation?");
      System.out.println("2. History?");
      System.out.println("3. Exit?");

      yesOrNo = userInput.next();

      if(yesOrNo.equals("1")) {
        z = 1;
        calculate();
      }
      else if (yesOrNo.equals("3")) {
        z = 1;
        keepOn = false;
        exitMessage();
      }
      else if (yesOrNo.equals("2")){
        loadHistory();
      }
    }
}
```

The next method we create, is called `loadHistory()`. It prints a message and then we are looping through our vector printing each item in it. Remember, the items in our vector are the results that the user has gotten from his operations he has done so far.

```
public void loadHistory() {
    System.out.println("Here are the calculations you have done so far: ");

    for (int i = 0; i < calculations.size(); i++){
      System.out.println(calculations.get(i));
    }
  }
```

The next one is the exit message we want to execute if the user has given us **3**. We quickly give him the operations he has done so far (*just a preference*) and display a *thank you* message. 

```
public void exitMessage() {
    loadHistory();
    
    System.out.println("Thank you for using our program! Hope you enjoyed the experience!");
}
```

And then finally, our last and maybe in fact most important method -- `calculate()`. Okay, here in this method we are basically combining all of the upper methods we have created. Firstly, we initialize 2 variables that we will be used for looping purposes. Then we initialize a **string** variable that will hold the operation that the user has chosen. 

We are asking the user to choose an operation by calling the `chooseOperator()` method (*look it up upper in this documentation for clarification*). After that, we have a couple of if statements that check what the operation the user has chosen. Based on his chosen operation, we get the numbers he wants (*look `getFirstNumber()` and `getSecondNumber()` for clarification*), perform the corresponding operation by calling the corresponding method (`addition()`, `sub()`, `division()` or `mult()`) and then finally we make x = 1 to end the asking for operation loop. Then after the operation has been performed successfully (or in other words `x = 1`), we call our method `showMenu()`. 

```
public void calculate() {
    int x = 0; 
    int y = 0; 
    String operation;
    
    while (x < 1) {
      operation = chooseOperator();
      if(operation.equals("+")){
        double num1 = getFirstNumber();
        double num2 = getSecondNumber();
        addition(num1, num2);
        x = 1;
      }
      else if (operation.equals("-")) {
        double num1 = getFirstNumber();
        double num2 = getSecondNumber();
        sub(num1, num2);
        x = 1;
      }
      else if (operation.equals("/")) {
        double num1 = getFirstNumber();
        double num2 = getSecondNumber();
        division(num1, num2);
        x = 1;
      }
      // aint working have to do fix it
    else if (operation.equals("*")) {
      double num1 = getFirstNumber();
      double num2 = getSecondNumber();
      mult(num1, num2);
      x = 1;
    } // end of multiplication 
  }
    if (x == 1) {
      showMenu();
    }
} 
```

# THANK YOU! :punch:
