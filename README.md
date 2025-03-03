To implement the `wc` command in C for a Linux environment, you'll need to read from a file or standard input and count lines, words, and characters. Here's a basic implementation using only command-line arguments


#include <stdio.h>

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Usage: %s <filename>\n", argv[0]);
        return 1;
    }

    FILE *file = fopen(argv[1], "r");
    if (!file) {
        perror("Error opening file");
        return 1;
    }

    int lines = 0, words = 0, characters = 0;
    int in_word = 0;
    char c;

    while ((c = fgetc(file)) != EOF) {
        characters++;

        if (c == '\n') {
            lines++;
        }

        if (c == ' ' || c == '\t' || c == '\n' || c == '\r' || c == '\v' || c == '\f') {
            in_word = 0;
        } else if (!in_word) {
            words++;
            in_word = 1;
        }
    }

    fclose(file);

    printf("Lines: %d\n", lines);
    printf("Words: %d\n", words);
    printf("Characters: %d\n", characters);

    return 0;
}
 It reads from the file specified in the command-line argument and prints the number of lines, words, and characters.
