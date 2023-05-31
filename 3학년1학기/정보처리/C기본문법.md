# 기본문법

[toc]



### 입출력 - scanf, printf

``` c
#include <stdio.h>
 main()  {
      int  i, j, k;
      scanf(“%d %d”, &i, &j);  //  6 4
      k = i + j;
      printf(“%d\n”, k);
}
```



* 데이터를 입력 받을때 &i , &j로 받는데 C언어만 특별하게 주소에 다가 값을 담는다.




***



``` c
#include <stdio.h>
 main()  {
      int  n1 = 15, n2 = 22; 
     // 참고 : XOR : ^ , OR : | , AND : &
      n1 ^= n2;  //  25 
      n2 ^= n1;   // 15
      n1 ^=  n2;  // 22
     printf(“%d %d ”,n1, n2);
}

참고 : %d, %o. %x, %c, %s, %f
```



* 비트 연산자를 통해서 값을 바꾼다.

* 15는 이진수로 00001111

* 22는 이진수로 00010111

* 25는 이진수로 00011001

* XOR은 같으면 0 다르면 1이 된다.

  

  ***

  

  ``` c
  #include <stdio.h>
   main()  {
        int result, a=100, b = 200, c=300;
        result = a < b ?  b++ : --c;
        printf(“ %d, %d, %d\n”, result, b, c)
  } 
  ```

  

* 가운데는 삼항연산자이다 a<b가 트루면 ? 뒤에 있는 b++을 실행하고 false 면 --c 를 한다.

* b가 a보다 더크므로 b++을 한다 

* 이것을 바탕으로 프린트 문을 찍으면 200,201,300이 출력된다.

* b++은 후위연산자 이기 때문에 b의 값을 result에 먼저 담은후 b의 값이 1증가 한다. 그러므로 result에는 200이 담기고 b는 201이 된다.



***



``` c 
#include <stdio.h>
 main()  {
      int  m , n; 
     scanf(“%o#%x”, &n, &m); // 입력 15#22
     printf(“%d %d ”,n, m);
}
```



* scanf에서 15,22를 입력하게되면 n의 15를 읽을때 8진수로 받고, 22를 읽을때 16진수로 읽는다.

* 그러므로 n과m을 출력을 했을때 15의 8진수인 13으로 나오고 m은 22의 16진수인 34로 나온다.

  

  ***

  

  ``` c
  #include <stdio.h>
   main()  {
        int  j=024, k=24, L=0x24, hap; 
        hap = j + k + L;
  printf(“%d, %d, %d, %d ”,k j, k, L, hap);
  } 
  ```

  

* 8진수 아닌이상 맨앞에 0이 나올 수가 없다.
* 맨앞에 0을 적으면 숫자로 인식한다.
* j는 8진수로 24로 읽어들인다. (10진수로는 20)
* L은 16진수로 24를 읽어서 36이 저장된다.
* 총합적으로는 20 + 24+36이 되므로 80이 출력된다.



***



``` c
#include <stdio.h>
 main()  {
      int  a=5, b=10, c=15, d=20, result; 
      result = a * 3 + b > d || c – b / a <= d && 1;
      printf(“%d\n”, result);
}   //  1
// 15 , 2 , 25, 13, 거짓, 참, 참, 참
```



* 연산자의 우선순위에 관련된 문제다.
* 수치 연산자(+,-,*,/) -> *,/의 순위는 같고 동시에있으면 앞에서부터 순서적으로 계산
* 논리 연산자(!, && , ||) -> not , && , ||순으로 계산하면 된다. 
* C언어에서 0만 false고 그 외의 숫자는 true다.
* 관계연산자 (<,>,=)  -> 대소관계는 순차적으로 판별  



***



### 제어문



``` c
#include <stdio.h>
 main()  {
      int score[] = { 86, 53, 95, 76, 61 };
      char grade, str[]=“Rank”;
      for ( int i= 0; i < 5; i++) {
            switch (score[i]/10) {
                  case 10:   case 9:            grade = ‘A’;          break; 
                  case 8:               grade = ‘B’;          break; 
                  case 7:               grade = ‘C’;          break; 
                  default:             grade = ‘F’;
               }
          if (grade != ‘F’) printf(“%d is %c %s \n, i+1, grade, str);
          }
 } 
```



