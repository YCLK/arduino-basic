## 회로 설계의 기본
- ![](images/Pasted%20image%2020241020120646.png)
- 전기가 흐르기 위해서는 **전위차**가 있어야 함.
	- 전위차란, 전기 에너지가 가지는 **위치 에너지의 차이**로, 전기 에너지가 가지는 위치 에너지가 **높은 곳에서 낮은 곳**으로 전기가 흐르게 됨.
	- 아두이노의 **5V(+)가 높은** 위치 에너지 **GND(-)가 낮은** 위치 에너지를 가짐.
## 아두이노란?
- ![](images/Pasted%20image%2020241025195411.png)
- 이탈리아어로 **'강력한 친구'** 라는 의미
- **전기·전자를 손쉽게 공부**할 수 있도록 개발된 보드(일종의 컴퓨터)이며 비전공자들도 널리 사용함.
- 프로그램을 작성해서 **보드에 저장**할 수 있으며 **전원이 인가**되는 동안 계속해서 **반복 실행**함.
## 브레드보드란?
- 납땜 없이 동시에 **여러 센서를 사용**해야 할 때 사용함.
- 아두이노는 **5V를 한 곳에서만 출력**하기에 브레드보드를 통해 여러 센서를 **병렬**로 연결할 수 있음. (모든 센서에 똑같이 5V를 공급)
## 옴의 법칙
$$V = I*R$$
- 각각의 센서는 **허용되는 전압/전류**가 있는데 이를 초과하게 되면 **센서가 망가지기** 때문에 회로를 잘 설계해 주어야 함.
- 아두이노의 전압은 일정하므로 (3.3V/5V) **저항(R)을 통해서 흐르는 전류를 조절**해 주어야 함.
## LED 센서 연결 실습
- LED 센서의 허용 전류는 20mA(0.02A)이므로 **3.3V 전압에 200옴의 저항을 사용**하여 허용 전류보다 낮은 16.5mA의 전류를 흐르게 할 수 있음. ($I = 3.3/200$)
- **5V의 전압을 주는 경우, 300옴의 저항**을 사용하여 약 16mA의 전류를 흐르게 할 수 있음. ($I = 5/300$)
- 저항은 일반적으로 생각하기에 `5V → 저항 → LED → GND`순으로 연결되어야 할 것 같지만 **회로를 인식한 다음에** 전기가 흐르기 때문에 `5V → LED → 저항 → GND`순으로 연결되어도 무방함.
	- ![](images/Pasted%20image%2020241020125817.png)
	- ![](images/Pasted%20image%2020241020125925.png)
## 스위치를 통한 회로 제어
- 회로 사이에 스위치를 끼워주게 된다면 스위치가 눌리지 않은 상태에서는 **전위차가 발생하지 않으**므로, 스위치가 **눌릴 때만 LED가 켜지게** 됨.
- ![](images/Pasted%20image%2020241020212522.png)

## 아두이노를 통한 출력
### 아두이노 프로그래밍 기초 구조

```c
// 전역변수를 선언하고, 사용할 라이브러리를 추가할 수 있음.

void setup() {
// 한 번만 실행되는 함수임.
// 핀모드나 센서의 초기값 등을 설정할 수 있음.
}

void loop() {
// 이후 계속해서 반복 실행되는 한수
}
```

### 디지털 출력과 아날로그 출력
- 두 가지 출력 모두 `pinMode(핀 번호, OUTPUT)`를 통해 출력을 시작함.
- 디지털 출력
	- ![](images/Pasted%20image%2020241025200602.png)
	- LOW(0V)와 HIGH(5V) 두 가지의 전압만 내보낼 수 있음.
	- `digitalWrite(핀 번호, HIGH/LOW)`를 통해서 출력이 이루어짐.
- 아날로그 출력
	- ![](images/Pasted%20image%2020241025201023.png)
	- 디지털 출력이 LOW(0V) 또는 HIGH(5V) 두 가지의 값만 출력할 수 있는 것에 비해 아날로그 출력은 연속적인 값을 출력해낼 수 있음.
	- `analogWrite(핀 번호, HIGH/LOW)`를 통해서 출력이 이루어짐.
