#include <stdio.h>
#include <string.h>

typedef struct {
    char ownerName[50];
    char dateOfRegistration[20];
    char vehicleModel[20];
    int numWheels;
    float fare;
} Vehicle;

void displayFareDetails() {
    printf("Fare details:\n");
    printf("1. 2-wheeler: Rs. 30\n");
    printf("2. 4-wheeler: Rs. 60\n");
    printf("3. 6-wheeler: Rs. 90\n");
    printf("4. 8-wheeler: Rs. 120\n");
}


void updateBasicFare(Vehicle *vehicles, int numVehicles) {
    for (int i = 0; i < numVehicles; i++) {
        if (vehicles[i].numWheels == 2) {
            vehicles[i].fare = 30;
        } else if (vehicles[i].numWheels == 4) {
            vehicles[i].fare = 60;
        } else if (vehicles[i].numWheels == 6) {
            vehicles[i].fare = 90;
        } else if (vehicles[i].numWheels == 8) {
            vehicles[i].fare = 120;
        }
    }
    printf("Basic fare updated for all vehicles.\n");
}
void recordDailyTrafficDetails(Vehicle *vehicles, int *numVehicles) {
    printf("Enter owner's name: ");
    scanf("%s", vehicles[*numVehicles].ownerName);
    printf("Enter date of registration: ");
    scanf("%s", vehicles[*numVehicles].dateOfRegistration);
    printf("Enter vehicle model: ");
    scanf("%s", vehicles[*numVehicles].vehicleModel);
    printf("Enter number of wheels: ");
    scanf("%d", &vehicles[*numVehicles].numWheels);
    (*numVehicles)++;
    printf("Vehicle record added.\n");
}
void deleteVehicleRecord(Vehicle *vehicles, int *numVehicles, char ownerName[50]) {
    int found = 0;
    for (int i = 0; i < *numVehicles; i++) {
        if (strcmp(vehicles[i].ownerName, ownerName) == 0) {
            for (int j = i; j < *numVehicles - 1; j++) {
                vehicles[j] = vehicles[j + 1];
            }
            (*numVehicles)--;
            found = 1;
            printf("Vehicle record deleted.\n");
            break;
        }
    }
    if (!found) {
        printf("Vehicle record not found.\n");
    }
}
void searchVehicleRecord(Vehicle *vehicles, int numVehicles, char ownerName[50])
{
int found = 0;
for (int i = 0; i < numVehicles; i++) {
if (strcmp(vehicles[i].ownerName, ownerName) == 0) {
printf("Owner's name: %s\n", vehicles[i].ownerName);
printf("Date of registration: %s\n", vehicles[i].dateOfRegistration);
printf("Vehicle model: %s\n", vehicles[i].vehicleModel);
printf("Number of wheels: %d\n", vehicles[i].numWheels);
printf("Fare: Rs. %.2f\n", vehicles[i].fare);
found = 1;
break;
}
}
if (!found) {
printf("Vehicle record not found.\n");
}
}
int main() {
Vehicle vehicles[100];
int numVehicles = 0;
int choice;
char ownerName[50];

do {
    printf("\nToll Plaza Management System\n");
    printf("1. Display fare details\n");
    printf("2. Update basic fare\n");
    printf("3. Record daily traffic details\n");
    printf("4. Delete vehicle record\n");
    printf("5. Search vehicle record\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            displayFareDetails();
            break;
        case 2:
            updateBasicFare(vehicles, numVehicles);
            break;
        case 3:
            recordDailyTrafficDetails(vehicles, &numVehicles);
            break;
        case 4:
            printf("Enter owner's name to delete: ");
            scanf("%s", ownerName);
            deleteVehicleRecord(vehicles, &numVehicles, ownerName);
            break;
        case 5:
            printf("Enter owner's name to search: ");
            scanf("%s", ownerName);
            searchVehicleRecord(vehicles, numVehicles, ownerName);
            break;
    }
} while (choice != 5);

return 0;
}
