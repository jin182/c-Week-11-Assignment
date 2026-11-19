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

## 4. 구조체로 2명의 3과목 성적을 생성해서 바이너리 형태로 my.bin에 저장해 줘

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

## 5. 바이너리 파일 읽기 및 평균 출력(이 파일을 읽고 개인 평균, 과목 평균을 출력해 줘)

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

## 7. 정수형 변수 2개에 각각 22와 33을 저장하고, 두 수의 합을 계산하여 화면에 출력하는 C언어 코드를 작성하시오.

```c
#include <stdio.h>

int main() {
    int a = 22, b = 33;
    int sum = a + b;
    printf("%d + %d = %d\n", a, b, sum);
    return 0;
}

```

## 8.  명령행 인자(Command Line Arguments)로 두 정수를 입력받아 합을 출력하는 프로그램을 작성하시오.

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

## 9.반복문(for 또는 while)을 사용하여 5부터 10까지의 정수를 모두 더한 결과를 화면에 출력하는 C언어 코드를 작성하시오.

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

## 10. 동적 메모리 할당(malloc)을 활용하여 정수 3개 공간을 할당받은 뒤, {11, 33, 55}를 저장하고 이들의 합을 출력(해제 포함)하는 C언어 코드를 작성하시오.

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

## 11. 다음 3명의 성적(국어 kr, 영어 en)을 구조체로 초기화하고 개인별 평균을 구하시오. 대상:J.C. Shim, G.D. Hong, J.Y. Ko 

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