- 아날로그 출력에서는 `analogWrite()`를 통해서 0V 또는 5V 값을 내보낼 수 있지만 디지털 출력에서는 `digitalWrite()`를 통해 0~255의 값을 내보낼 수 없음을 유의하자!

> [!NOTE]
> 1초 간격으로 켜졌다, 꺼졌다를 반복하도록 LED 회로와 아두이노 프로그램을 작성하시오.
> > `digitalWrite()`함수와 `analogWrite()`함수는 토글(한번만 작동시켜도 작동 상태가 지속되는 방식)로 작동한다는 점과 `delay(시간, 단위는 ms)`함수에 유의하자!

```c
// 1번 과제
void setup() {
	pinMode(11, OUTPUT); // 11번 핀을 출력으로 설정
}

void loop() {
	digitalWrite(11, HIGH); // 11번 핀에 5V 전압을 출력
	delay(1000); // 1초 대기
	digitalWrite(11, LOW); // 11번 핀에 0V 전압을 출력
	delay(1000); // 1초 대기
}
```

> [!NOTE]
> 1번 문제에서 LED가 다시 켜질 때마다 밝기가 약 10%씩 감소하도록 프로그램을 작성하시오.

```c
void setup() {
	pinMode(11, OUTPUT); // 11번 핀을 출력으로 설정
}

int a = 250; // a라는 정수형 변수를 선언한 뒤, 250이라는 값을 대입함

void loop() {
	analogWrite(11, a); // 11번 핀에 a만큼의 전압을 출력
	delay(1000); // 1초 대기
	a = a-25; // a에서 25만큼을 뺌. 255(5V)의 약 10%는 250
}
```

> [!NOTE]
> 1초 간격으로 LED 색이 변하도록 회로와 프로그램을 구현하시오. (RGB LED 모듈 사용)
> > 11번 핀을 빨간색, 9번 핀을 파란색에 연결했다고 가정하자.

```c
void setup() {
	pinMode(9, OUTPUT); // 9번 핀을 출력으로 설정
	pinMode(11, OUTPUT); // 11번 핀을 출력으로 설정
}

void loop() {
	// 빨간색 출력
	digitalWrite(11, HIGH); // 11번 핀에 5V 전압을 출력
	delay(1000); // 1초 대기
	
	// 보라색 출력
	digitalWrite(11, LOW); // 11번 핀에 0V 전압을 출력
	digitalWrite(11, HIGH); // 11번 핀에 5V 전압을 출력
	digitalWrite(9, HIGH); // 9번 핀에 5V 전압을 출력
	delay(1000); // 1초 대기
	
	// 파란색 출력
	digitalWrite(11, LOW); // 11번 핀에 0V 전압을 출력
	digitalWrite(9, LOW); // 9번 핀에 0V 전압을 출력
	digitalWrite(9, HIGH); // 9번 핀에 5V 전압을 출력 
	delay(1000); // 1초 대기
	
	// 모든 LED 끄기
	digitalWrite(9, LOW); // 9번 핀에 0V 전압을 출력
}
```
## 아두이노와의 시리얼 통신
### 시리얼 통신이란?
- 아두이노에서는 쉽게 **단순히 아두이노와 컴퓨터 간의 통신**으로 생각하여도 무방함.
- 시리얼 입력은 **버퍼의 데이터**를 확인하여 **문자를 하나씩 읽는 것**임
- **시리얼 모니터**(Tool -> Serial Monitor)를 통해서 확인할 수 있음.
- `pySerial` 라이브러리를 활용하면 **파이썬과의 연계**도 가능함.
### 시리얼 통신을 위한 함수들
- `Serial.begin(통신속도, 보통 9600을 많이 사용함)`: 시리얼 통신을 시작함.
- `Serial.print(내용)`, `Serial.println(내용)`: 시리얼 통신을 통해 내용을 출력함.
- `Serial.available()`: 버퍼에 있는 데이터의 길이를 바이트 단위로 확인함.
- `Serial.read()`: 버퍼에서 문자를 하나 가져옴.
- `Serial.readString()`: 버퍼에서 문자열을 가져옴.

