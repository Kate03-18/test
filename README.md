// Reading from a file

#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "r");
    if (file == NULL) {
        printf("Could not open file\n");
        return 1;
    }

    char str[100];
    while (fscanf(file, "%s", str) != EOF) {
        printf("%s\n", str);
    }

    fclose(file);
    return 0;
}

// Writing to a File

#include <stdio.h>

int main() {
    FILE *file = fopen("output.txt", "w");
    if (file == NULL) {
        printf("Could not open file\n");
        return 1;
    }

    fprintf(file, "Hello, World!\n");

    fclose(file);
    return 0;
}

// Using Structures

#include <stdio.h>

struct Person {
    char name[50];
    int age;
};

int main() {
    struct Person person1;
    
    // Assigning values to structure members
    strcpy(person1.name, "Alice");
    person1.age = 30;

    // Printing structure members
    printf("Name: %s\n", person1.name);
    printf("Age: %d\n", person1.age);

    return 0;
}

// Array of Pointers

#include <stdio.h>

void sortStrings(char *arr[], int n) {
    char *temp;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (strcmp(arr[i], arr[j]) > 0) {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
}

char* findLongestString(char *arr[], int n) {
    char *longest = arr[0];
    for (int i = 1; i < n; i++) {
        if (strlen(arr[i]) > strlen(longest)) {
            longest = arr[i];
        }
    }
    return longest;
}

void reverseString(char *str) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - i - 1];
        str[len - i - 1] = temp;
    }
}

int main() {
    char *fruits[] = {"Apple", "Banana", "Cherry", "Date"};
    int n = sizeof(fruits) / sizeof(fruits[0]);

    // Finding the longest string
    char *longest = findLongestString(fruits, n);

    printf("Longest string: %s\n", longest);

     for (int i = 0; i < n; i++) {
        reverseString(fruits[i]);
    }

    // Printing the reversed strings
    for (int i = 0; i < n; i++) {
        printf("%s\n", fruits[i]);
    }

    sortStrings(fruits, n);

    for (int i = 0; i < n; i++) {
        printf("%s\n", fruits[i]);
    }

    return 0;
}

// Strings

#include <stdio.h>
#include <string.h>

int main() {
    char str1[20] = "Hello";
    char str2[20] = "World";

    // Concatenating strings
    strcat(str1, " ");
    strcat(str1, str2);
    printf("%s\n", str1); // Output: Hello World

    // Finding the length of a string
    printf("Length: %lu\n", strlen(str1)); // Output: 11

    // Comparing strings
    if (strcmp(str1, str2) == 0) {
        printf("Strings are equal\n");
    } else {
        printf("Strings are not equal\n");
    }

    return 0;
}


// რიცხვების ციფრების ჯამი
#include <stdio.h>

int main() {
  int num, sum = 0, digits = 0;
  
  scanf("%d", &num);
  do
   {
      sum += num % 10;
      num /= 10;
      digits++;
  }
  while (num > 0);
  printf("sum = %d\ndigits = %d", sum, digits);

    return 0;
} 


    1. შექმენით სტრუქტურა - ავტომობილი, რომლის წევრებია:
    • მანქანის მოდელი
    • მწარმოებელი
    • ტიპი
    • გამოშვების წელი
    • რეგისტრაციის თარიღი
    • შექმენით სტრუქტურის ტიპის მასივი (მინიმუმ 5 ელემენტით);
    • განახორციელეთ მასივის ობიექტების ინიციალიზაცია;
    • გამოიტანეთ სრული ინფორმაცია იმ მანქანების შესახებ, რომელთა ასაკი 10 წელზე ნაკლებია
    • გამოიტანეთ სედანის ტიპის მანქანების შესახებ სრული ინფორმაცია,  თუ ასეთი ინფორმაცია არ არსებობს გამოტანეთ შესაბამისი შეტყობინება

ამოხსნა:
#include <stdio.h>
#include <string.h>

// Structure definition for a car
struct Car {
    char model[50];
    char manufacturer[50];
    char type[20];
    int release_year;
    char registration_date[20];
};

