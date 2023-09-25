# [한 번에 네 글자 받기]
unsigned int 자료형의 크기는 4바이트이다.

이 자료형에 1바이트인 문자를 네 개 저장할 수 있다.


unsigned int 크기의 수를 받고, 문자열을 출력하시오.

입력 설명
unsigned int 범위의 수가 하나 입력된다.

출력 설명
해당 수의 각 바이트 별 문자 네 개를 출력하시오.

입력 예시 복사
1735348036
출력 예시 복사
DOog
```
#include<stdio.h>
int main() {
	unsigned int a = 0;
	char a1, a2, a3, a4 = 0;
	int bina[32];
	scanf("%u", &a);
	for (int i = 31; i >= 0; i--) {
		bina[i] = (a >> i) & 1;
	}
	a1 = bina[7] * 128 + bina[6] * 64 + bina[5] * 32 + bina[4] * 16 + bina[3] * 8 + bina[2] * 4 + bina[1] * 2 + bina[0];
	a2 = bina[15] * 128 + bina[14] * 64 + bina[13] * 32 + bina[12] * 16 + bina[11] * 8 + bina[10] * 4 + bina[9] * 2 + bina[8];
	a3 = bina[23] * 128 + bina[22] * 64 + bina[21] * 32 + bina[20] * 16 + bina[19] * 8 + bina[18] * 4 + bina[17] * 2 + bina[16];
	a4 = bina[31] * 128 + bina[30] * 64 + bina[29] * 32 + bina[28] * 16 + bina[27] * 8 + bina[26] * 4 + bina[25] * 2 + bina[24];

	printf("%c%c%c%c", a1, a2, a3, a4);


	return 0;
}
```
# [ 파형 읽어내기 ]

정보를 담은 전자기파가 전선을 통해 흘러온다.

HIGH/LOW를 구분하며 한 비트 한 비트를 읽어 모으면,
비로소 모든 정보가 모인 수를 얻을 수 있게 된다.
입력 설명
첫째 줄에 정수 n이 입력된다. (1 <= n < 10)
둘째 줄에 n*8개의 문자가 입력된다. 각 문자는 '-' 또는 '_'이며,
'-'는 1을 '_'는 0을 의미한다.
출력 설명
해석을 완료한 n개의 수를 출력하라. 부호없는 1바이트 정수이다.
입력 예시 복사
3
-_-_-_-_________----____
출력 예시 복사
170 0 240
```
int main() {
	int n;

	scanf("%d", &n);

	char bina[80]; 
	scanf("%s", bina);

	for (int i = 0; i < n; i++) {
		unsigned char result = 0; 

		for (int j = 0; j < 8; j++) {

			if (bina[i * 8 + j] == '-') {
				result = result | (1 << (7 - j));
			}
		}
		printf("%u ", result); 
	}

	return 0;
}
```

# [ 모세의 기적 ]

0~255 사이의 숫자 data와, 0~4사이의 숫자 n이 주어질 때,
data의 중심을 양쪽으로 n칸씩 가른 수를 출력하시오.

예를 들어, 170과 1이 주어진다면,
1010_1010 -> 0100_0101
69를 출력해야한다.

입력 설명
data와 n이 공백으로 구분되어 입력된다.
출력 설명
설명과 같은 연산을 한 결과를 출력하시오

```
int main() {
	unsigned int data;
	int n;

	scanf("%u %d", &data, &n);

	unsigned char num1, num2;
	num1 = data & ~32767;
	num2 = data & 32767;

	num1 = num1 << n;

	num2 = num2 >> n;

	num1 = num1 | num2;

	printf("%u", num1);

	

	return 0;
}
```
# [암호화2]


문제 설명:

int 변수의 첫 바이트와 네번 째 바이트의 위치를 바꿔 저장하고

두번 째 바이트와 세번 째 바이트의 위치를 바꿔 저장하는 방식으로

암호화를 하고자 한다.

즉, 네 바이트의 순서를 뒤집는다.


예를 들어 0x543210ff를 0xff103254로 변환하는 것이다.


위와 같은 작업을 실행하여 결과를 출력하는 프로그램을 작성하시오.

입력 설명
unsigned int 범위의 10진수가 하나 주어진다.

출력 설명
위와 같은 과정을 거쳐 암호화된 수를 10진수로 출력하시오.

입력 예시 
305419896
출력 예시 
2018915346

