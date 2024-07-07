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