* 본인의 성적에 따라 본인의 등급이 나오는 코드다. 
* 본인의 성적이 F면 출력이 되지 않는다.
* C에는 String이 존재하지 않아서 char을 많이 사용한다.



***



``` c
#include <stdio.h>
main() {
     int i = 1, n = 0;
     while (i <=50) {
         if (i % 7 == 0) n+= i;
         i++;
      }
      printf("%d", n);
} 
```

* i를 7로 나눈나머지가 0 이면 n + i값을 진행해라.
* n값 출력



***



``` c
#include <stdio.h>
main() {
     int arr[6];
     int max = 0, min = 99;
     int sum = 0;
     for (int i = 0; i < 6; i++) {
          arr[i] = i * i; //  0, 1, 4, 9, 16, 25
          sum += arr[i]; //  55
      } for (int i = 0; i < 6; i++) {
             if (max < arr[i])  max = arr[i]; //  25
             if (min > arr[i])  min = arr[i];  //  0
     }
     printf("%.2f", (sum-max - min) / 4.0);
}  
```



* 정답이 잘못되어있음 5.5가 아닌 7.50가 나온다.

* %.2f를 하면 소수점 2자리 까지 출력이므로 7.50이 나와야한다.




***



``` c
#include <stdio.h>
main() {
     int i = 1, n = 0;
     while (i <=50) {
         if (i % 7 == 0) n+= i;
         i++;
      }
      printf("%d", n);
} // 0 +
```



* a 와 b를 i로 나눈 값이 0 이 동시에 되는 시점에 g에 i값을 저장한다.
* 그 후 a과b의 값을 곱한후 g로 나눈 값을 L에 저장한다.
* 그리고 g와L을 더한값을 출력한다.



***



``` c
#include <stdio.h>
main() {
    int a = 27, b = 12;
    int L, g;      
    for (int i = b; i > 0; i--) {
    if (a % i == 0 && b % i == 0) {
    g = i;   //  3
    break;
    }
    }
    L = a * b / g; //   27 * 12 / 3
    printf("%d", g + L);
} //
```



* 1~35중 짝수와 홀수의 갯수를 더하는 문제다.



***



``` c
#include <stdio.h>
main() {
    int n = 3, r = 0;
    for (int i=1; i < 10; i = i + 2)  r = r + n * i;
    printf("%d", r);
} 
```





* 누적합계를 출력하는 문제
* 3을 1,3,5,7,9를 각각 곱한거를 출력한다.



***



``` c
#include <stdio.h>
main() {
int a[3][5] = { {27, 13, 21, 41, 12}, 
                            {11, 20, 17, 35, 15},
                            {21, 15, 32, 14, 10} };
int sum, ssum = 0;
for (int i = 0; i < 3; i++) {
sum = 0;
for (int j = 0; j < 5; j++)  sum += a[i][j];
ssum += sum;
}
printf("%d", ssum);
}
```



* 이중배열에 있는 값을 다 누적해서 출력하는 문제다.



***



### 포인터 *,&

``` c
#include <stdio.h>
    main() {
        int a = 50;
        int *b = &a;
        *b= *b+ 20:
        printf("%d %d\n", a, *b); //  70  70
        char *s;
        S = ="gilbut";
        for (int i = 0; i < 6; i += 2) {
        printf("%c, ", s[i]); //  g, g, gilbut
        printf("%c, ", *(s + i)); //  l, l, lbut
        printf("%s\n", s + i); // u, u, ut
    }
}
```



* b는 정수형 포인터다. b는 a의 주소 값을 가진다.

* *b = *b +20은 b가 담고있는 주소의 값을 20을 더한다. 그러면 a 주소를 찾아가서 a의 값에 20을 더한다.  -> 즉 a값도 증가가 됨 50에서 70이 된다.

* C에서는 ++, -- 연산자가 1증가 1감소라고 하면안된다. 포인터 개념때문에 다음주소로 넘어가라 이전주소로 넘어가라라는 식으로 작동이 되면 값이 달라질 수 있다. 

* P라는 포인터 용어가 존재한다. 

