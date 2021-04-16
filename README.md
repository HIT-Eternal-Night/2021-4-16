# 2021-4-16
指针、字符串练习！前进！

1、从键盘任意输入一个字符串(可以包含：字母、数字、标点符号，以及空格字符)，计算其实际字符个数并打印输出，
即不使用字符串处理函数strlen()编程，但能实现strlen()的功能。
程序运行示例：
Please enter a string:how are you↙
The length of the string is: 11
程序如下，横线处代表有缺失的源代码，请补充缺少的部分，并将完整的程序代码填写在答题区。

#include  <stdio.h>
___________ /*  函数声明  */
int main()
{
	char   a[80];
	unsigned int  len;
	printf("Please enter a string:");
	___________   /*   输入字符串   */
	 ___________      /* 调用函数，计算字符串实际字符个数 */
	printf("The length of the string is: %u\n", len); 
	return 0;
}

/* 函数功能：用字符指针作函数参数，计算字符串的长度 */
unsigned int  MyStrlen(char *pStr)
{ 
	___________      /* 声明计数变量 */
	for ( ______ ;_______  ;________)       /* 循环控制条件  */
	{
		len++;                 /* 统计不包括'\0'在内的字符个数 
	}
	        ___________       /* 返回实际字符个数 */
}

我的答案：
#include  <stdio.h>

unsigned int  MyStrlen(char *pStr);/*  函数声明  */

int main()
{
	char   a[80];
	unsigned int  len;
	printf("Please enter a string:");
	gets(a);  /*   输入字符串   */
	len = MyStrlen(a);    /* 调用函数，计算字符串实际字符个数 */
	printf("The length of the string is: %u\n", len); 
	return 0;
}

/* 函数功能：用字符指针作函数参数，计算字符串的长度 */
unsigned int  MyStrlen(char *pStr)
{ 
	int len = 0;      /* 声明计数变量 */
	for ( len = 0 ; *pStr != '\0'  ; pStr++)       /* 循环控制条件  */
	{
		len++;                 /* 统计不包括'\0'在内的字符个数 */
	}
	        return len;       /* 返回实际字符个数 */
}

总结：字符串的输入与输出方式：
一、
  char str[10];
	int i;
	for (i=0 ; i<10 ; i++)
	{
		scanf("%c",&str[i]);
	}
	for (i=0 ; str[i]!='\0' ; i++)
	{
		printf("%c",str[i]);
	}
说明：这种方式的输入必须输入9个字符才能结束，但输出灵活，无论字符串中的字符数是已知的还是未知的都可采用。

二、
	char str[10];
	scanf("%s",str);
	printf("%s",str);
说明：用%d输入数字或%s输入字符串时，忽略空白字符（空格、回车符或制表符）（它们被作为数据的分隔符）。
读到这些字符时，系统认为数据读入结束，因此用scanf按s格式符不能输入带空格的字符串。

三、使用字符串处理函数gets(),可以输入带空格的字符串，因为空格和制表符都是字符串的一部分。
此外，函数gets()和scanf()对回车符的处理也不同。gets()以回车符作为字符串的终止符，
同时将回车符从输入缓冲区读走，但不作为字符串的一部分。而scanf()不读走回车符，回车符仍留在输入缓冲区中。
函数puts()用于从括号内的参数给出的地址开始，依次输出存储单元中的字符，当遇到第一个‘\0’时输出结束，并且自动输出一个换行符。
函数puts()输出字符串简洁方便，唯一不足是无法输出其他字符信息并控制输出格式。
只需#include<stdio.h>即可

四、上述输入方式都存在安全隐患，很容易引起缓冲区溢出。
建议使用下面的能够限制输入字符串长度的函数：
fgets(name,sizeof(name),stdin);
终止条件：①读入n-1个字符②遇到第一个换行符
原理：①终止在末尾添加一个空字符。
           ②终止保留换行符再在末尾添加一个空字符。 
返回值：当读到文件末尾时返回空指针。
	char str[10];
printf("Please enter a string:");
	fgets(str,sizeof(str),stdin);
	puts(str);

2、下面程序的功能是删除字符串中第一次出现的a字符。其中有两处错误，请改正并使程序正确执行。
#include <stdio.h>
#include <string.h>
void fun(char *s,int n,int *t)
{
    int i,k=0;
    s[n]='a';
    s[n+1]='\0';
    while(s[k]!='a') k++;
    if(k==n){*t=0;}
    else
    {
        for(i=k;i<n;i++)
            s[i]=s[i+1];
        s[i]='\0';
    }
}
main()
{
    char s[20];
    int len,t;
    printf("Input a string:");
    gets(s);
    len=strlen(s);
    fun(s,len,t);
    if(t==0) printf("Not exist!\n");
    else    printf("Result is:%s\n",s);
}

我的答案：
#include <stdio.h>
#include <string.h>
void fun(char *s,int n,int *t)
{
    int i,k=0;
    s[n]='a';
    s[n+1]='\0';
    while(s[k]!='a') k++;
    if(k==n){*t=0;}
    else
    {
        for(i=k;i<n;i++)
            s[i]=s[i+1];
        s[i-1]='\0';
    }
}
int main()
{
    char s[20];
    int a = 1;
    int len,*t = &a;
    printf("Input a string:");
    gets(s);
    len=strlen(s);
    fun(s,len,t);
    if(*t==0) printf("Not exist!\n");
    else    printf("Result is:%s\n",s);
}

总结：
指针的初始化问题：初学者最常见的问题就是定义了一个指针变量，还没有让它指向东西，
就开始对其赋值。
