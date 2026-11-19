1. scanf 및 보안
c```
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>

int main(void) {
    char str[1000];
    printf("문장 입력: ");
    scanf("%999[^\n]", str);
    for (int i = (int)strlen(str) - 1; i >= 0; i--) {
        printf("%c", str[i]);
    }
    return 0;
}
```
2. 함수의 포인터
c```
  #include <stdio.h>

int sub(int a, int b) {
    return a - b;
}

int main() {
    int a = 11, b = 22;
    int (*calc)(int, int) = sub;
    printf("%d\n", calc(a, b));
    return 0;
}
```
3. 2차원 배열
c```
#include <stdio.h>

int main() {
    int a[3][4] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 };
    int i, j, s = 0;

    for (i = 0; i < 3; i++)
        for (j = 0; j < 4; j++)
            if (a[i][j] % 2 == 1)
                s += a[i][j];

    printf("%d\n", s);
    return 0;
}
```
