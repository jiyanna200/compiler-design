Pgm 1
#include <stdio.h>
#include <ctype.h>
#include <string.h>

int main() {
    FILE *f = fopen("input.c", "r");
    char ch, s[100];
    int i;

    if (!f) {
        printf("File not found");
        return 0;
    }

    while ((ch = fgetc(f)) != EOF) {
        if (isspace(ch)) continue;

        if (isalpha(ch)) {
            i = 0;
            do {
                s[i++] = ch;
                ch = fgetc(f);
            } while (isalnum(ch));
            s[i] = '\0';
            if (ch != EOF) ungetc(ch, f);

            if (!strcmp(s, "int") || !strcmp(s, "float") ||
                !strcmp(s, "if") || !strcmp(s, "return"))
                printf("%s : Keyword\n", s);
            else
                printf("%s : Identifier\n", s);
        }
        else if (isdigit(ch))
            printf("%c : Number\n", ch);
        else if (strchr("+-*=<>!", ch))
            printf("%c : Operator\n", ch);
        else if (strchr("(){}[],;#", ch))
            printf("%c : Symbol\n", ch);
    }

    fclose(f);
    return 0;
}


else if (isdigit(ch)) {
    i = 0;
    do {
        s[i++] = ch;
        ch = fgetc(f);
    } while (isdigit(ch) || ch == '.');
    s[i] = '\0';
    if (ch != EOF) ungetc(ch, f);
    printf("%s : Number\n", s);
}