* C에서 문자열은 첫번째 주소부터 맨마지막에 존재하는 null이 나올때까지로 인지한다. 그래서 끝이 어디인지 모른다.

  

  ***

  

  ``` c
  #include <stdio.h>
      main() {
          char a[3] [5] = { "KOR", "HUM", "RES" };
          char* pa[] = { a[0], a[1], a[2] };
          int n = sizeof(pa) / sizeof(pa[0]);
          for (int i = 0; i < n; i++)  printf("%c", pa[i][i]);
  } //  
  ```

  

* pa[] = {a[0], a[1],a[2]}를 하게되면 char a의 kor hum res에서 각각의 첫번째 문자의 주소를 가르키게된다

* a[0]의 경우에는 kor의 k를 시작주소를 가르킨다.

* a[1]의 경우에는 hum의 h를 시작주소로 가르킨다.

* a[2]의 경우에는 res의 r를 시작주소로 가르킨다.

* int n = sizeof(pa)/sizeof(pa[0])의 경우에는

* sizeof는 해당 메모리의 주소의 크기값을 리턴한다 

* char은 2바이트이고 pa는 char의 배열이면서 3개의 공간이 존재하기 때문에 6 바이트다.

* pa[0]은 char 이므로 2바이트다. 



***



``` c
 #include <stdio.h>
main() {
char *p = "KOREA";
printf("%s\n", p);      // KOREA
printf("%s\n", p + 3); //  EA
printf("%c\n", *p); //  K
printf("%c\n", *(p + 3)); // E
printf("%c\n", *p + 2); // M
}
```

* %s에 p+index를 더하게 되면 해당 위치부터 시작해서 끝까지 출력을하게 된다. 
* %c는 한글자 출력이므로 p+index를 하게되면 해당 자리의 값 한글자만 출력한다.



***



``` c 
#include <stdio.h>
    int main() {
        int ary[3];
        ints=0;
        *(ary+ 0) = 1; //   1
        ary[1] = *(ary+ 0) + 2; //   3
        ary[2] = *ary + 3:  //   4
        for (int i = 0; i < 3; i++)  s = s + ary[i];
        printf("%d", s);
}
```



* *(ary+0) 이말은 ary[0] 과 같은말이다.
* ary[1] = *(ary+0) +2 은 ary[1] = ary[0]+2 로 바꿔 이해할 수 있다.
* ary[2] = *ary +3은 ary의 첫번째 변수값 즉 ary[0]의 값을 가져와서 더한다. ary[2] = ary[0]+3



***



``` c
#include <stdio.h>
	int main(){
        int * array [3];
        int a = 12, b=24, c=36;
        array[0] = &a; //   a의 주소
        array[1] = &b; //  b의 주소
        array[2] = &c; //   c의 주소
        printf("%d", *array[1]+ **array+ 1); //   24 + 12 +1
} 
```



* **array는 array 배열의 첫번쨰 포인터가 가리키는 정수의 값이다 -> 12 
* array에 a,b,c,의 주소를 넣는다.
* printf할때 주소가 저장한 값을 다 더해서 출력한다.



# 구조체

**여러가지 자료형을 하나로 만드는 것을 구조체라 한다.**



``` c
#include <stdio.h>
    struct jsu {
        char nae[12];
        int os, db, hab, hhab;
    }
     int main() {
        struct  jsu st[3] = { {“데이터1”, 95, 88} , {“데이터2”, 84, 91} , {“데이터3”, 86, 75}}; 
        struct jsu* p;
        p = &st[0];
        (p+1) ->hab = (p+1)->os + (p+2)->db;  // 159
        (p+1) ->hhab = (p+1)->hab + p->os + p->db; // 342
        printf(“%d”, (p+1)->hap + (p+1)->hhab); // 159 + 342 = 501
} 
```



struct는 구조체 라는 의미를 나타낸다.

struct jsu st[3] 을하면 jsu라는 구조체 통체로 담는 배열3개가 선언이 되고 그 안에 데이터를 넣었는데

char nae에 데이터1이 들어가고 int os에 95 db에 88등 순서대로 데이터가 적재가된다.

항목이 없는애들은 안들어가게 된다.



(p+1) -> hab 를 하면 st의 첫번째 위치에 존재하는 데이터의 hab를 호출한다.