> [!NOTE]
> 구구단 중 하나를 시리얼로 출력하시오.
> > 출력하는 구구단은 2단이다.

```c
void setup() {
	Serial.begin(9600); // 9600의 속도로 시리얼 통신을 시작
}

int a = 1; // a라는 정수형 변수를 선언한 뒤, 1이라는 값을 대입함

void loop() {
	while (a < 10) { // a가 10미만일 동안 (2*9 까지만 출력함)
		Serial.println(2*a); // 2*a의 값을 출력함
		a = a+1; // a에 1을 더해줌
	}
}
```

> [!NOTE]
> ‘T’, ‘F’ 문자를 시리얼로 입력하면 LED가 켜지고 꺼지도록 회로와 프로그램을 작성하시오.
> > LED 모듈은 8번 핀에 연결했다고 가정하자.

```c
void setup() {
	pinMode(8, OUTPUT); // 8번 핀을 출력으로 설정
	Serial.begin(9600); // 9600의 속도로 시리얼 통신을 시작
}

void loop() {
  if(Serial.available() > 0) { // 버퍼의 데이터 길이 > 0 이면 (=읽을 데이터가 있으면)
	  char c = Serial.read(); // char 자료형의 변수 c를 선언하고 문자 하나를 읽음
	  if(c == 'T') { // c가 'T'와 같다면
		  digitalWrite(8, HIGH); // 8번 핀에 5V 전압을 출력
	  }
	  if(c == 'F') { // C가 'F'와 같다면
		  digitalWrite(8, LOW); // 8번 핀에 0V 전압을 출력
	  }
  }
}
```
## 아두이노를 통한 입력
### 디지털 입력과 아날로그 입력
- 두 가지 입력 모두 `pinMode(핀 번호, INPUT)`를 통해 입입력을 시작함.
- 디지털 입력
	- ![](images/Pasted%20image%2020241025200602.png)
	- 0V를 LOW, 5V를 HIGH로 인식함.
	- `digitalRead(핀 번호)`함수를 사용했을 때 **HIGH 또는 LOW 값**을 읽어냄.
	- **전기가 들어오지 않을 때** `digitalRead(핀 번호)`함수를 사용하면 **Floating 상태**(떠있는 상태, 입력핀이 전기적으로 연결되지 않아 불안정한 상태)가 되므로 **LOW값과 HIGH값이 임의로** 읽어온다.
	- 이를 방지하기 위해 `pinMode(핀 번호, INPUT_PULLUP)`함수를 통해 풀업 저항을 사용할 수 있다.
		- 풀업 저항을 사용하면 기본적으로 핀이 HIGH 값을 읽어오도록 하고 전기적으로 연결될 때 LOW 값을 읽어오도록 한다.
- 아날로그 입력
	- ![](images/Pasted%20image%2020241025201023.png)
	- 디지털 출력이 **LOW(0V) 또는 HIGH(5V) 두 가지의 값**만 읽을 수 있는 것에 비해 아날로그 출력은 **0부터 1023까지의 연속적인 값**을 읽어낼 수 있음.
	- `analogWrite(핀 번호)`를 통해서 0에서 1023까지의 값을 읽어옴.
### 조도센서(CDS)란?
- 밝기에 따라 저항값이 바뀌는 **가변저항**(반비례, 어두워지면 값이 커짐)임.
- 밝기에 따라 저항값이 달라지므로 **아날로그 신호**를 만들 수도 있음.

> [!NOTE]
> 어두워지면 LED가 켜지고, 밝아지면 LED가 꺼지도록 회로와 프로그램을 작성하시오.

