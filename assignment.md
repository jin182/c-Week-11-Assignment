# C언어 학습 정리 (보조자료 6개 + 퀴즈2 5개)

## 1. scanf 및 보안 (문자열 거꾸로 출력)
```c
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

## 2. 함수의 포인터

```c
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

## 3. 2차원 배열

```c
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

## 4. 구조체 성적 바이너리 파일 저장

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

typedef struct {
    int k, e, m;
} S;

int main() {
    S a[2] = { {80, 90, 85}, {70, 75, 95} };
    FILE *p = fopen("my.bin", "wb");
    if (p != NULL) {
        fwrite(a, sizeof(S), 2, p);
        fclose(p);
    }
    return 0;
}

```

## 5. 바이너리 파일 읽기 및 평균 출력

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

typedef struct {
    int k, e, m;
} S;

int main() {
    S a[2];
    FILE *p = fopen("my.bin", "rb");
    if (p != NULL) {
        fread(a, sizeof(S), 2, p);
        fclose(p);

        printf("개인1: %.1f, 개인2: %.1f\n", (a[0].k + a[0].e + a[0].m) / 3.0, (a[1].k + a[1].e + a[1].m) / 3.0);
        printf("과목1: %.1f, 과목2: %.1f, 과목3: %.1f\n", (a[0].k + a[1].k) / 2.0, (a[0].e + a[1].e) / 2.0, (a[0].m + a[1].m) / 2.0);
    }
    return 0;
}

```

## 6. 버블 정렬 (Bubble Sort)

```c
#include <stdio.h>

int main() {
    int a[] = { 2, 4, 1, 5, 3 }, i, j, t;
    for (i = 0; i < 4; i++)
        for (j = 0; j < 4 - i; j++)
            if (a[j] < a[j + 1]) {
                t = a[j];
                a[j] = a[j + 1];
                a[j + 1] = t;
            }
    for (i = 0; i < 5; i++)
        printf("%d ", a[i]);
    return 0;
}

```

---

## 7. 정수형 변수 2개의 합 출력 (퀴즈 2-2)

```c
#include <stdio.h>

int main() {
    int a = 22, b = 33;
    int sum = a + b;
    printf("%d + %d = %d\n", a, b, sum);
    return 0;
}

```

## 8. 명령행 인자로 두 정수의 합 출력 (퀴즈 2-5)

```c
#include <stdio.h>
#include <stdlib.h>

int main(int n, char *v[]) {
    if (n < 3) {
        printf("사용법: 프로그램이름 정수1 정수2\n");
        return 1;
    }

    int a = atoi(v[1]);
    int b = atoi(v[2]);
    
    printf("%d\n", a + b);
    return 0;
}

```

## 9. 반복문을 이용한 5부터 10까지의 합 (퀴즈 2-3)

```c
#include <stdio.h>

int main() {
    int sum = 0, i = 5;
    while (i <= 10) {
        sum += i;
        i++;
    }
    printf("%d\n", sum);
    return 0;
}

```

## 10. 동적 메모리 할당을 이용한 합 출력 (퀴즈 2-4)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p = (int*)malloc(sizeof(int) * 3);
    
    *(p + 0) = 11; 
    *(p + 1) = 33; 
    *(p + 2) = 55;
    
    printf("%d\n", *(p + 0) + *(p + 1) + *(p + 2));
    
    free(p);
    return 0;
}

```

## 11. 구조체 초기화 및 개인별 평균 계산 (퀴즈 2-1)

```c
#include <stdio.h>

typedef struct {
    char name[20];
    int kr, en;
} Student;

int main() {
    Student s[3] = {
        {"J.C. Shim", 90, 80},
        {"G.D. Hong", 85, 95},
        {"J.Y. Ko", 88, 92}
    };
    
    for(int i = 0; i < 3; i++) {
        double avg = (s[i].kr + s[i].en) / 2.0;
        printf("%s 평균: %.2f\n", s[i].name, avg);
    }
    return 0;
}

```

```

```
