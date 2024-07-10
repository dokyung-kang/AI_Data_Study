# AI와 데이터 기초1 - 2일차

## 데이터 종류와 구조

### 빅데이터 종류

**정형데이터(structured data)**

- 미리 정해 놓은 형식과 구조에 따라 저장된 데이터
- 예 : 관계형 데이터베이스의 테이블, 스프레드시트, CSV 등

<br/>

**반정형데이터(semi-structured data)**

- 일정한 규칙의 고정된 필드에 저장되어 있지 않지만 데이터의 구조 정보를 데이터와 함께 제공하는 데이터
- 예 : XML, HTML, JSON, 웹문서, 웹로그 등

<br/>

**비정형데이터(unstructured data)**

- 정의된 구조가 없이 데이터 자체만으로 내용에 대한 질의 처리를 할 수 없는 데이터
- 예 : 소셜 데이터, 텍스트 문서, 동영상/이미지/음성 데이터, 문서(PDF) 등

<br/>

#### (정형)데이터 구조

**데이터(표)는 행(row)와 열(colum)로 구성**

- 행(row): 하나의 단위로 다루어지는 데이터의 집합(표의 가로축) - 레고드(record)
- 열(column): 특정 자료형을 갖는 일련의 데이터 값(표의 세로축)

<br/>

**칼럼(column) = 열**
- 칼럼(column) = 열 : 통계 분야
- 변수(variable) : 컴퓨터 분야
- 속성(attribute) : 속성
- 특징(feature) : 패턴인식 분야

<br/>

**칼럼의 종류**
- 수치형(Numeric) : 정수형(int), 실수형(float), Bool형
- 범주형(Categorical) : 순서형(category), 텍스트(object)

<br/>

#### 데이터 정보가 중요한가?

- **행과 열**
    - 데이터의 크기를 알 수 있음
    - 처리의 양을 파악할 수 있음
    - 변수(칼럼)들을 통해서 변수간의 관련성에 대한 의문점을 가질 수 있음

- **칼럼의 종류**
    - 칼럼들의 연산 가능여부 확인 가능
    - 간단한 통계정보를 통하여 데이터에 대한 대략적인 분석 가능
    - 칼럼의 종류에 따라 프로그램 작성 시 오류 파악 가능

<br/>

#### 데이터의 크기

**데이터가 크다? : 행이 많거나 열이 많음**

<br/>

**데이터 분석을 위해서는 행과 열 중 무엇이 많은게 좋을까 : [답] 열**
- 행이 많은 경우
    - 행의 개수가 많을수록 처리하는 양이 많아짐으로 컴퓨터가 느려짐
    - 물리적인 비용(메모리나 CPU, 분산처리, 클라우드)으로 해결가능
    - 100만명과 100명의 평균 또는 분석 방법이 같다면 데이터 분석의 노력 결과는 달라지지 않음
- 열이 많은 경우
    - 변수간의 관계에 대해 분석할 수 있는 사항들이 많아짐
    - 분석 방법 및 기술이 다양해짐

<br/>

**행과 열의 수보다 '다양한 데이터가 더 중요!!'**
- 데이터의 가치는 어떤 현상이 조건에 따라 달라진다는 사실을 발견할 때 생김
- 조건에 따른 현상은 다양한 데이터에 포함된 변수간의 관련서으로 분석

<br/>

## 예제로 보는 데이터 구성 (seaborn 데이터셋)

### seaborn 데이터셋 불러오기(titanic)

**seaborn**
- 데이터 시각화 라이브러리
- 내장 데이터셋 22개 제공(sns.get_dataset_names() 명령으로 확인 가능)

```python
import seaborn as sns
df = sns.load_dataset('titanic')
df.head()
```

<br/>

### titanic 데이터 전체보기

```python
df
```

<br/>

### titanic 데이터 구성 확인하기

```python
df.info()
```

<br/>

### titanic 데이터셋 시각화하기

```python
sns.countplot(data=df, x='alive')
```

<br/>

## 데이터 준비하기(pandas)

### pandas란

- 데이터 분석을 위한 Python 라이브러리
    - Panel Data Analysis
    - 대용량의 (정형)데이터 처리를 지원함
    - 데이터 관리와 정제 기능을 가진 라이브러리
    - 머신러닝, 시각화 등의 데이터 사이언스 관련 라이브러리에서 사용

<br/>

**Excel과의 차이점**

||엑셀|판다스|
|---|---|---|
|자동화|- 기본적으로 사람의 손으로 작업 <br/> - VB로 자동화 가능하기는 함|코딩을 통한 자동화|
|대용량 데이터 처리|- 큰 데이터 처리에 부적합함 <br/> -로딩이 안되는 경우도 있음 <br/> - 데이터 처리 속도가 느림|데이터 처리 속도 빠름|
|분석 방법|지원되는 기능에 한정|사용자가 코딩을 통해 다양한 창의적인 데이터 분석이 가능함|

<br/>

### 설치방법 및 라이브러리 선언

1. 콘솔에서 아래의 명령으로 설치
    - Path 설정에 문제가 있는 경우 아래 명령이 실행 안될 수도 있음
    - 그럴 경우 pip 명령이 있는 위치로 경로를 이동한 후 실행
    ```python
    pip install pandas
    ```