```c
void setup() {
  Serial.begin(9600); // 9600의 속도로 시리얼 통신을 시작
  pinMode(A0, INPUT); // A0 핀을 입력으로 설정
  pinMode(7, OUTPUT); // 7번 핀을 입력으로 설정
}

void loop() {
  int a = analogRead(A0); // a라는 정수형 변수를 선언한 뒤 A0 핀을 통해 읽어온 값을 대입함
  if(a > 300) { // 읽어온 값 a가 300보다 크다면(=어두우면)
    digitalWrite(7, HIGH); // 7번 핀에 5V 전압을 출력
  }
  if(a < 300) { // 읽어온 값 a가 300보다 작다면(=밝으면)
    digitalWrite(7,LOW); // 7번 핀에 0V 전압을 출력
  }
}
```
## 아두이노 프로그래밍
### 일반적인 센서의 사용방법
- 센서: **저항**(220옴, 10K옴 등)을 연결해 주어야 함. (Ex. LED, 조도(빛) 센서 등)
- 센서 모듈: 저항까지 **센서에 포함**되어 있어 별도로 **저항을 연결하지 않아**도 됨.

![](images/Pasted%20image%2020241020214249.png)

```c
#include "DHT.h"
#include <LiquidCrystal_I2C.h>

#define DHTPIN 6
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  Serial.begin(9600);
  dht.begin();

  // LCD를 초기화 및 백라이트 ON
  lcd.init();
  lcd.backlight();
}

void loop() {
  // 온습도센서(DHT11)를 이용하여 온도와 습도값을 측정하고 LCD에 출력하시오.
  float humidity = dht.readHumidity(); // 습도 읽기
  float temperature = dht.readTemperature(); // 온도 읽기
  
  Serial.print((int)temperature); Serial.print(" *C, "); // 온도값 출력
  Serial.print((int)humidity); Serial.println(" %"); // 습도값 출력

  String humi = "Humi : ";
  humi += (String)humidity;
  humi += "%";
  
  String temp = "temp : ";
  temp += (String)temperature;
  temp += "C";

  lcd.setCursor(0, 0);
  lcd.print(humi);

  lcd.setCursor(0, 1);
  lcd.print(temp);

  delay(1500);
}
```
## 아두이노를 위한 C언어 기초
### 자료형과 자료구조
| 파이썬의 자료형 | C언어의 자료형 |
| -------- | -------- |
| 정수       | 정수       |
| 실수       | 실수       |
| 문자열      | 문자(char) |
- 언뜻 보기에는 큰 차이가 없어보이나 C언어는 문자열이 아닌 문자(char, character의 약자)를 자료형으로 가짐
- 즉 char에는 하나의 문자만 저장할 수 있음을 의미함. `char c = a`
- 따라서 아두이노의 경우 라이브러리를 통해 String을 지원하고 있음.

| 파이썬의 자료구조 | C언어의 자료구조 |
| --------- | --------- |
| 리스트       | 배열        |
| 딕셔너리      |           |
| 튜플        |           |
- 배열과 리스트와 비슷하지만 **자료형에 관계없**이 모든 요소를 추가할 수 있는 것에 비해 배열은 **동일한 자료형**만 저장할 수 있음.
### 조건문
- 파이썬의 조건문 문법
	- **elif**를 통해서 여러 개의 조건을 확인할 수 있음. 
```python
if 질문 : 
	질문이 참일 때 실행할 코드
```
- C언어의 조건문 문법
	- elif 대신 **else if**를 사용해야 함.
	- switch를 사용할 수도 있음.
```c
if (질문) {
	질문이 참일 때 실행할 코드
}
```
- 파이썬의 반복문 문법
```python
# while문
while 질문 : 
	질문이 참인 동안 반복할 부분

# for문
for 변수 in 집합 : 
	변수가 집합의 원소를 순회하며 실행될 코드
```
- C의 반복문 문법
```c
// while문
while (질문) {
	질문이 참인 동안 반복할 부분
}

// for문
for (초기값; 질문; 증감식) {
	질문이 참인 동안 반복할 부분
}

// 예시 | 0 1 2 3 4 출력
for (int i=0; i<5; i=i+1) {
	Serial.println(i);
}
```
- 파이썬에서의 함수 생성
```python
def 함수이름(매개변수) : 
	실행할 내용
```
- C언어에서의 함수 생성
```c
반환형 함수이름(매개변수) {
	실행할 내용
}
```

