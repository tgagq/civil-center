#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_LENGTH 50
#define MAX_CITIZENS 100

struct Citizen {
    int ID;
    char name[MAX_LENGTH];
    char surname[MAX_LENGTH];
    char address[MAX_LENGTH];
    char phone[MAX_LENGTH];
    char email[MAX_LENGTH];
};

struct Citizen citizens[MAX_CITIZENS];
int citizenCount = 0;

void registerCitizen() {
    if (citizenCount >= MAX_CITIZENS) {
        printf("Kufiri i qytetareve te regjistruar eshte arritur.\n");
        return;
    }

    struct Citizen newCitizen;

    printf("Vendosni ID: ");
    scanf("%d", &newCitizen.ID);

    printf("Vendosni emrin: ");
    scanf("%s", newCitizen.name);

    printf("Vendosni mbiemrin: ");
    scanf("%s", newCitizen.surname);

    printf("Vendosni adresen: ");
    scanf("%s", newCitizen.address);

    printf("Vendosni numrin e telefonit: ");
    scanf("%s", newCitizen.phone);

    printf("Vendosni email-in: ");
    scanf("%s", newCitizen.email);

    citizens[citizenCount++] = newCitizen;

    printf("Qytetari u regjistrua me sukses.\n");
}

void modifyCitizen() {
    int ID;
    printf("Vendosni ID-n e qytetarit per te modifikuar te dhenat: ");
    scanf("%d", &ID);

    for (int i = 0; i < citizenCount; i++) {
        if (citizens[i].ID == ID) {
            printf("Vendosni emrin e ri: ");
            scanf("%s", citizens[i].name);

            printf("Vendosni mbiemrin e ri: ");
            scanf("%s", citizens[i].surname);

            printf("Vendosni adresen e re: ");
            scanf("%s", citizens[i].address);

            printf("Vendosni numrin e telefonit te ri: ");
            scanf("%s", citizens[i].phone);

            printf("Vendosni email-in e ri: ");
            scanf("%s", citizens[i].email);

            printf("Te dhenat e qytetarit u modifikuan me sukses.\n");
            return;
        }
    }

    printf("Qytetari me kete ID nuk u gjet.\n");
}

void deleteCitizen() {
    int ID;
    printf("Vendosni ID-n e qytetarit per te fshire te dhenat: ");
    scanf("%d", &ID);

    for (int i = 0; i < citizenCount; i++) {
        if (citizens[i].ID == ID) {
            for (int j = i; j < citizenCount - 1; j++) {
                citizens[j] = citizens[j + 1];
            }
            citizenCount--;
            printf("Te dhenat e qytetarit u fshine me sukses.\n");
            return;
        }
    }

    printf("Qytetari me kete ID nuk u gjet.\n");
}

void searchByName() {
    char name[MAX_LENGTH];
    printf("Vendosni emrin qe dëshironi të kërkoni: ");
scanf("%s", name);

int found = 0;

for (int i = 0; i < citizenCount; i++) {
if (strcmp(citizens[i].name, name) == 0) {
printf("ID: %d\nEmri: %s\nMbiemri: %s\nAdresa: %s\nNumri i telefonit: %s\nEmail: %s\n",
citizens[i].ID, citizens[i].name, citizens[i].surname, citizens[i].address, citizens[i].phone, citizens[i].email);
found = 1;
}
}

if (!found) {
printf("Nuk u gjet asnje qytetar me kete emer.\n");
}
}

void searchBySurname() {
char surname[MAX_LENGTH];
printf("Vendosni mbiemrin qe deshironi te kerkoni: ");
scanf("%s", surname);
int found = 0;

for (int i = 0; i < citizenCount; i++) {
    if (strcmp(citizens[i].surname, surname) == 0) {
        printf("ID: %d\nEmri: %s\nMbiemri: %s\nAdresa: %s\nNumri i telefonit: %s\nEmail: %s\n",
            citizens[i].ID, citizens[i].name, citizens[i].surname, citizens[i].address, citizens[i].phone, citizens[i].email);
        found = 1;
    }
}

if (!found) {
    printf("Nuk u gjet asnje qytetar me këtë mbiemër.\n");
}
}

void searchByPhone() {
char phone[MAX_LENGTH];
printf("Vendosni numrin e telefonit që dëshironi të kërkoni: ");
scanf("%s", phone);
int found = 0;

for (int i = 0; i < citizenCount; i++) {
    if (strcmp(citizens[i].phone, phone) == 0) {
        printf("ID: %d\nEmri: %s\nMbiemri: %s\nAdresa: %s\nNumri i telefonit: %s\nEmail: %s\n",
            citizens[i].ID, citizens[i].name, citizens[i].surname, citizens[i].address, citizens[i].phone, citizens[i].email);
        found = 1;
    }
}

if (!found) {
    printf("Nuk u gjet asnje qytetar me këtë numër telefoni.\n");
}
}

void displayStoredData() {
for (int i = 0; i < citizenCount; i++) {
printf("ID: %d\nEmri: %s\nMbiemri: %s\nAdresa: %s\nNumri i telefonit: %s\nEmail: %s\n",
citizens[i].ID, citizens[i].name, citizens[i].surname, citizens[i].address, citizens[i].phone, citizens[i].email);
}
}

void sortByName() {
for (int i = 0; i < citizenCount - 1; i++) {
for (int j = 0; j < citizenCount - i - 1; j++) {
if (strcmp(citizens[j].name, citizens[j + 1].name) > 0) {
struct Citizen temp = citizens[j];
citizens[j] = citizens[j + 1];
citizens[j + 1] = temp;
}
}
}
printf("Qytetaret u rradhitën sipas emrit.\n");
}

void sortBySurname() {
for (int i = 0; i < citizenCount - 1; i++) {
for (int j = 0; j < citizenCount - i - 1; j++) {
if (strcmp(citizens[j].surname, citizens[j + 1].surname) > 0) {
struct Citizen temp = citizens[j];
citizens[j] = citizens[j + 1];
citizens[j + 1] = temp;
}
}
}printf("Qytetaret u rradhitën sipas mbiemrit.\n");
}

int main() {
int choice;
printf("Menuja\n");
printf("0.RRegjistro nje qytetar te ri.\n");
printf("1.Modifiko te dhenat e nje qytetari.\n");
printf("2.Fshi te dhenat e nje qytetari.\n");
printf("3.Kerko sipas emrit.\n");
printf("4.Kekro sipas mbiemrit.\n");
printf("5.Kekro sipas numrit te telefonit\n");
printf("6.Afisho te dhenat e ruajtrua me pare.\n");
printf("7.Rradhit qytetaret sipas emrit.\n");
printf("8.rradhit qytetare sipasi mbiemrit\n");
printf("9.Dil nga programi.\n");
printf("Zgjidh nje opsion:");
do{
    
     
    scanf("%d", &choice);

    switch (choice) {
        case 0:
            registerCitizen();
            break;
        case 1:
            modifyCitizen();
            break;
        case 2:
            deleteCitizen();
            break;
        case 3:
            searchByName();
            break;
        case 4:
            searchBySurname();
            break;
        case 5:
            searchByPhone();
            break;
        case 6:
            displayStoredData();
            break;
        case 7:
            sortByName();
            break;
        case 8:
            sortBySurname();
            break;
        case 9:
            printf("Programi perfundoi.\n");
            return 0;
        default:
            printf("Opsioni i zgjedhur nuk ekziston.\n");
    }
} while (1);

return 0;
}
