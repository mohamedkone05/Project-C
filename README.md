# Project-C
Un jeu de calcul mathématique 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
typedef struct {
 char name[50];
 int score;
} User;

void saveUserData(User user) {
 FILE *file = fopen("point2.txt", "r");
 FILE *temp = fopen("temp.txt", "w");
 int found = 0;
 User tempUser;

 if (temp == NULL) {
 printf("Error opening file!");
 return;
 }

 if (file != NULL) {
 while (fscanf(file, "%49s %d", tempUser.name, &tempUser.score) != EOF) {
 if (strcmp(tempUser.name, user.name) == 0) {
 tempUser.score = user.score;
 found = 1;
 }
 fprintf(temp, "%s %d\n", tempUser.name, tempUser.score);
 }
 fclose(file);
 }
 
 if (!found) {
 fprintf(temp, "%s %d\n", user.name, user.score);
 }
 
 fclose(temp);
 remove("point2.txt");
 rename("temp.txt", "point2.txt");
}



User loadUserData(char *nom) {
 User user;
 FILE *file = fopen("point2.txt", "r");
 if (file == NULL) {
 strcpy(user.name, nom);
 user.score = 0;
 return user;
 }
 
 while (fscanf(file, "%49s %d", user.name, &user.score) != EOF) {
 if (strcmp(user.name, nom) == 0) {
 fclose(file);
 return user; // User found, return existing data
 }
 }
 
 fclose(file);
 // If user not found, return a new user with default values
 strcpy(user.name, nom);
 user.score = 0;
 return user;
}
int Addition(int *score) {
 int point, x, y, solution, s_user, suivant, montre_solution;

 printf("=== Addition ===\n"); 
 printf("Vous avez 3 essais.\n");

 do { 
 srand(time(NULL));
 point = 1;
 x = rand() % 101; 
 y = rand() % 100 + 1; 
 solution = x + y; 
 do { 
 printf("%d + %d = ", x, y);
 scanf("%d", &s_user);

 if (s_user == solution) { 
 
 printf("Bravo !\n");
 break;
 } else {
 printf("Perdu ! Si tu veux voir la solution, entrez 5, sinon entrez 4 "": "); 
 scanf("%d", &montre_solution);
 if (montre_solution ==
 5) { 
 printf("La solution est : %d\n", solution);
 point = 0; 
 break;
 }
 }
 point++;
 } while (point < 4);
 if (point == 1) {
 printf("Vous avez gagne 10 points.\n");
 *score += 10;
 } else if (point == 2) {
 printf("Vous avez gagne 5 points.\n"); 
 
 *score += 5;
 } else if (point == 3) {
 printf("Vous avez gagne 1 point.\n"); 
 
 *score += 1;
 } else {
 printf("Vous avez perdu.\nDesole, vous ne gagnez aucun point.\n"); 
 }
 printf("Votre score est : %d\n", *score); 
 do {
 printf("Voulez-vous continuer ? (1 = Oui, 0 = Non) : ");
 scanf("%d", &suivant);

 if (suivant != 0 && suivant != 1) {
 printf("Valeur invalide. Veuillez entrer 1 ou 0.\n");
 }
 } while (suivant != 0 && suivant != 1);

 } while (suivant == 1);

 printf("Fin du jeu. Votre score final est : %d\n",*score);
 
 return (*score);
}
int complexoperation(int *score) {
 int x, y, z, point, suivant, montre_solution;
 int solution, user_solution;
 char operation[] = "+*-";
 printf("====complex operation ===="); 
 printf("\n");
 do { 
 point = 1;
 char op =
 operation[rand() % 3]; 
 char op2 =
 operation[rand() % 3]; 
 do {
 x = rand() % 101; 
 y = rand() % 10; 
 z = rand() % 100 + 1; 
 } while (x < y || x < z || y < z);
 do 
 {
 switch (
 op) 
 {
 case '+':
 switch (op2) {
 case '+':
 solution = x + y + z; 
 printf("%d + %d + %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 case '-':
 solution = x + y - z;
 printf("%d + %d - %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 case '*':
 solution = x + (y * z);
 printf("%d + %d * %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 }
 break;
 case '-':
 switch (op2) {
 case '+':
 solution = x - y + z;
 printf("%d - %d + %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 case '-':
 solution = x - y - z;
 printf("%d - %d - %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 case '*':
 solution = x - (y * z);
 printf("%d - %d * %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 }
 break;
 case '*':
 switch (op2) {
 case '+':
 solution = (x * y) + z;
 printf("%d * %d + %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 case '-':
 solution = (x * y) - z;
 printf("%d * %d - %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 case '*':
 solution = x * (y * z);
 printf("%d * %d * %d = ", x, y, z);
 scanf("%d", &user_solution);
 break;
 }
 }
 if (user_solution == solution) { 
 printf("bravo \n");
 break;
 } else {
 printf("Perdu ! Si tu veux voir la solution, entrez 5, sinon entrez 4 "":"); 
 scanf("%d", &montre_solution);
 if (montre_solution ==
 5) { 
 printf("la solution est : %d \n", solution);
 point = 0; 
 break;
 }
 }
 point++;
 } while (point < 4);
 if (point == 1) {
 printf("Vous avez gagne 10 points.\n");
 *score += 10;
 } else if (point == 2) {
 printf("Vous avez gagne 5 points.\n"); 
 *score += 5;
 } else if (point == 3) {
 printf("Vous avez gagne 1 point.\n"); 
 *score += 1;
 } else {
 printf("Vous avez perdu \n");
 printf("Desole, vous ne gagnez aucun point.\n");
 }
 printf("Votre score est : %d\n", *score);
 do { 
 printf("Voulez-vous continuer ? (1 = Oui, 0 = Non) : ");
 scanf("%d", &suivant);

 if (suivant != 0 && suivant != 1) {
 printf("Valeur invalide. Veuillez entrer 1 ou 0.\n");
 }
 } while (suivant != 0 && suivant != 1);
 } while (suivant == 1);
 printf("Fin du jeu. Votre score final est : %d\n",
 *score); 
 
 return (*score); 
}
int Division(int *score) {
 int point, x, y, solution, s_user, suivant, montre_solution;

 printf("=== Division ===\n"); 
 printf("Vous avez 3 essais.\n");

 do { 
 srand(time(NULL));
 point = 1;
 do {
 x = rand() % 101; 
 y = rand() % 100 + 1;
 } while (x % y != 0 || y == 0 ||
 x == 0); 
 solution = x / y; 
 do { 
 printf("%d / %d = ", x, y);
 scanf("%d", &s_user);

 if (s_user == solution) { 
 printf("Bravo !\n");
 break;
 } else {
 printf("Perdu ! Si tu veux voir la solution, entrez 5, sinon entrez 4 : ");
 scanf("%d", &montre_solution);

 if (montre_solution ==5) { 
 printf("La solution est : %d\n", solution);
 point = 0;
 break;
 }
 }
 point++;
 } while (point < 4);
 if (point == 1) { 
 printf("Vous avez gagne 10 points.\n");
 *score += 10;
 } else if (point ==
 2) { 
 printf("Vous avez gagne 5 points.\n");
 *score += 5;
 } else if (point == 3) { 
 printf("Vous avez gagne 1 point.\n");
 *score += 1;
 } else {
 printf("Vous avez perdu.\nDesole, vous ne gagnez aucun point.\n"); 
 }
 printf("Votre score est : %d\n", *score);
 do {
 printf("Voulez-vous continuer ? (1 = Oui, 0 = Non) : ");
 scanf("%d", &suivant);

 if (suivant != 0 &&
 suivant != 1) { 
 printf("Valeur invalide. Veuillez entrer 1 ou 0.\n");
 }
 } while (suivant != 0 && suivant != 1);

 } while (suivant == 1);

 printf("Fin du jeu. Votre score final est : %d\n",*score); 

 return (*score); 
}

int multiplication(int *score) {
 int point, x, y, solution, s_user, suivant, montre_solution;

 printf("=== Multiplication ===\n"); 
 printf("Vous avez 3 essais.\n");

 do { 
 point = 1;
 x = rand() % 11; 
 y = rand() % 10 + 1; 
 solution = x * y; 

 do { 
 printf("%d * %d = ", x, y);
 scanf("%d", &s_user);

 if (s_user == solution) { 
 printf("Bravo !\n");
 break;
 } else { 
 printf("Perdu ! Si tu veux voir la solution, entrez 5, sinon entrez 4 : ");
 scanf("%d", &montre_solution);

 if (montre_solution ==5) { 
 printf("La solution est : %d\n", solution);
 point = 0; 
 break;
 }
 }
 point++;
 } while (point < 4);
 if (point == 1) {
 printf("Vous avez gagne 10 points.\n"); 
 *score += 10;
 } else if (point == 2) {
 printf("Vous avez gagne 5 points.\n");
 *score += 5;
 } else if (point == 3) {
 printf("Vous avez gagne 1 point.\n"); 
 *score += 1;
 } else {
 printf("Vous avez perdu.\nDesole, vous ne gagnez aucun point.\n"); 
 }
 printf("Votre score est : %d\n", *score); 
 do {
 printf("Voulez-vous continuer ? (1 = Oui, 0 = Non) : ");
 scanf("%d", &suivant);

 if (suivant != 0 && suivant != 1) {
 printf("Valeur invalide. Veuillez entrer 1 ou 0.\n");
 }
 } while (suivant != 0 && suivant != 1);

 } while (suivant == 1);

 printf("Fin du jeu. Votre score final est : %d\n",
 *score); 
 
 return (*score); 
}
int Soustraction(int *score) {
 int point, x, y, solution, s_user, suivant, montre_solution;
 printf("=== Soustraction ===\n");
 printf("Vous avez 3 essais.\n");
 do {
 srand(time(NULL));
 point = 1;
 do { 
 x = rand() % 101; 
 y = rand() % 100 + 1;
 } while (y < x);
 solution = y - x; 
 do {
 printf("%d - %d = ", y, x);
 scanf("%d", &s_user);
 if (s_user == solution) { 
 printf("Bravo !\n");
 break;
 } else {
 printf("Perdu ! Si tu veux voir la solution, entrez 5, sinon entrez 4 "": "); 
 scanf("%d", &montre_solution);
 if (montre_solution ==
 5) { 
 printf("La solution est : %d\n", solution);
 point = 0; 
 break;
 }
 }
 point++;
 } while (point < 4);
 if (point == 1) {
 printf("Vous avez gagne 10 points.\n"); 
 *score += 10;
 } else if (point == 2) {
 printf("Vous avez gagne 5 points.\n"); 
 *score += 5;
 } else if (point == 3) {
 printf("Vous avez gagne 1 point.\n"); 
 *score += 1;
 } else {
 printf("Vous avez perdu.\nDesole, vous ne gagnez aucun point.\n"); 
 }
 printf("Votre score est : %d\n", *score); 
 do { 
 printf("Voulez-vous continuer ? (1 = Oui, 0 = Non) : ");
 scanf("%d", &suivant);
 if (suivant != 0 && suivant != 1) {
 printf("Valeur invalide. Veuillez entrer 1 ou 0.\n");
 }
 } while (suivant != 0 && suivant != 1);
 } while (suivant == 1);
 printf("Fin du jeu. Votre score final est : %d\n",
 *score); 
 
 return (*score); 
}
int table_multi(int *score) {
 int i, nb, solution, user_solution, point, suivant;
 printf("===TABLE DE MULTIPLICATION==="); 
 printf("\n");
 do { 
 printf("entrez le nombre : ");
 scanf("%d", &nb); 
 printf("\n");
 point = 0;
 for (i = 1; i <= 10; i++) {
 solution = nb * i;
 printf("%d * %d = ? \n ", nb, i);
 scanf("%d", &user_solution);
 if (user_solution != solution) { 
 printf("perdu \n");
 break;
 } else {
 printf("bravo \n"); 
 point += 1;
 }
 }
 *score = *score + point; 
 printf("vous avez gagne : %d \n,", point ); 
 do { 
 printf("Voulez-vous continuer ? (1 = Oui, 0 = Non) : ");
 scanf("%d", &suivant);

 if (suivant != 0 && suivant != 1) {
 printf("Valeur invalide. Veuillez entrer 1 ou 0.\n");
 }
 } while (suivant != 0 && suivant != 1);

 } while (suivant == 1);
 printf("Fin du jeu. Votre score final est : %d\n",
 *score); 
 return (*score); 
}
int choix(int *score) {
 int choix;

 printf("\n+--------------------------------+\n");
 printf("| 1 : Addition |\n");
 printf("| 2 : Soustraction |\n");
 printf("| 3 : Multiplication |\n");
 printf("| 4 : Tables des multiplications |\n");
 printf("| 5 : Divisions |\n");
 printf("| 6 : Operation complexe |\n");
 printf("| 7 : Factorisation |\n");
 printf("| 0 : Sortir du jeu |\n");
 printf("+--------------------------------+\n");
 printf("Votre score actuel est : %d\n", *score);
 printf("Quel est votre choix ? ");
 scanf("%d", &choix);

 while (choix < 0 || choix > 7) {
 printf("Choix invalide, veuillez reessayer : ");
 scanf("%d", &choix);
 }

 switch (choix) {
 case 1:
 Addition(score);
 break;
 case 2:
 Soustraction(score);
 break;
 case 3:
 multiplication(score);
 break;
 case 4:
 table_multi(score);
 break;
 case 5:
 Division(score);
 break;
 case 6:
 complexoperation(score);
 break;
 case 7:
 Factorisation(score);
 break;
 case 0: 
 printf("Merci de votre visite !\n");
 printf("Votre score final est : %d\n", *score);
 return (0);
 break;
 
 }
 return (1);
}


int main() {
 srand(time(NULL)); 
 char nom[50];
 int i ; 
 printf("Enter your name: ");
 scanf("%49s", nom);
 User user = loadUserData(nom);
 if (strcmp(user.name,"Unknown") != 0) {
 printf("bienvenu, %s! votre dernie score est : %d\n", user.name, user.score);
 }else{
 user.score = 0 ; 
 printf("ok");
 }
 i=1;
 do{
 i = choix(&user.score);
 }while(i!=0);
 saveUserData(user);
 
 return 0;
}
