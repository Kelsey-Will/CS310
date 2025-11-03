# CS310
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

class bankAccount {
private:
    string holderName;
    int accountNumber;
    string accountType;
    double balance;
    double interestRate;

    static int nextAccountNumber;

public:
    // Default constructor
    bankAccount() {
        holderName = "";
        accountType = "checking";
        balance = 0.0;
        interestRate = 0.0;
        accountNumber = nextAccountNumber++;
    }

    // Parameterized constructor
    bankAccount(string name, string type, double initialBalance, double rate) {
        holderName = name;
        accountType = type;
        balance = initialBalance;
        interestRate = rate;
        accountNumber = nextAccountNumber++;
    }

    // Member functions
    void deposit(double amount) {
        if (amount > 0)
            balance += amount;
    }

    void withdraw(double amount) {
        if (amount > 0 && amount <= balance)
            balance -= amount;
        else
            cout << "Insufficient funds or invalid amount.\n";
    }

    void addInterest() {
        balance += balance * interestRate;
    }

    double getBalance() const {
        return balance;
    }

    void display() const {
        cout << fixed << setprecision(2);
        cout << "Account #" << accountNumber << " | "
             << "Name: " << holderName << " | "
             << "Type: " << accountType << " | "
             << "Balance: $" << balance << " | "
             << "Interest Rate: " << interestRate * 100 << "%\n";
    }
};

// Initialize static member
int bankAccount::nextAccountNumber = 1001;

int main() {
    const int SIZE = 10;
    bankAccount customers[SIZE] = {
        bankAccount("Malik Johnson", "checking", 1345.75, 0.021),
        bankAccount("Aaliyah Brooks", "saving", 2980.00, 0.035),
        bankAccount("DeShawn Carter", "checking", 875.60, 0.018),
        bankAccount("Imani Robinson", "saving", 4105.25, 0.04),
        bankAccount("Tyrone Mitchell", "checking", 1120.00, 0.015),
        bankAccount("Nia Washington", "saving", 3275.90, 0.03),
        bankAccount("Jamal Harris", "checking", 960.45, 0.02),
        bankAccount("Zuri Thompson", "saving", 3895.80, 0.038),
        bankAccount("Keisha Moore", "checking", 745.00, 0.012),
        bankAccount("Darius Green", "saving", 5210.10, 0.045)
    };

    // Reset balance of first account to 222.00 using withdraw + deposit
    double currentBalance = customers[0].getBalance();
    customers[0].withdraw(currentBalance);
    customers[0].deposit(222.00);

    // Simulate some transactions
    customers[1].deposit(500);
    customers[2].withdraw(200);
    customers[3].addInterest();

    // Display all accounts
    cout << "=== Bank Account Summary ===\n";
    for (int i = 0; i < SIZE; ++i) {
        customers[i].display();
    }

    return 0;
}
