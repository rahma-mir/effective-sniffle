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