```
#include <stdio.h>

int main() {
	unsigned int num;


	scanf("%u", &num);

	unsigned char a1 = (num >> 24) & ~0;
	unsigned char a2 = (num >> 16) & ~0;
	unsigned char a3 = (num >> 8) & ~0;
	unsigned char a4 = num & ~0;

	
	unsigned int result = (a4 << 24) | (a3 << 16) | (a2 << 8) | a1;

	
	printf("%u", result);

	return 0;
}
```
#[진법 변환기]

10진수 N과 임의의 수 X( 2 <= X < 10 )가 공백으로 구분되어 입력된다.
N을 X진수로 변환한 결과를 출력하시오.
X진수는 0부터 X개의 숫자를 이용하여 수를 나타낸다.
예를 들어, 2진수는 0부터 두 개이므로 0과 1만을 사용하여 나타낸다.
3이라면 2진수로 11이 된다. (1 * 2^1 + 1 * 2^0)
3은 3진수로 10이다. (1 * 3^1 + 0 * 3^0)
5는 3진수로 12이다. (1 * 3^1 + 2 * 3^0)

입력 설명
unsigned int 범위의 수 N과 X가 공백으로 구분되어 주어진다.

출력 설명
N을 X진수로 변환한 결과를 출력하시오.

입력 예시 복사
65535 2
출력 예시 복사
1111 1111 1111 1111

입력: 10 9
출력: 11

입력: 81 9
출력: 100

입력: 65535 8
출력: 177777

입력: 32768 5
출력: 2022033

입력: 1688213 7
출력: 20230622
```
#include<stdio.h>
int main() {
	int a, b;
	int arr[32] = {0,};

	scanf("%d %d", &a, &b);

	for (int i = 0;i < 32;i++) {
		arr[i] = a % b;
		a = a / b;

	}
	int cnt = 0;

	for (int i = 0;i < 32;i++) {
		if (arr[31 - i] ) {
		
			break;
		}
		cnt++;
	}
	for (int i = cnt;i < 32;i++) {
		printf("%d", arr[31 - i]);

	}



	return 0;
}
```
# 3주차 테스트(0922) + 숙제제
# [모세의 기적2]

unsigned int 범위의 data와, 0~16사이의 숫자 n이 주어진다.
data의 중심을 기준으로 양쪽으로 n칸씩 시프트 연산한 결과를 16진수로 출력하시오.

data의 중심이란, 16번 비트와 15번 비트 사이를 의미한다.

예를 들어, 0x35AFAB96과 3이 주어진다면,
00110101_10101111_10101011_10010110
-> 10101101_01111000_00010101_01110010
이므로, 0xAD781572를 출력해야한다.
입력 설명
data와 n이 공백으로 구분되어 입력된다.
단, data는 16진수로 주어진다.
출력 설명
연산한 결과를 16진수 형태로 출력하시오.
입력 예시 복사
35AFAB96 16
출력 예시 복사
0
```#include<stdio.h>
int main() {

	unsigned int data = 0;
	int n = 0;
	scanf("%xu %d", &data, &n);

	unsigned int a1, a2 = 0;

	a1 = data & 256+ 256^2;
	a2 = data & ~(256 + 256 ^ 2);

	a1 = a1 << n;
	a2 = a2 >> n;

	a1 = a1 | a2;

	printf("%u", a1);


	return 0;
}
```
# [비트를 그림으로]

unsigned int 크기의 정수 하나를 입력받아,
해당 정수의 비트를 그림으로 변환하여 출력하시오.

정수의 각 비트가 1이면 @, 0이면 O으로 변환하여 1 x 32 크기의 그림을 출력한다.

예를 들어, 4294967294의 비트 표현은
11111111_11111111_11111111_11111101이므로
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@O@를 출력한다.
```
#include<stdio.h>
int main() {

	int a[32];
	int n = 0;
	scanf("%d", &n);

	for (int i = 31; i >= 0; i--) {
	a[31 - i] = (n >> i) & 1;

	}


	for (int i = 0; i <32; i++) {
		if (a[i] == 1) {
			printf("@");

		}
		if(a[i]!=1) {
			printf("O");
		}
		

	}
	
	return 0;
}
```
# [한글인가 알파벳인가 그것이 문제로다]

한글 또는 알파벳 한 글자가 입력된다.
입력된 글자가 영어라면 "english"를,
한글이라면 "한글"을 출력하시오.

입력 설명:
한글 또는 알파벳 한 글자가 입력된다.

출력 설명:
입력된 글자가 영어라면 "english"를,
한글이라면 "한글"을 출력하시오.
```
#include<stdio.h>
int main() {
	unsigned char str[3];

	scanf("%s", &str);

	if (str[0] >= 32 && str[0] < 128) {
		printf("english");
	}
	else {
		printf("한글");
	}

	return 0;
}
```