| 파이썬 주석       | C언어 주석     |
| ------------ | ---------- |
| `# 주석`       | `// 주석`    |
| `''' 주석 '''` | `/* 주석 */` |
- 기타 C의 특징
	- 포인터: 변수를 통해서 **메모리 공간에 직접 접근**하고 조작할 수 있음.
	- **데이터의 표현**이 파이썬에 비해 상대적으로 **제한적**임
	- 문자를 숫자로 변경하거나 숫자를 문자로 변경할 수 있음 (반대도 가능함, ASCII 코드)

> [!NOTE]
> 시리얼로 문자열을 입력받아, 문자 a의 개수를 세는 프로그램을 작성하시오.

```c
void setup() {
	Serial.begin(9600); // 9600의 속도로 시리얼 통신을 시작
}

void loop() {
	int n = 0; // a라는 정수형 변수를 선언한 뒤, 0이라는 값을 대입함
	
	if (Serial.available() > 0) { // 버퍼의 데이터 길이 > 0 이면 (=읽을 데이터가 있으면)
		char a = Serial.read(); // char 자료형의 변수 c를 선언하고 문자 하나를 읽음
		if (a == 'a') { // a가 'a'와 같다면
			n = n + 1; // 변수 n에 1을 더함
		}   
	}
Serial.println(n); // n의 값을 출력함
}
```

> [!NOTE]
> 문자 ‘A’와 ‘a’를 숫자로 변환하여 출력하시오.

```c
void setup() {
	Serial.begin(9600); // 9600의 속도로 시리얼 통신을 시작
}

void loop() {
	Serial.println('A'); // 'A'를 출력함
	Serial.println((int)'a'); // 01100001을 출력함, 정수 변환값
	Serial.println((int)'A'); // 01000001을 출력함, 정수 변환값
}
```
## 수행평가 예제 코드

> [!TIP]
> 터치센서에 손이 닿아있는 동안, LED가 켜지도록 프로그램을 작성하시오.
> > 터치 센서가 연결된 핀을 4번, LED 모듈이 연결된 핀을 2번이라고 가정하자.

```c
void setup() {
    pinMode(4, INPUT); // 4번 핀을 입력으로 설정
    pinMode(2, OUTPUT);  // 2번 핀을 출력으로 설정
}

void loop() {
    int touchValue = digitalRead(4); // 터치 센서 상태 읽기

    if (touchValue == HIGH) { // 센서가 터치되었을 때
        digitalWrite(2, HIGH); // LED 켜기
    } else {
        digitalWrite(2, LOW); // LED 끄기
    }

    delay(10); // 0.01초간 대기
}
```

> [!TIP]
> 측정된 밝기에 따라 LED 밝기의 출력이 달라지도록 프로그램을 작성하시오.
> > 조도 센서가 연결된 핀을 A0, LED 모듈이 연결된 핀을 9번이라고 가정하자.

```c
void setup() {
	pinMode(A0, INPUT); // A0 핀을 입력으로 설정
	pinMode(9, OUTPUT); // 9번 핀을 출력으로 설정
}

void loop() {
	int sensorValue = analogRead(A0); // 조도 센서 값 읽기
	
	/* 1부터 10까지 측정되는 센서가 5라는 값을 측정했다고 하자.
	이를 0~1 사이의 값으로 나타내기 위해 (측정한 값)/(전체 측정 범위)로 계산하고
	최대 전앖 255(5V)를 곱해 조도 센서 측정 값에 따른 전압을 계산할 수 있다. */
	
	int brightness = (sensorValue / 1023.0) * 255; // 센서 값을 LED 밝기 값으로 변환
	analogWrite(ledPin, brightness); // 9번 핀에 brightness만큼의 전압을 출력
	delay(100); // 0.1초간 대기
}
```
## 참고
[직렬연결 vs 병렬연결 - 달빛과학](https://dalvitjeju.tistory.com/74)
[03-1 디지털과 아날로그 신호 - 위키독스](https://wikidocs.net/30776)
[05-3 내부 풀업(Pull-up)저항 사용하기](https://wikidocs.net/30793)
[온습도 센서(모듈)로 온/습도 확인하기](https://kocoafab.cc/tutorial/view/726)
