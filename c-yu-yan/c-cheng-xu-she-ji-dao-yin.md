# C程序设计导引

### 3.1 闰年表达式

![](../.gitbook/assets/image%20%2814%29.png)

```c
/*
闰年：
（1）不能被100整除，且能被4整除
（2）能被100整除，且能被400整除（能被400整除，必定能被100整除）
*/
(y % 100 != 0 && y % 4 == 0) || (y % 400 == 0)
```

### 3.3 名次预测正确表达式

![](../.gitbook/assets/image%20%28106%29.png)

```c
/*
设A~F六名选手的预测名次为1~6，实际名次是a~f
利用真值等于1的特点
*/
a == 1 + b == 2 + c == 3 && d == 4 && e == 5 && f == 6
```

### 4.2 最大公约数

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
	printf("求两个整数a和b的最大公约数，输入a和b的值:\n");
	int a, b;
	scanf("%d %d", &a, &b);

	int i = 1, max_gcd;
	while (i <= a && i<= b) {
		if (a % i == 0 && b % i == 0) // i是a和b的一个公约数
			max_gcd = i;
		i++;
	}
	printf("%d和%d的最大公约数为：%d\n", a, b, max_gcd);
	return 0;
}
```

### 4.3 数据输入

![](../.gitbook/assets/image%20%2860%29.png)

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
	printf("Please input a 5-digit number.");
	int i;
	while (scanf("%d", &i) == 0 || i < 10000 || i > 99999) { // scanf为读入任何数据返回0
		printf("Please input a 5-digit numbner\n");
		while (getchar() != '\n');
	}
	printf("The 5-digit number of you inputing is %d\n", i);
	return 0;
}
```

![](../.gitbook/assets/image%20%2872%29.png)

### 4.4 行数统计

![](../.gitbook/assets/image%20%2846%29.png)

```c
int c, n = 0;
while ((c = getchar()) != EOF) {
    if (c == '\n') n++;
}
printf("%d lines", n);
```

### 4.8 输出提示信息，读入应答

```c
do {
    printf("Are you sure? (y/n)");
    c = getchar();
} while (c != 'y' && c != 'n')
if (c == 'y') 
...
else
...
```

### 4.10 连续正整数

![](../.gitbook/assets/image%20%2843%29.png)

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
	int n;
	do {
		printf("请输入一个正整数!\n");	
		scanf("%d", &n);
	} while (n <= 0);

	int i, j, temp, sum, count = 0;
	for (i = 1; i <= n/2; i++) {
		sum = i;
		for (j = i+1; sum < n; j++)
			sum += j;
		if (sum == n) {
			count++;
			printf("%d=%d", sum, i);
			for (temp = i+1; temp < j; temp++) 
				printf("+%d", temp);
			putchar('\n');
		} 
	}
	if (count == 0) {
		printf("NONE\n");
	}

	return 0;
}
```

### 4.12 乒乓球赛

![](../.gitbook/assets/image%20%2896%29.png)

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
	int A, B, C;
	for (A = 'X'; A <= 'Z'; A++) {
		for (B = 'X'; B <= 'Z'; B++) {
			for (C = 'X'; C <= 'Z'; C++) {
				if (A == B || A == C || B == C)
					continue;
				if (A != 'X' && C != 'X' && C != 'Z')
					printf("A <--> %c\nB <--> %c\nC <--> %c\n", A, B, C);
			}
		}	
	}
	return 0;
}
```

### 5.2 星期几 

![](../.gitbook/assets/image%20%2815%29.png)

```c
/*
用0-6表示星期一到星期日
从x到y增加天数 = 该月所剩余天数 + 下个月天数 = n - x + k 
所求结果 =（星期y + 从x到y增加天数）% 7 = (y + n - x + k) % 7
*/

int week_day(int x, int y, int n, int k) 
{
    return (y + n - x + k) % 7; 
}
```

### 5.3 最大公约数

```c
/*

*/
```

### 5.4 水仙花数

![](../.gitbook/assets/image%20%2820%29.png)

```c
int is_daffo(int i) 
{
    int a = i / 100 % 10;
    int b = i / 10 % 10;
    int c = i / 1 % 10;    
    return (i == a*a*a + b*b*b + c*c*c);
}

int main(int argc, char *argv[])
{
    int i;
    for (i=100; i<1000; i++)
        if (isdaffo(i))
            printf("%d\n",i);
    return 0;
}
```

### 5.5 π的近似值

![](../.gitbook/assets/image%20%2875%29.png)

### 5.6 判断整数的奇偶

![](../.gitbook/assets/image%20%2866%29.png)

```c
int is_even(int n) 
{
    return n % 2 == 0; 
}
```

