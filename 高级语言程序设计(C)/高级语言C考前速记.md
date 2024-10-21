## 知识点总结

* **'0'=48, 'A'=65, 'a'=97**
* **feof() 函数文件结束返回非 0**
* **int x; x== 0 与 !x 等价, x!=0 与 x 等价**
* **$e^x$ 对应的函数是 exp(double x)**
* 数组的第二维需要指定，第一维不需要
* (*p)[M] 表示指向数组(包含M个元素)的指针
* *p[M] 表示一个指针数组

### 大题：

**计算表达式近似值程序模板**

```c
#include <stdio.h>
#include <math.h>

#define EPS 1e-4

/**
 * 计算阶乘分支1
 * @param n
 * @return
 */
double fun(int n) {
    double result = 1.0;
    for (int i = 1; i <= n; i++) {
        result /= i;
    }
    return result;
}

int main() {
    double x, item, sum = 0;
    int sign = 1;

    int i = 0;

    printf("请输出x的值: \n");
    scanf("%lf", &x);

    do {
        item = pow(x, i) * fun(i);
        if (sign > 0) {
            sum += item;
        } else {
            sum -= item;
        }
        sign = -sign;
        i += 2;
    } while (item >= EPS);

    printf("计算结果为: %lf\n", sum);
}
```

**读取文件模版:**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    FILE *fp1, * fp2;
    char ch;
    if ((fp1 = fopen("old.txt", "r")) == NULL) {
        printf("error\n");
        exit(1);
    }
    if ((fp2 = fopen("new.txt", "w+")) == NULL) {
        printf("error\n");
        exit(1);
    }

    while (!feof(fp1) && ((ch = fgetc(fp1)) != -1)) {
        putchar(ch);
        if (ch >= '0' && ch <= '9') {
            ch = 'Z' - (ch - 48);
        }
        fputc(ch, fp2);
    }
    printf("\n");
    rewind(fp2);

    while (!feof(fp2) && ((ch = fgetc(fp2)) != -1)) {
        putchar(ch);
    }
    fclose(fp1);
    fclose(fp2);

    return 0;
}
```