2. 코랩(colab)에는 이미 설치되어 있음
3. 라이브러리 선언
    ```python
    import pandas as pd
    ```

<br/>

### 파이썬 기본 자료구조

- **리스트**
    - a = [10, 20, 30]
    - b = [[1, 2], [3, 4], [5, 6]]
    - 데이터 개별 접근 : a[0] + a[2] / a[0:2] / b[2][1]
- **튜플 : 데이터 변경 불가**
    - a = (10, 20, 30)
    - b = ((1, 2), (3, 4), (5, 6))
    - 데이터 개별 접근 : a[0] + a[2] / a[0] = 1 (error)
- **딕셔너리**
    - key : value 형식으로 데이터 저장
    - dict = {'a': 100, 'b' : 200, 'c': 300}
    - 데이터 개별 접근 : dict['a'] + dict['b']

<br/>

### pandas 자료 구조

- **Series**
    - 1차원 배열 형태로써 같은 종류의 데이터가 순서대로 나열된 데이터 구조
- **DataFrame**
    - 데이터를 표 형식 데이터(행, 열) 구조로 저장
    - 예 : CSV, EXCEL

<br/>

#### Series

- 여러 값을 나열한 1차원 자료구조
- DataFrame을 구성하는 하위요소
- DataFrame을 다루는 함수는 대부분 시리즈를 이용하여 연산함

<br/>

1. index 자동 부여
    ```python
    import pandas as pd
    data = pd.Series([3, 4, 5])
    print(data)
    print(data[0])
    print(data[1])
    print(data[2])
    ```
2. index 직접 부여
    ```python
    x_data = pd.Series([20, 25, 22], index=['kim', 'lee', 'park'])
    print(x_data)
    print(x_data[0])
    print(x_data[1])
    print(x_data[2])
    print(x_data['kim'])
    print(x_data['lee'])
    print(x_data['park'])
    ```

<br/>

#### DataFrame

- DataFrame을 이용한 데이터 생성
    - pd.DataFrame({'key1':value1, 'key2':value2, ...})
        - key : 열이름(변수명)
        - value : 열이름에 해당하는 데이터들(데이터, 리스트)
            ```python
            import pandas as pd

            no = [20231021, 20225412, 20210578]
            name = ['박형식', '공유', '아이유']
            major = ['영어영문학과', '화학과', '수학과']

            df = pd.DataFrame({'학번':no, '이름':name, '학과':major})
            df
            ```
    - pd.DataFrame([데이터들], columns=['열이름들'])
        ```python
            import pandas as pd

            A1_class = [[20231021, '박형식', '영어영문학과'],
                        [20225412, '공유', '화학과'],
                        [20210578, '아이유', '수학과']
                        ]

            df = pd.DataFrame(A1_class, columns=['학번', '이름', '학과'])
            df
            ```

<br/>

## 실습하기

### 1. Series를 활용한 데이터 생성

- index 자동 부여
    - 변수명 = pd.Series([데이터])
        - 데이터 : 리스트 형식으로 작성
        - 데이터 참조 : 리스트 참조 방식으로 사용 
- index 직접 부여
    - 변수명 = pd.Series([데이터], index=[index이름])
        - 데이터 : 리스트 형식으로 작성
        - index이름 : 데이터의 개수만큼 생성

<br/>

### 2. DataFrame을 활용한 데이터 생성

- 변수명 = pd.DataFrame({'key1':value1, 'key2':value2, ...})
    - key: 열이름(변수명)
    - value : 열이름에 해당하는 데이터들(리스트)
- 변수명 = pd.DataFrame([데이터], columns=['열이름들'])
    - 데이터들 : 각 열의 데이터들(리스트)
    - 열이름들 : 각 열의 변수명

<br/>

### 3. 데이터 읽어오기

```python
import pandas as pd # 데이터 관리와 정제 기능을 가진 라이브러리
```

- xlsx 파일을 불러올 때 : 
    - 변수명 = pd.read_excel('파일경로명', 속성들)
- csv 또는 txt 파일을 불러올 때 : 
    - 변수명 = pd.read_csv('파일경로명', 속성들)

<br/>

#### pd.read_csv()와 pd.read_excel()의 속성들

- delimiter='구분기호'
    - 생략 시 ","로 인식
    - \t: tab을 열 구분 문자로 인식
- header=[행번호] 
    - 위에서 몇 째 줄부터 읽어올지 지정(줄 수는 0부터 시작)
    - 열이름(변수이름)으로 설정할 index 번호 기술
- encoding='인코딩방식'
    - 한글이 깨져서 보일 경우 인코딩 방식 설정
    - EUC_KR (한글이 포함된 일반적인 경우)/cp949 (MS office에서 저장한 파일 형식)
- thousands=','
    - ','가 포함된 문자열 데이터에서 ','을 삭제하고 숫자형 데이터로 변경

<br/>

### 4. 데이터 정보 보기

- 변수명.info() : 데이터 타입, 각 아이템 개수, 누락데이터 수 등 확인

<br/>

### 5. 데이터를 파일에 저장하기

- 변수명.to_csv('파일명')
    - DataFrame을 csv 파일로 저장
- 변수명.to_excel('파일명')
    - DataFrame을 excel 파일로 저장