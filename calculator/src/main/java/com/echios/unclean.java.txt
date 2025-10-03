package com.echios;
import com.echios.calculator.Calculator; // Import the Calculator class

public class App 
{
    public static void main( String[] args )
    {
        System.out.println( "Module test 2" );

        // Use the Calculator class
        // Calculator calc = new Calculator();
        // double result = calc.add(5, 3);
        double result;

        result = compute(5, 3, "+");
        System.out.println("The result of 5 + 3 is: " + result);

        // double difference = calc.subtract(10, 4);
        result = compute(10, 4, "-");
        System.out.println("10 - 4 = " + result);
    }

    public static double compute(double n1, double n2, String op) {
        Calculator calc = new Calculator();
        double result = 0;

        System.out.println("Started compute");

        if (op.equals("+")) {
            result = calc.add(n1, n2);
        } else if (op.equals("-")) {
            result = calc.subtract(n1, n2);
        }

        System.out.println("result is: " + result);

        return result;
    }

}
