# banking-account-management-system
creating account
#include <stdio.h>
#include <string.h>

#define MAX_ACCOUNTS 100

// Define the Account structure
struct Account {
    int accountNumber;
    char name[100];
    float balance;
};

// Global array to store accounts
struct Account accounts[MAX_ACCOUNTS];
int totalAccounts = 0;

// Function declarations
void createAccount();
void displayAccount();
void depositMoney();
void withdrawMoney();

int main() {
    int choice;

    while (1) {
        printf("\n--- Banking Account Management System ---\n");
        printf("1. Create Account\n");
        printf("2. Display Account\n");
        printf("3. Deposit Money\n");
        printf("4. Withdraw Money\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: createAccount(); break;
            case 2: displayAccount(); break;
            case 3: depositMoney(); break;
            case 4: withdrawMoney(); break;
            case 5: return 0;
            default: printf("Invalid choice!\n");
        }
    }

    return 0;
}

void createAccount() {
    if (totalAccounts >= MAX_ACCOUNTS) {
        printf("Cannot create more accounts.\n");
        return;
    }

    printf("Enter account number: ");
    scanf("%d", &accounts[totalAccounts].accountNumber);
    printf("Enter account holder name: ");
    getchar(); // Clear newline character
    fgets(accounts[totalAccounts].name, 100, stdin);
    accounts[totalAccounts].name[strcspn(accounts[totalAccounts].name, "\n")] = '\0'; // Remove newline
    accounts[totalAccounts].balance = 0.0;

    totalAccounts++;
    printf("Account created successfully.\n");
}

void displayAccount() {
    int accNo, found = 0;
    printf("Enter account number: ");
    scanf("%d", &accNo);

    for (int i = 0; i < totalAccounts; i++) {
        if (accounts[i].accountNumber == accNo) {
            printf("Account Number: %d\n", accounts[i].accountNumber);
            printf("Account Holder: %s\n", accounts[i].name);
            printf("Balance: %.2f\n", accounts[i].balance);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Account not found.\n");
    }
}

void depositMoney() {
    int accNo;
    float amount;
    printf("Enter account number: ");
    scanf("%d", &accNo);

    for (int i = 0; i < totalAccounts; i++) {
        if (accounts[i].accountNumber == accNo) {
            printf("Enter amount to deposit: ");
            scanf("%f", &amount);
            if (amount > 0) {
                accounts[i].balance += amount;
                printf("Amount deposited successfully.\n");
            } else {
                printf("Invalid amount.\n");
            }
            return;
        }
    }

    printf("Account not found.\n");
}

void withdrawMoney() {
    int accNo;
    float amount;
    printf("Enter account number: ");
    scanf("%d", &accNo);

    for (int i = 0; i < totalAccounts; i++) {
        if (accounts[i].accountNumber == accNo) {
            printf("Enter amount to withdraw: ");
            scanf("%f", &amount);
            if (amount > 0 && accounts[i].balance >= amount) {
                accounts[i].balance -= amount;
                printf("Amount withdrawn successfully.\n");
            } else {
                printf("Insufficient balance or invalid amount.\n");
            }
            return;
        }
    }

    printf("Account not found.\n");
}

