# EXPENSE-TRACKER-APPLICATION
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;

public class ExpenseTracker {
    private JFrame frame;
    private JTextField amountField;
    private JTextField categoryField;
    private JTextArea expenseList;
    private ArrayList<Expense> expenses;

    // Constructor for initializing the GUI
    public ExpenseTracker() {
        expenses = new ArrayList<>();
        frame = new JFrame("Expense Tracker");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 400);
        frame.setLayout(new FlowLayout());

        // Set up the labels, text fields, and buttons
        JLabel amountLabel = new JLabel("Amount:");
        amountField = new JTextField(10);
        JLabel categoryLabel = new JLabel("Category:");
        categoryField = new JTextField(10);
        JButton addButton = new JButton("Add Expense");
        expenseList = new JTextArea(10, 30);
        expenseList.setEditable(false);

        // Action listener for the "Add Expense" button
        addButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                addExpense(); // Calls addExpense method when button is pressed
            }
        });

        // Add components to the frame
        frame.add(amountLabel);
        frame.add(amountField);
        frame.add(categoryLabel);
        frame.add(categoryField);
        frame.add(addButton);
        frame.add(new JScrollPane(expenseList));

        // Make the frame visible
        frame.setVisible(true);
    }

    // Method to add expense when the button is pressed
    private void addExpense() {
        String amountText = amountField.getText();
        String categoryText = categoryField.getText();
        
        // Validate input and add expense if valid
        if (!amountText.isEmpty() && !categoryText.isEmpty()) {
            try {
                double amount = Double.parseDouble(amountText); // Convert amount to double
                expenses.add(new Expense(amount, categoryText)); // Add expense to the list
                updateExpenseList(); // Update the list of expenses displayed
                amountField.setText(""); // Clear the input fields
                categoryField.setText("");
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(frame, "Please enter a valid amount.");
            }
        } else {
            JOptionPane.showMessageDialog(frame, "Please enter both amount and category.");
        }
    }

    // Method to update the expense list in the JTextArea
    private void updateExpenseList() {
        StringBuilder list = new StringBuilder();
        for (Expense expense : expenses) {
            list.append(expense.toString()).append("\n");
        }
        expenseList.setText(list.toString()); // Update the text area with the expenses
    }

    // Main method to run the ExpenseTracker application
    public static void main(String[] args) {
        new ExpenseTracker(); // Create a new ExpenseTracker object, which launches the GUI
    }
}

// Expense class to store expense details (amount and category)
class Expense {
    private double amount;
    private String category;

    // Constructor to initialize Expense object
    public Expense(double amount, String category) {
        this.amount = amount;
        this.category = category;
    }

    // Override toString method to format the expense as a string
    @Override
    public String toString() {
        return "Amount: $" + amount + ", Category: " + category;
    }
}