그러므로 (p+1) -> hab = (p+1) os + (p+2) -> db 의 경우에는 데이터2의 84값 + 데이터3의 75값을 더한다는 말이다.



***



### 구조체 -1



```  c
#include <stdio.h>
int main() {
    struct insa {
        char name[10];
        int age;
    } a[0] = { “Kim”, 28 , “Lee”, 38, “Park”,42, “Choi”, 31}; 
    struct insa* p;
    p = a;
    p++;
    printf(“%s\n”, p->name); // Lee
    printf(“%d\n”, p->age); // 38
} 
```

일단 a[0] 의미파악해보기

struct insa * p하면 구조체 insa를 담는 구조체 포인트변수가 생성된다.

p에 a를 담고 p++을하면 p의 0번쨰엔 kim 28이 담기고 1번째엔 Lee 38이 담기고 2번쨰엔 choi 31이 담긴다.

초반에 p가 0이므로 p++을 한후 p가 가르키는 곳의 이름을 부르면

Lee가 호출되고 p가 가르키는곳의 age를 호출하면 38이 나온다.



***

### 사용자 정의 함수 -1



``` c
#include <stdio.h>
 int factorial(int n); 
 int main() {
 int (*pf)(int); 
 pf = factorial;
 printf(“%d”, pf(3));    // printf(“%d”, factorial(3)); 
 } 
 int factorial(int n) {
    if (n<=1) return 1;
    else return n * factorial(n-1);
 } 
```



int factorial(int n){} 의 함수는 함수포인터 이며 int를 return 해줘야한다.

int (*pf)(int); 를 사용하게되면 factorial 포인터 함수를 pf에 담을 수 있다.

그 후 pf(3) 요렇게하면 자바에서 factorial(3)을 하는것과 값이 같게 나온다.



***



### 사용자 정의 함수 -2



```c
 #include <stdio.h>
 #include <math.h>
 main() {
      int arr[5];
      for (int i = 0; i < 5; i++)  arr[i] = (i + 2) +(i * 2); // 2 5 8 11 14
      for (int i = 0; i < 5; i++)  printf("%d", check(arr[i])); // 1 1 0 1 0
 }
 int check (int a) {
      int n = (int) sqrt(a);
      int i = 2; 
      while (i <= n) {
             if (a % i == 0) return 0;
             i++;
       }
       return 1;
 }
```



arr 배열에 2 5 8 11 14를 담은후

check 라는 포인터 함수에 arr 배열값을 하나하나 집어넣는다

넣은값을 제곱을 씌운후 제곱근의 값이 i보다 클경우에만 해당 값이 i로 나누어진다면 0을 리턴하고

아닌경우 i를 1증가 시킨후 다시 i가 n보다 작거나 같은지 판별후 while문을 돌아가고 

만약 i가 n보다 크게될 경우 1을 리턴함

즉 결과값이 1로 출력되는 애들은 i로 나눠지지 않고 i보다 작아져서 1이 리턴된애들이고

0이 된애들은 i로 나눠서 0이 나온애들이다.



***



### 사용자 정의 함수 - 3



``` c
#include <stdio.h>
func (int *p) {
     printf("%d\n", *p);
     printf("%d\n", p[2]);
}
main() { 
     int a[7] = {1,2,3,4,5 };
     func(a);
     func(a + 2);
}
```







***



### 사용자 정의 함수 - 4



```C 
#include <stdio.h>
void align (int a[]) {
    int temp;
    for (int i = 0; i < 4; i++)
         for (int j = 0; j < 4 - i; j++) 
              if (a[j] > a[j+1]) {
                  temp = a[j];
                  a[j] = a[j+1];
                  a[j+1] = temp;
             }
     }    
main() {
    int a[] = { 85, 75, 50, 100, 95 };
    align (a);
    for (int i = 0; i < 5; i++)  printf("%d ", a[i]);
}
```



***



### 사용자 정의 함수 -5



```C 
#include <stdio.h>
int r1() {
       return 4;
}
int r10() {
       return (30+ r1());
}
int r100() {
       return (200 + r10());
}
int main() {
        printf("%d\n", r100() );
        return 0;
}
```

