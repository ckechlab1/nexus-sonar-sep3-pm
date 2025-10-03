package com.echios;

import java.util.logging.Level;
import java.util.logging.Logger;

import com.echios.calculator.Calculator;

public class App {

    private static final Logger LOGGER = Logger.getLogger(App.class.getName());

    public static void main(String[] args) {

        double result;

        result = compute(5, 3, "+");
        LOGGER.log(Level.INFO, "Module test-v9: {0}", result);

        result = compute(10, 4, "-");
        LOGGER.log(Level.INFO, "Module test-v9: {0}", result);

    }

    public static double compute(double n1, double n2, String op) {
        Calculator calc = new Calculator();
        double result = 0;

        if (op.equals("+")) {
            result = calc.add(n1, n2);
        } else if (op.equals("-")) {
            result = calc.subtract(n1, n2);
        }

        return result;
    }

}
