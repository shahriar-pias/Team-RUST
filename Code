## Ghotsts of the Void
---

## *Code:*

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NAME_LEN 50
#define MAX_DESC_LEN 300

// Structure to hold equipment data
typedef struct {
    char name[MAX_NAME_LEN];
    char celestialBody[20]; // "Mars" or "Moon"
    char arrival[MAX_DESC_LEN];
    char importance[MAX_DESC_LEN];
    char discoveries[MAX_DESC_LEN];
} Equipment;

// Function prototypes
void displayWelcomeBanner();
void exploreEquipment(Equipment *eqList, int count);
void addNewEquipment(const char *filename);
int loadEquipmentFromFile(const char *filename, Equipment *eqList, int maxItems);
void saveEquipmentToFile(const char *filename, Equipment *eq, int count);

int main() {
    const char *dataFile = "ghosts_data.txt";
    Equipment equipmentDatabase[20];
    int itemCount = loadEquipmentFromFile(dataFile, equipmentDatabase, 20);

    // Seed default data if database is empty
    if (itemCount == 0) {
        strcpy(equipmentDatabase[0].name, "Spirit Rover");
        strcpy(equipmentDatabase[0].celestialBody, "Mars");
        strcpy(equipmentDatabase[0].arrival, "Landed on Mars on January 4, 2004 (UTC) via parachute and airbag landing system.");
        strcpy(equipmentDatabase[0].importance, "Paved the way for modern long-range Martian surface exploration and robotic geology.");
        strcpy(equipmentDatabase[0].discoveries, "Proved that Mars once had a watery past by discovering mineral evidence of past water activity.");

        strcpy(equipmentDatabase[1].name, "Apollo 11 Lunar Module Descent Stage");
        strcpy(equipmentDatabase[1].celestialBody, "Moon");
        strcpy(equipmentDatabase[1].arrival, "Landed at Tranquility Base on July 20, 1969.");
        strcpy(equipmentDatabase[1].importance, "Marked humanity's first successful crewed landing on a celestial body beyond Earth.");
        strcpy(equipmentDatabase[1].discoveries, "Served as the launch platform for humanity's return and left behind early seismic and laser-ranging arrays.");

        itemCount = 2;
        saveEquipmentToFile(dataFile, equipmentDatabase, itemCount);
    }

    int choice;
    do {
        displayWelcomeBanner();
        printf("\n=========================================\n");
        printf("         GHOSTS OF THE VOID MENU         \n");
        printf("=========================================\n");
        printf("1. Explore Relics (Mars & Moon)\n");
        printf("2. Add New Discovered Artifact\n");
        printf("3. Exit Mission Control\n");
        printf("Enter your choice: ");

        if (scanf("%d", &choice) != 1) {
            printf("Invalid input. Please enter a number.\n");
            while(getchar() != '\n'); // clear buffer
            continue;
        }
        getchar(); // consume newline

        switch (choice) {
            case 1:
                exploreEquipment(equipmentDatabase, itemCount);
                break;
            case 2:
                if (itemCount < 20) {
                    addNewEquipment(dataFile);
                    itemCount = loadEquipmentFromFile(dataFile, equipmentDatabase, 20);
                } else {
                    printf("Database is full!\n");
                }
                break;
            case 3:
                printf("\nExiting Ghosts of the Void. Keep exploring the cosmos!\n");
                break;
            default:
                printf("Invalid choice. Try again.\n");
        }
    } while (choice != 3);

    return 0;
}

void displayWelcomeBanner() {
    printf("\n=====================================================\n");
    printf("         GHOSTS OF THE VOID: THE UNSUNG HARDWARE     \n");
    printf("         NASA Space Apps Challenge 2026              \n");
    printf("=====================================================\n");
}