int main() {
    
    struct Car cars[5] = {
        {"car1", "company1", "truck", 2010, "2010-05-21"},
        // {"car2", "company2", "sedan", 2012, "2012-05-21"},
        // {"car3", "company3", "sedan", 2010, "2015-05-21"},
        {"car4", "company4", "sport", 2020, "2021-05-21"},
        {"car5", "company5", "truck", 2010, "1999 -05-21"},
        
    };

    
    printf("Cars older than 10 years:\n");
    int olderThanTenFound = 0;
    for (int i = 0; i < 5; i++) {
        if (2024 - cars[i].release_year > 10) {
            olderThanTenFound = 1;
            printf("Model: %s\nManufacturer: %s\nType: %s\nRelease Year: %d\nRegistration Date: %s\n\n",
                   cars[i].model, cars[i].manufacturer, cars[i].type, cars[i].release_year, cars[i].registration_date);
        }
    }
    if (!olderThanTenFound) {
        printf("No cars older than 10 years found.\n");
    }

    int sedanFound = 0;
    printf("Sedan type vehicles:\n");
    for (int i = 0; i < 5; i++) {
        if (strcmp(cars[i].type, "sedan") == 0) {
            printf("Model: %s\nManufacturer: %s\nType: %s\nRelease Year: %d\nRegistration Date: %s\n\n",
                   cars[i].model, cars[i].manufacturer, cars[i].type, cars[i].release_year, cars[i].registration_date);
        }
    }
    if (!sedanFound) {
        printf("No sedan type cars found.\n");
    }

    return 0;
}


    2. წაიკითხეთ 2 სტრიქონი კონსოლიდან. 
დაადგინეთ სტრიქონების სიგრძე;
შეადარეთ სტრიქონები;
ფუნქციის გამოყენებით სტრიქონის სიმბოლოები გადაიყვანეთ დაბალი რეგისტრის სიმბოლოებში და დათვალეთ ციფრების რაოდენობა სტრიქონში.

ამოხსნა:

#include <stdio.h>
#include <string.h>

int main() {
    char str1[100], str2[100];
    int len1, len2;
    int digitCount1 = 0, digitCount2 = 0;

    
    printf("Enter the first string: ");
    scanf("%99s", str1); 

    printf("Enter the second string: ");
    scanf("%99s", str2); 

    len1 = strlen(str1);
    len2 = strlen(str2);

    
    int compareResult = strcmp(str1, str2);
    if (compareResult < 0) {
        printf("String 1 is before String 2.\n");
    } else if (compareResult > 0) {
        printf("String 2 is before String 1.\n");
    } else {
        printf("Both strings are equal.\n");
    }

    
    for (int i = 0; str1[i] != '\0'; i++) {
        
        if (str1[i] >= 'A' && str1[i] <= 'Z') {
            str1[i] += ('a' - 'A');
        }
        
        if (str1[i] >= '0' && str1[i] <= '9') {
            digitCount1++;
        }
    }

    for (int i = 0; str2[i] != '\0'; i++) {
        
        if (str2[i] >= 'A' && str2[i] <= 'Z') {
            str2[i] += ('a' - 'A');
        }
        
        if (str2[i] >= '0' && str2[i] <= '9') {
            digitCount2++;
        }
    }

    printf("Length of String 1: %d\n", len1);
    printf("Length of String 2: %d\n", len2);
    printf("Number of digits in String 1: %d\n", digitCount1);
    printf("Number of digits in String 2: %d\n", digitCount2);

    return 0;
}


3. შეადარეთ ორ სტრიქონული ცვლადი ერთმანეთს, გამოიყენეთ ფუნქცია, ფუნქციას არგუმენტებად გადაეცით მისამართები. 

#include <stdio.h>
int compareStrings(char *str1, char *str2); 

int main() {
        char str1[] = "Hello";
        char str2[] = "Hello";
        
        
        if (compareStrings(str1, str2) == 1) {
                printf("The strings are equal.\n");
        } else {
                printf("The strings are not equal.\n");
        }
        
        return 0;
}

int compareStrings(char *str1, char *str2) {
        while (*str1 && *str2 && *str1 == *str2) {
                str1++;
                str2++;
        }
        if(*str1 == '\0' && *str2 == '\0'){
                return 1;
        }else{
                return 0;
        }
        
}

4. დაწერეთ კოდი, რომელიც ფაილიდან წაიკითხავს მონაცემებს სტრუქტურაში და გამოიტანს ეკრანზე. ფაილი შეიცავს სტუდენტის სახელსა და გვარს და 3 საგანში შეფასებებს

#include <stdio.h>

#define MAX_STUDENTS 100
#define MAX_NAME_LENGTH 50


struct Student {
    char firstName[MAX_NAME_LENGTH];
    char lastName[MAX_NAME_LENGTH];
    float Qartuli;
    float Matematika;
    float Istoria;
};