# [비트 셋팅]

unsigned int 범위의 정수 n과, 0 ~ 31 사이의 정수 x가 주어진다.
정수 n의 x번 비트를 1로 바꾼 결과를 출력하시오.
```
#include<stdio.h>
int main() {
	unsigned char a = 0;
	unsigned int x;

	scanf("%hhu %u", &a, &x);

	unsigned char mask = ~(1 << x);

	a = a & mask;

	printf("%hhu\n", a);

	return 0;
}
```

# [비트열 추출하기]

unsigned char 범위의 정수 n이 주어진다.
정수 n의 5번 비트부터 2번 비트까지를 추출하여
추출한 4비트를 16진수 한 자리로 출력하시오.
```
#include<stdio.h>
int main() {
	int a[8];
	unsigned char n = 0;
	scanf("%hhu", &n);

	for (int i = 7; i >= 0; i--) {
		a[7 - i] = (n >> i) & 1;

	}
	

	int sum;
	sum = a[2] * 8 + a[3] * 4 + a[4] * 2 + a[5];

	printf("%X", sum);

	return 0;
}
```

# [특수한 16진수]

unsigned char 변수의 크기는 1바이트(8비트)이다.
16진수 한 자리는 4비트의 크기를 표현할 수 있으므로, 
unsigned char 변수는 각각 4비트씩 두 자리의 16진수로 표현할 수 있다.

예를 들어, 0111_1010 은
0111 -> 7
    1010 -> A
01111010 -> 7A 로 표현된다.

만약, 같은 unsigned char 변수 값을 앞에서부터 4비트씩 차례로 읽어 변환한다면, 
아래와 같이 5자리의 16진수로 변환할 수 있다.

0111 -> 7
 1111 -> F
  1110 -> E
   1101 -> D
    1010 -> A
01111010 -> 7FEDA 로 표현된다.

위와 같은 방법으로 변환하여 출력하는 프로그램을 작성하시오.
```
#include<stdio.h>
int main() {
	unsigned char a;
	int bit[8];

	scanf("%hhd", &a);
	for (int i = 7; i >= 0; i--) {
		bit[7 - i] = (a >> i) & 1;

	}

	int arr[5];
	arr[0] = bit[0] * 8 + bit[1] * 4 + bit[2] * 2 + bit[3];
	arr[1] = bit[1] * 8 + bit[2] * 4 + bit[3] * 2 + bit[4];
	arr[2] = bit[2] * 8 + bit[3] * 4 + bit[4] * 2 + bit[5];
	arr[3] = bit[3] * 8 + bit[4] * 4 + bit[5] * 2 + bit[6];
	arr[4] = bit[4] * 8 + bit[5] * 4 + bit[6] * 2 + bit[7];


	int cnt = 0;
	for (int i = 0;i < 5;i++) {
		if (arr[i] == 0) {
			cnt++;
		}
		else { 
			break;
		}
	}
	if (cnt == 5) {

		printf("0");
	}


	for (int i = cnt;i < 5;i++) {
		if (arr[i] < 10) {
			printf("%d", arr[i]);
		}
		else {
			printf("%c", 'A' + (arr[i] - 10));
		}
	}
	return 0;
}
```

# [암호화 1]

비트 XOR을 사용하면 암호화를 할 수 있다.

1로 xor연산을 하면 무조건 반전되고,
0으로 xor연산을 하면 무조건 유지된다.

이미 xor 연산으로 암호화된 1byte 크기의 data와
암호화에 사용된 1byte 크기의 key가 주어질 때,
원래의 data는 무엇이었는지 출력하시오
```#include<stdio.h>
int main() {
	unsigned char data, key;

	scanf("%hhd %hhd", &data, &key);

	unsigned char result = data ^ key;

	printf("%u", result);
	return 0;
}
```
# [패턴찾기]
unsigned char 범위의 정수 n과, 3비트 크기의 정수 x가 입력된다.
2진수 표현에서 정수 n에 비트 패턴 x가 몇번 나타나는지 출력하시오.

예를 들어, 247과 7이 주어졌다면,
11110111
111
 111
     111
이므로 정수 n에는 비트 패턴 x가 3번 나타난다.

입력 설명:
정수 n과 x가 공백으로 구분되어 입력된다.

