# car_management_system
#include <stdio.h>
#include <string.h>

#define MAX_CARS 100

// Structure to store car information
struct Car {
    char model[50];
    char brand[50];
    float price;
};

// Global array of cars and a counter for the number of cars
struct Car cars[MAX_CARS];
int carCount = 0;

// Function prototypes
void addCar();
void showCars();
void deleteCar();
void menu();

int main() {
    int choice;
    while (1) {
        menu();
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addCar();
                break;
            case 2:
                showCars();
                break;
            case 3:
                deleteCar();
                break;
            case 4:
                printf("Exiting program...\n");
                return 0;
            default:
                printf("Invalid choice, please try again.\n");
        }
    }
    return 0;
}

// Function to display the menu options
void menu() {
    printf("\n--- Car Management System ---\n");
    printf("1. Enter Car Details\n");
    printf("2. Show All Car Records\n");
    printf("3. Delete Car Record\n");
    printf("4. Exit\n");
}

// Function to add a car's details
void addCar() {
    if (carCount < MAX_CARS) {
        // Read car model
        printf("\nEnter car model (single word): ");
        scanf("%49s", cars[carCount].model);  // Read model name without spaces

        // Read car brand
        printf("Enter car brand (single word): ");
        scanf("%49s", cars[carCount].brand);  // Read brand name without spaces

        // Read car price
        printf("Enter car price: ");
        scanf("%f", &cars[carCount].price);

        carCount++;
        printf("\nCar added successfully!\n");
    } else {
        printf("Car database is full, cannot add more cars.\n");
    }
}

// Function to show all car records
void showCars() {
    if (carCount == 0) {
        printf("\nNo car records available.\n");
    } else {
        printf("\n--- Car Records ---\n");
        for (int i = 0; i < carCount; i++) {
            printf("\nCar %d:\n", i + 1);
            printf("Model: %s\n", cars[i].model);
            printf("Brand: %s\n", cars[i].brand);
            printf("Price: %.2f\n", cars[i].price);
        }
    }
}

// Function to delete a car record
void deleteCar() {
    int index;
    if (carCount == 0) {
        printf("\nNo car records available to delete.\n");
        return;
    }

    printf("\nEnter the index of the car to delete (1 to %d): ", carCount);
    scanf("%d", &index);

    // Validate index
    if (index < 1 || index > carCount) {
        printf("Invalid index. No car deleted.\n");
    } else {
        // Shift the elements to the left to delete the car
        for (int i = index - 1; i < carCount - 1; i++) {
            cars[i] = cars[i + 1];
        }
        carCount--;
        printf("\nCar record deleted successfully!\n");
    }
}