void exploreEquipment(Equipment *eqList, int count) {
    char targetBody[20];
    printf("\nSelect Destination ([1] Mars / [2] Moon): ");
    int destChoice;
    scanf("%d", &destChoice);
    getchar();

    if (destChoice == 1) {
        strcpy(targetBody, "Mars");
    } else if (destChoice == 2) {
        strcpy(targetBody, "Moon");
    } else {
        printf("Invalid destination selection.\n");
        return;
    }

    printf("\n--- Available Relics on %s ---\n", targetBody);
    int matchIndices[20];
    int matchCount = 0;

    for (int i = 0; i < count; i++) {
        if (strcasecmp(eqList[i].celestialBody, targetBody) == 0) {
            matchIndices[matchCount] = i;
            printf("[%d] %s\n", matchCount + 1, eqList[i].name);
            matchCount++;
        }
    }

    if (matchCount == 0) {
        printf("No equipment logged for %s yet.\n", targetBody);
        return;
    }

    printf("Select a piece of equipment (1-%d): ", matchCount);
    int eqChoice;
    scanf("%d", &eqChoice);
    getchar();

    if (eqChoice < 1 || eqChoice > matchCount) {
        printf("Invalid selection.\n");
        return;
    }

    Selected:
    {
        Equipment selected = eqList[matchIndices[eqChoice - 1]];
        int tabChoice;
        do {
            printf("\n=========================================\n");
            printf(" RELIC: %s (%s)\n", selected.name, selected.celestialBody);
            printf("=========================================\n");
            printf("1. Arrival Data\n");
            printf("2. Mission Importance\n");
            printf("3. Major Discoveries\n");
            printf("4. Back to Destination Menu\n");
            printf("Select an information tab: ");
            scanf("%d", &tabChoice);
            getchar();

            switch (tabChoice) {
                case 1:
                    printf("\n[Arrival Log]:\n%s\n", selected.arrival);
                    break;
                case 2:
                    printf("\n[Importance]:\n%s\n", selected.importance);
                    break;
                case 3:
                    printf("\n[Discoveries]:\n%s\n", selected.discoveries);
                    break;
                case 4:
                    break;
                default:
                    printf("Invalid tab choice.\n");
            }
        } while (tabChoice != 4);
    }
}

void addNewEquipment(const char *filename) {
    Equipment newEq;
    printf("\nEnter equipment name: ");
    fgets(newEq.name, MAX_NAME_LEN, stdin);
    newEq.name[strcspn(newEq.name, "\n")] = 0;

    printf("Enter celestial body (Mars/Moon): ");
    fgets(newEq.celestialBody, 20, stdin);
    newEq.celestialBody[strcspn(newEq.celestialBody, "\n")] = 0;

    printf("Enter Arrival details: ");
    fgets(newEq.arrival, MAX_DESC_LEN, stdin);
    newEq.arrival[strcspn(newEq.arrival, "\n")] = 0;

    printf("Enter Importance details: ");
    fgets(newEq.importance, MAX_DESC_LEN, stdin);
    newEq.importance[strcspn(newEq.importance, "\n")] = 0;

    printf("Enter Discovery details: ");
    fgets(newEq.discoveries, MAX_DESC_LEN, stdin);
    newEq.discoveries[strcspn(newEq.discoveries, "\n")] = 0;

    FILE *file = fopen(filename, "a");
    if (file == NULL) {
        printf("Error opening data file for writing.\n");
        return;
    }

    fprintf(file, "%s|%s|%s|%s|%s\n", newEq.name, newEq.celestialBody, newEq.arrival, newEq.importance, newEq.discoveries);
    fclose(file);
    printf("Successfully added new relic to the archive!\n");
}

int loadEquipmentFromFile(const char *filename, Equipment *eqList, int maxItems) {
    FILE *file = fopen(filename, "r");
    if (file == NULL) {
        return 0; // File doesn't exist yet
    }

    int count = 0;
    char buffer[1024];
    while (fgets(buffer, sizeof(buffer), file) != NULL && count < maxItems) {
        buffer[strcspn(buffer, "\n")] = 0;
        char *token = strtok(buffer, "|");
        if (token != NULL) strcpy(eqList[count].name, token);

        token = strtok(NULL, "|");
        if (token != NULL) strcpy(eqList[count].celestialBody, token);

        token = strtok(NULL, "|");
        if (token != NULL) strcpy(eqList[count].arrival, token);

        token = strtok(NULL, "|");
        if (token != NULL) strcpy(eqList[count].importance, token);

        token = strtok(NULL, "|");
        if (token != NULL) strcpy(eqList[count].discoveries, token);

        count++;
    }

    fclose(file);
    return count;
}

void saveEquipmentToFile(const char *filename, Equipment *eqList, int count) {
    FILE *file = fopen(filename, "w");
    if (file == NULL) return;

    for (int i = 0; i < count; i++) {
        fprintf(file, "%s|%s|%s|%s|%s\n", eqList[i].name, eqList[i].celestialBody, eqList[i].arrival, eqList[i].importance, eqList[i].discoveries);
    }
    fclose(file);
}
```