int main() {
    FILE *file;
    struct Student students[MAX_STUDENTS];
    int numStudents = 0;


    file = fopen("gr5.txt", "r");
    if (file == NULL) {
        printf("Error opening file.\n");
        return 1;
    }


    while (fscanf(file, "%s %s %f %f %f", students[numStudents].firstName, students[numStudents].lastName,
                  &students[numStudents].Qartuli, &students[numStudents].Matematika, &students[numStudents].Istoria) != EOF) {
        numStudents++;
        if (numStudents >= MAX_STUDENTS) {
            printf("Maximum number of students reached.\n");
            break;
        }
    }


    fclose(file);

    printf("Student\t\t\tQartuli\tMatematika\tIstoria\n");
    for (int i = 0; i < numStudents; i++) {
        printf("%s %s\t\t%.2f\t%.2f\t%.2f\n", students[i].firstName, students[i].lastName,
               students[i].Qartuli, students[i].Matematika, students[i].Istoria);
    }

    return 0;
}

6.  წაიკითხეთ text_shifr.txt ფაილიდან ტექსტი. რომელიც დაშიფრულია.  დაადგინეთ ტექსტის სიგრძე. ეკრანზე გამოიტანეთ მიმდინარე თარიღი და დრო.  
აღადგინეთ საწყისი ტექსტი, თუ დაშიფვრისათვის გამოყენებულია  შემდეგი კოდირება. 
ხმოვნები: 
 a - # 
e- @ 
o-! 
u-$ 
I -% 
რამდენიმე თანხმოვანი: c- ( 
 k -) 
b -* 
d -& 
t - ^ 
მიღებული ტექსტი და მიმდინარე თარიღი ჩაწერეთ ახალ ფაილში.
დაშიფრული ტექსტი: ^h#^'s !n@ sm#ll s^@p f!r # m#n, !n@ g%#n^ l@#p f!r m#n)%n&.

კოდი: 
#include <stdio.h>
#include <time.h>


void decryptText(char *text) {
    while (*text) {
        switch (*text) {
            case '#':
                *text = 'a';
                break;
            case '@':
                *text = 'e';
                break;
            case '!':
                *text = 'o';
                break;
            case '$':
                *text = 'u';
                break;
            case '%':
                *text = 'I';
                break;
            case '(':
                *text = 'c';
                break;
            case ')':
                *text = 'k';
                break;
            case '*':
                *text = 'b';
                break;
            case '&':
                *text = 'd';
                break;
            case '^':
                *text = 't';
                break;
        }
        text++;
    }
}

int main() {
    
 
  FILE *file;
  char ciphertext[1000]; 

 
  file = fopen("text_shifr.txt", "r");
  if (file == NULL) {
      printf("Error opening file!");
  }

  
  fscanf(file, "%[^\n]", ciphertext);

 
  fclose(file);

    
  decryptText(ciphertext);

    
  time_t current_time = time(NULL);
  struct tm *timeinfo = localtime(&current_time);
  char time_str[20];
  strftime(time_str, 20, "%Y-%m-%d %H:%M:%S", timeinfo);

  
  file = fopen("decrypted_text.txt", "w");
  if (file != NULL) {
      fprintf(file, "Decrypted Text: %s\n", ciphertext);
      fprintf(file, "Current Date and Time: %s\n", time_str);
      fclose(file);
  } else {
      printf("Error opening file!");
  }

  return 0;
}
 
 
 7. წაიკითხეთ მონაცმები ფაილიდან, რომელშიც ყოველ სტრიქონზე არის ორი რიცხვების წყვილი, გამოყოფილი ერთმანეთისაგან space-ით. განიხილეთ ეს რიცხვები, როგორც ვექტორის კოორდინატები სიბრტყეზე. იპოვეთ 
პრაქტიკული დავალება 5 
თითოეული ვექტრის სიგრძე, მიღებული შედეგები და საწყისი მონაცემები ჩაწერეთ ახალ ფაილში შემდეგი სახით: 
 ვექტორი: | vector(x,y)|=მიღებული შედეგი მაგ.: თუ ფაილში წერია 3 4 
 6 8 
 5 7 
უნდა მიიღოთ 
| vector(3,4)|=5 
| vector(6,8)|=10 
| vector(5,7)|=8.7234


კოდი:
#include <stdio.h>
#include <math.h>

int main() {
    FILE *inputFile, *outputFile;
    inputFile = fopen("input.txt", "r");
    outputFile = fopen("output.txt", "w");

    if (inputFile == NULL || outputFile == NULL) {
        printf("Error opening files.\n");
    }

    float x, y;
    while (fscanf(inputFile, "%f %f", &x, &y) == 2) {
        float length = sqrt(x * x + y * y);
        fprintf(outputFile, "| vector(%f,%f)|=%f\n", x, y, length);
    }

    fclose(inputFile);
    fclose(outputFile);

    return 0;
}