출력 설명:
정수 n에 x가 나타난 횟수를 출력하시오.
```
#include<stdio.h>
int main() {
	unsigned char n,x;
	scanf("%hhu %hhu", &n, &x);

	int cnt = 0;
	int bit1[8];
	int bit2[8];

	for (int i = 7; i >= 0; i--) {
		bit1[7 - i] = (n >> i) & 1;
		
	}
	for (int i = 7; i >= 0; i--) {
		bit2[7 - i] = (x >> i) & 1;
		
	}
	
	for (int i = 0; i < 6; i++) {
		if (bit1[i] == bit2[5]) {
			if (bit1[i+1] == bit2[6]) {
				if (bit1[i+2] == bit2[7]) {
					cnt++;
				}
			}
		}
	}

	printf("%d", cnt);

	return 0;
}
```

# [진법 변환기2]

양의 정수 N과 X가 공백으로 구분되어 입력된다.
여기서 X(2 <= X < 10)는 정수 N이 X진수임을 의미한다. 

정수 N을 10진수로 변환한 결과를 출력하시오.


N을 10진수로 변환한 결과는 unsigned int 범위에 있다.

입력 설명
정수 N과 X가 공백으로 구분되어 입력된다.
출력 설명
정수 N을 10진수로 변환한 결과를 출력하시오.
```
#include <stdio.h>
#include <string.h>

int main() {
	char N[100]; 
	unsigned long long X;
	scanf("%s %llu", N, &X);

	unsigned long long result = 0;
	unsigned long long pos = 1;

	int len = strlen(N);

	for (int i = len - 1; i >= 0; i--) {
		unsigned long long num;
		if (N[i] >= '0' && N[i] <= '9') {
			num = N[i] - '0';
		}
		else {
			num = N[i] - 'A' + 10;
		}
		result += num * pos;
		pos *= X;
	}

	printf("%llu\n", result);

	return 0;
}
```
```
#include <stdio.h>

int main() {
	unsigned long long N;
	unsigned long long X;
	scanf("%llu %llu", &N, &X);

	unsigned long long result = 0;
	unsigned long long pos = 1;

	while (N > 0) {
		unsigned long long num = N % 10;
		result = result +  (num * pos);
		pos = pos * X;
		N = N/10;
	}

	printf("%llu", result);

	return 0;
}

```
# [암호화4]

unsigned int 크기의 data와, unsigned char 크기의 key가 주어진다.
data의 모든 바이트에 key를 xor한 결과를 출력하시오.
```
#include<stdio.h>
int main() {
	unsigned int data;
	unsigned char key;

	scanf("%u %hhd", &data, &key);


	unsigned int a1 = data & 0xFF000000;
	a1 = (a1 >> 24) ^ key;
	unsigned int a2 = data & 0x00FF0000;
	a2 = (a2 >> 16) ^ key;
	unsigned int a3 = data & 0x0000FF00;
	a3 = (a3 >> 8) ^ key;
	unsigned int a4 = data & 0x000000FF;
	a4 = a4 ^ key;
	unsigned int result = (a1 << 24) | (a2 << 16) | (a3 << 8) | a4;
	printf("%u", result);

	return 0;
}
```

# [암호화 2]

int 변수의 첫 바이트와 세번 째 바이트의 위치를 바꿔 저장하고
두번 째 바이트와 네번 째 바이트의 위치를 바꿔 저장하는 방식으로
암호화를 하고자 한다.

예를 들어 0x543210ff를 0x10ff5432로 변환하는 것이다.

위와 같은 작업을 실행하여 결과를 출력하는 프로그램을 작성하시오.
```
#include <stdio.h>

int main() {
	unsigned int input;
	unsigned int result;

	scanf("%u", &input);

	
	result = ((input & 0x000000FF) << 16) | ((input & 0x00FF0000) >> 16) |
		((input & 0x0000FF00) << 16) | ((input & 0xFF000000) >> 16);

	printf("%u", result);

	return 0;
}

```

# [비트 뒤집기]


unsigned char 크기의 정수가 하나 입력된다.
이 정수의 비트열을 뒤집은 결과를 출력하시오.

비트열을 뒤집는다는 것은, 문자열을 뒤집듯이 비트를 뒤집는 것이다.

예를 들어, 42 (0010_1010)를 뒤집으면 84 (0101_0100)가 된다.

```
#include <stdio.h>

int main() {
	unsigned char num;
	unsigned char reverse= 0;

	
	scanf("%hhu", &num);

	
	for (int i = 0; i < 8; i++) {
		reverse <<= 1;            
		reverse = reverse|(num & 1);   
		num >>= 1;              
	}

	
	printf("%u", reverse);

	return 0;
}

```
