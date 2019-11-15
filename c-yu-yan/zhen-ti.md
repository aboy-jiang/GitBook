# 真题

## 2018

一、

1-5 ABCA 6-10

五、

1-5 ABCBD 6-10 BCBDD

六、

1.

{% code title="" %}
```c
int i, j, count = 0;
i = 0;
while(i < 100) {
    j = 100;
    while (j >=i) {
        count += j - i;
        j-=2;
    }
    i++;
}
```
{% endcode %}

2. 

```c
char *msg1; 
声明了一个指向字符串的指针变量，并没有在栈内存中分配任何内存
char msg2[20];
声明了一个长度为20的char类型数组
```

## 2017

DCBBC ACABD

## 2016

CCADC DDBAD

## 2015

六

```c
1.
k <= n
k++;

2.
a[i-1]
a[9-i]

3.
p = s[0]
p = s[i]

4. 对链表进行插入排序
*p > *r
p+1

5.
a[n-1]
p>=a

6.
return 1
return n + sum(n-1)

7.
-1
i

8.
fopen(argv[1], "wb")
ch, fout

9.
flag
!eof(fp)

10.
scanf("%f", &n)
fwrite(&n, sizeof(float), 1,fp);
```

## 2014

DBACA BDCA\_

七

```c
1.
a[k-1]
a[9-k]

2.
k / j == 0
break;

3.
substr[k] == '\0'
i+1

4.
*p == *q
*news = *old
news++

5.
fopen("file.bat", "r"))
fp, "%d", &num
i == count
```

## 2013

五

```c
1.
break
a

2.
a[2] >= a[1]
FUNC2(a, n-1)

3.
(p+i*N+i)
(q+i*N+9-i)

4.
i!=0
'0'+n%10

5.
ch = ch - ('a' - 'A') + 2
ch = ch - 'Z' - 1 + 'A';

6.
s[i]
c[t++]

7.
strlen(p)-1
p<q

8.

9.
6
&number

10.
argv[1], "rb"
argv[2], "wb"
```

## 2012

CDACB DADBA

七

```c
1.
50, &x

2.
i%2==0 ? 1 : -1
(2*i+1)

3.
c=c+5
c='a'+c-'v'

4.
*t
*s-*t

5.
str[3]=str2[j++]
str[2]!='\0'

6.
argc>1
*argv

7.
aw
r
fp2
fgetc(fp2)

8.
计算整数n的位数

9.
判断输入的字符串是否为回文

10.
在file.txt文件末尾写入“data”字符串，然后打印文件中字符个数
```

## 2011

1. ch\(1\)=65, ch\(2\)=B
2. 8
3. 2332
4. 11
5. 2
6. 354
7. Y=7
8. 9
9. 12
10. IF YOU FAIL TO P

## 2010

DCACD BBBDC CBADC DCDAB

## 2009

## 2008

## 2007

## 2006

## 2005

