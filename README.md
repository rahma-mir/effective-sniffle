# effective-sniffle
Banking application 
public class BankAccount {
    private int accountNumber;
    private int pin;
    private String name;
    private double currentBalance;

    public BankAccount(int accountNumber, int pin, String name, double initialBalance) {
        this.accountNumber = accountNumber;
        this.pin = pin;
        this.name = name;
        this.currentBalance = initialBalance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            currentBalance += amount;
            System.out.println("Deposited: $" + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= currentBalance) {
            currentBalance -= amount;
            System.out.println("Withdrew: $" + amount);
            return true;
        } else {
            System.out.println("Insufficient funds or invalid amount.");
            return false;
        }
    }

    public void checkBalance() {
        System.out.println("Current Balance: $" + currentBalance);
    }

    public boolean validatePin(int inputPin) {
        return this.pin == inputPin;
    }

    public int getAccountNumber() {
        return accountNumber;
    }

    public String getName() {
        return name;
    }
}

import java.util.ArrayList;
import java.util.List;

public class Bank {
    private List<BankAccount> accounts;

    public Bank() {
        accounts = new ArrayList<>();
        // Creating 3 sample accounts
        accounts.add(new BankAccount(101, 1234, "Alice", 500.0));
        accounts.add(new BankAccount(102, 5678, "Bob", 300.0));
        accounts.add(new BankAccount(103, 9101, "Charlie", 700.0));
    }

    public BankAccount findAccount(int accountNumber, int pin) {
        for (BankAccount account : accounts) {
            if (account.getAccountNumber() == accountNumber && account.validatePin(pin)) {
                return account;
            }
        }
        return null;
    }
    
    public void performTransaction(BankAccount account) {
        java.util.Scanner scanner = new java.util.Scanner(System.in);
        boolean continueTransaction = true;

        while (continueTransaction) {
            System.out.println("Choose an option: 1. Check Balance 2. Deposit 3. Withdraw 4. Exit");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    account.checkBalance();
                    break;
                case 2:
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    account.deposit(depositAmount);
                    break;
                case 3:
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    account.withdraw(withdrawAmount);
                    break;
                case 4:
                    continueTransaction = false;
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Bank bank = new Bank();

        System.out.println("Welcome to the Banking Application!");
        System.out.print("Enter Account Number: ");
        int accountNumber = scanner.nextInt();
        System.out.print("Enter PIN: ");
        int pin = scanner.nextInt();

        BankAccount account = bank.findAccount(accountNumber, pin);
        if (account != null) {
            System.out.println("Login successful! Welcome, " + account.getName());
            bank.performTransaction(account);
        } else {
            System.out.println("Invalid account number or PIN. Please try again.");
        }

        scanner.close();
    }
}

