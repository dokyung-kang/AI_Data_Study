# AI와 데이터 기초2 - 2일차

## numpy 이해와 자료구조

### numpy란

- **넘파이(numpy)**
    - 수치 연산, 과학 연산을 위한 파이썬 외부 라이브러리
    - 복잡한 연산을 수행하는 데이터분석, 시각화, 머신러닝 등의 작업에 필수
    - 벡터, 행렬 등의 자료구조 및 연산 지원
- **제공하는 기능들**
    - 통계 함수 : 최대, 최소, 평균, 중간값, 분산, 표준편차, n분위수
    - 수학 함수 : 삼각함수, 로그함수 등
    - 벡터 및 행렬 연산 : 행렬의 곱, 역행렬, 전치행렬(array라는 이름을 제공)
    - 공학 수학, 선형대수학 등

<br/>

### numpy의 장점

- **데이터를 생성할 수 있다**
    - 특정 패턴의 수열, 랜덤 수, 특정 분포에 근거한 데이터, 수학 함수 데이터(삼각 함수 등)
- **많은 데이터를 쉽고 빠르게 처리할 수 있다.**
    - 리스트로 하는 것보다 수행 속도가 훨씬 빠름
    - 코드도 훨씬 빠름
- **복잡한 연산을 수행할 수 있다.**
    - 통계, 선형 대수(행렬 연산 등), 푸리에 연산 등

<br/>

### numpy 설치하기

- 설치
    - pip install numpy
- 주피터 노트북과 코랩은 이미 설치되어 있음
- 라이브러리 선언
    - import numpy as np

<br/>

### numpy가 왜 필요할까

- **문제1**
    - 1부터 20까지 3씩 증가되는 리스트 생성하기
    - 수열의 모든 값에 10을 더하기
    - 수열의 모든 값에 2를 곱하기
        ```python
        x = list(range(1, 20, 3))
        x

        for i in range(len(x)):
        x[i] = x[i] + 10
        x

        for i in range(len(x)):
        x[i] = x[i] * 2
        x
        ```
- **문제2**
    - 0.5부터 2.5까지 0.3씩 증가되는 수열(리스트)를 생성하기
    - 수열의 모든 값에 10을 더하기
    - 수열의 모든 값에 2를 곱하기

- **문제1로 문제2를 해결할 때 문제점**
    - range()함수로는 실수에 대한 수열을 생성 불가능 
    - 반복문을 사용해야 하는 번거로움
    - 복잡한 소스코드

<br/>

### numpy의 자료구조(array)

- **1차원 행렬**
    - 리스트를 만든 후 Array로 변환하여 생성
        ```python
        arrData = np.array([1, 2, 3, 4, 5])
        print(arrData)
        print(type(arrData))
        ```
- **2차원 행렬**
    - 2차원 리스트 생성 후 array로 변환
        ```python
        arrData2 = np.array([[1, 2, 3],
                     [4, 5, 6],
                     [10, 11, 12]])
        print(arrData2)
        print(type(arrData2))
        ```

<br/>

## numpy를 이용한 데이터 생성 및 통계

### 수열 생성

- **.np.arange(a, b, c)**
    - a : 시작값
    - b : 종료값
    - c : 증감값
    - 실수값 지원
    - list가 아니라 array 형태로 생성
- **np.linspace(a, b, c)**
    - a : 시작값
    - b : 종료값
    - c : 데이터 생성 개수(등급의 개수)
        - 100으로 하면 100개의 구간으로 나누는 수열 생성

<br/>

### range()와 np.arange()의 차이점

- **공통점**
    - (시작값, 종료값, 증감값) 동일
- **차이점**
    - range() : 시작값, 종료값, 증감값에 실수 지원 안함
    - np.arange() : 시작값, 종료값, 증감값에 실수 지원

<br/>

### np.arange()를 이용한 Sin 함수 그리기

```python
import matplotlib.pyplot as plt

x=np.arange(0, 3.14*2, 0.1)

y = np.sin(x)

plt.plot(x, y)
plt.show()
```

<br/>

### Sin, Cos 함수 그리기

```python
x = np.arange(0, 3.14*2, 0.1)

y1 = np.sin(x)
y2 = np.cos(x)

plt.plot(x, y1, label='sine')
plt.plot(x, y2, label='cosine')

plt.title('sine & cosine graph')
plt.xlabel('x value')
plt.ylabel('y value')
plt.grid(True)
plt.legend()

plt.show()
```

<br/>

### np.linspace()

- **np.linspace(a, b, c)**
    - a : 시작값 # 정수, 실수
    - b : 종료값 # 종료값을 포함한 정수, 실수
    - c : 데이터 생성 개수(등급 개수) # 정수
        - 100으로 하면 100개의 구간으로 나누는 수열 생성
    ```python
    x = np.linspace(-np.pi, np.pi, 100)

    y1 = np.sin(x)
    y2 = np.cos(x)

    plt.plot(x, y1, label='sine')
    plt.plot(x, y2, label='cosine')

    plt.title('sine & cosine graph')
    plt.xlabel('x value')
    plt.ylabel('y value')
    plt.grid(True)
    plt.legend()

    plt.show()
    ```

<br/>

### random 함수들 : 난수 생성

- **np.random.rand(a, b)**
    - 0.0~1.0 사이의 실수형 난수
    - (a, b) : 난수로 이루어진 2차원 array 생성
        - b 생략 시 난수로 이루어진 1차원 array 생성
