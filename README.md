#include <stdio.h>
struct Patient {
 char name[50];  int age;
    char disease[100];
};

int main() {
    FILE *fp;
    int choice;
    char filename[] = "patients.txt";
    struct Patient p;
    char buffer[200];
    int ch;

    while (1) {
        printf("\n------ PATIENT MENU ------\n");
        printf("1. Add Patient (write using fprintf)\n");
        printf("2. View Patients (read using fscanf)\n");
        printf("3. Display File (character-by-character)\n");
        printf("4. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);
        getchar();   // clear newline

        switch (choice) {

        case 1:   // ADD PATIENT
            fp = fopen(filename, "a");
            if (!fp) {
                printf("Error opening file!\n");
                break;
            }

            printf("Enter patient name: ");
            fgets(p.name, sizeof(p.name), stdin);

            printf("Enter age: ");
            scanf("%d", &p.age);
            getchar();

            printf("Enter disease: ");
            fgets(p.disease, sizeof(p.disease), stdin);

            // write record
            fprintf(fp, "%s%d\n%s", p.name, p.age, p.disease);
            fprintf(fp, "---\n"); // separator

            fclose(fp);
            printf("Patient added!\n");
            break;

        case 2:   // VIEW PATIENTS using fscanf/fgets
            fp = fopen(filename, "r");
            if (!fp) {
                printf("patients.txt not found!\n");
                break;
            }

            printf("\n------ PATIENT RECORDS ------\n");
            while (fgets(buffer, sizeof(buffer), fp)) {
                printf("%s", buffer);
            }

            fclose(fp);
            break;

        case 3:   // SHOW CHAR BY CHAR
            fp = fopen(filename, "r");
            if (!fp) {
                printf("patients.txt not found!\n");
                break;
            }

            printf("\n------ FILE (char-by-char) ------\n");
            while ((ch = fgetc(fp)) != EOF) {
                putchar(ch);
            }

            fclose(fp);
            break;

        case 4:
            printf("Exiting...\n")
 return 0;

        default:
            printf("Invalid choice!\n");
        }
    }

    return 0;
}