- **np.random.randint(a, b, size=(x, y))**
    - a부터 b-1까지의 정수형 난수 생성
    - size(x, y) : 난수 생성 개수 # 2차원 array로 생성
- **np.random.normal(a, b, c)**
    - 정규분포를 갖는 난수 생성
    - a : 모평균
    - b : 표준편차
    - c : 생성할 개수

<br/>

## 데이터 정제

### 데이터 정제란

- **오류 데이터**
    - 데이터 수집 과정에서 누락되거나 범위에서 벗어나는 데이터
    - 데이터 분석 결과가 왜곡되어 신뢰할 수없음
- **데이터 정제 : 잘못된 데이터를 찾아서 오류를 수정하는 것**
- **데이터 정제가 필요한 데이터 종류**
    - 결측치 : 특정 행 및 열에 누락된 데이터
    - 이상치 : 정상 범위에서 벗어난 데이터
    - 중복값 : 데이터 내에 도일 데이터가 존재

<br/>

### 결측치

- **누락된 데이터, NaN(Not a Number), "?", "-" 등으로 표시됨**
- **결측치가 발생하는 경우**
    - 데이터가 수집되지 않은 경우
    - 측정 장치의 고장 및 사고로 확보할 수 없을 때
- **결측치를 찾는 이유**
    - 함수 적용이 안되는 경우 발생
    - 분석 결과가 왜곡됨
    - 데이터 분석 결과를 신뢰할 수 없음

<br/>

### 결측치 찾기

- 변수명.info()
    - DataFrame의 행/열 정보를 통해서 확인
- 변수명['열이름'].value_counts(dropna=False)
    - 데이터 빈도수를 활용하여 확인
    - dropna=False : NaN 데이터를 포함하여  데이터 빈도수 알려줌
- 변수명.isna()
    - 테이블 전체에서 결측치 찾기
    - 결측치 유무를 True/False 값으로 반환
- 변수명['열이름'].isna()
    - 특정열에서 결측치 찾기
- pd.isna(변수명).sum()
    - 각 열의 결측치 개수 확인

<br/>

### 결측값 제거하기(df.dropna())

- df.dropna(subset=['열이름1', '열이름2'])
    - subset=['열이름'] : 특정열에 NaN이 존재하는 행만 선택하여 삭제
    - subset=['열이름1', '열이름2'] : 열이름1 또는 열이름2에 NaN이 있는 모든 행 삭제
        - 단점 : 분석에 필요한 데이터도 삭제될 수 있음
- df.dropna(axis=0, how='any', thresh=개수, inplace=True)
    - 행과 열에 존재하는 결측치를 선택하여 삭제
    - axis=0 : 행과 열을 선택하여 삭제
        - axis=0 : 행 삭제
        - axis=1 : 열 삭제
    - how='any' : 결측치의 포함 정도에 따라 삭제
        - how='any' : 하나라도 포함하면 행/열 삭제
        - how='all' : 모두 포함하면 행/열 삭제
    - thresh = 개수 : 유효한 데이터가 존재하는 '개수' 이상만 남기고 삭제
    - inplace=True : 원본 데이터에 반영

<br/>

### 결측치 치환하기 (df.fillna())

- 데이터의 수가 적고 결측치가 많을 때 활용
- df.interpolate() : 앞/뒤 행의 중간값으로 치환 
- df.fillna(method='ffill') : 결측치가 있는 앞/뒤 행의 값으로 치환
    - method='ffill' : 앞 행의 값으로 치환
    - method='bfill' : 뒤 행의 값으로 치환
- df.fillna(값, inplace=True)
    - Table에 있는 전체 NaN을 동일값으로 변경
    - 값 : 변환할 데이터, 데이터가 저장된 변수명, 열의 평균이나 중간값
        - df['math'].mean() : math 열의 평균값으로 대체
        - df.fillna({'학과' : '영어영문학과'}) : 학과열의 NaN을 모두 '영어영문학과'로 변환
        - df.fillna({'학과' : '영어영문학과', '참여횟수' : 15})
            - 학과열의 NaN을 모두 '영어영문학과'로 변환하고 '참여횟수'를 15로 변환

<br/>

### 이상치 확인 및 치환하기

- **이상치**
    - 정상 범위에서 벗어난 존재할 수 없는 값 또는 극단적인 값
    - 예 : 성별은 1(남)과 2(여) 값만을 갖는데 그외의 다른 데이터
- **이상치 확인하기**
    - df['열이름'].value_couknts().sort_index()
 **이상치 데이터 치환하기**
    - df['열이름'] = df['열이름'].replace('찾는 데이터', '변환할 데이터')

<br/>

### 중복값 확인하기

- df.duplicated(['열이름'])
    - '열이름'을 기준으로 중복되는 행 검출

<br/>

### 중복값 제거하기

- df.drop_duplicates(['열이름']) : 열이름을 기준으로 중복 데이터 행 삭제
- df.drop_duplicates(subset=['열이름', '열이름'], keep="last")
    - subset=['열이름', '열이름'] : 2개 열의 데이터가 일치하는 행 삭제
    - keep="" : 데이터를 유지할 행 설정
        - 기본은 첫 번째 데이터를 유지
        - keep="last" : 마지막 데이터 유지
        - keep=False : 모두 삭제