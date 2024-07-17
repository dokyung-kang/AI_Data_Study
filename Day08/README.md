# AI와 데이터 기초2 - 3일차

## 반정형 데이터 수집(JSON)

### 공공데이터 종류

- **정형데이터(structured data)**
    - 미리 정해 놓은 형식과 구조에 따라 저장된 데이터
    - 예 : 관계형 데이터베이스의 테이블, 스프레드시트, CSV 등
- **반정형데이터(semi-structured data)**
    - 일정한 규칙의 고정된 필드에 저장되어 있지 않지만 데이터의 구조 정보를 데이터와 함께 제공하는 데이터
    - 예 : XML, HTML, JSON, 웹문서, 웹로그 등

<br/>

### JSON이란

- **Json(JavaScript Object Notation)**
    - 자바 스크립트 언어로 구조화된 문자 기반 표준 포맷
    - 파이썬의 딕셔너리와 리스트를 중첩한 것과 비슷

<br/>

### JSON과 Python 변환

- JSON 라이브러리 선언
    - import json
- JSON(문자열)과 Python 객체(Dictionary) 변환

<br/>

### JSON 문자열 생성 및 변환

- json.dumps() : 파이썬 객체를 JSON 문자열로 변경
    - json.dumps(데이터, ensure_ascii=False)
        - 데이터 : 파이썬 객체(Dictionary 구조)
        - ensure_ascii = False : 한글이 깨지지 않고 저장된 문자 그대로 출력
- json.loads() : JSON 문자열을 파이썬 객체로 변경
    - json.loads(데이터)
        - 데이터 : json 구조를 갖는 문자열
- pd.DataFrame() : 파이썬 객체를 DataFrame 구조로 변경
    - pd.DataFrame(데이터)
        - 데이터 : 파이썬 객체

<br/>

## JSON 파일 읽어오기

### Python 객체(dictionary)를 JSON 파일로 변환

- with open('파일명', 'w') as 파일 객체 : 파일을 열기 위한 명령문
    - 파일명 : JSON 경로명과 파일명(*.json)
    - 'w' : 파일을 쓰기 전용으로 open
    - 파일 객체 : 파일을 관리하는 객체
- json.dump(데이터, 파일객체) : 파이썬 객체를 JSON 파일로 변경
    - 데이터 : 파이썬 객체(Dictionary 구조)
    - 파일 객체 : 파일을 관리하는 객체

<br/>

### JSON 파일 읽어오기와 excel로 저장하기

- with open('파일명', 'r') as 파일객체 : 파일을 열기 위한 명령문
    - 파일명 : JSON 경로명과 파일명(*.json)
    - 'r' : 파일을 읽기 전용으로 open
    - 파일객체 : 파일을 관리하는 객체
- 변수명 = json.load(파일객체) : JSON 파일의 binary를 파이썬 객체로 변경
    - 데이터 : json 구조를 갖는 binary 데이터
- pd.to_excel(파일명) : DataFrame에 저장된 데이터를 excel 파일로 저장
    - 파일명 : excel 파일명

<br/>

## openAPI로 데이터 읽어오기

### API(Application Programming Interface)란

- 데이터베이스 접근 권한이 없는 데이터나 웹사이트에서 데이터를 수집할 수 있는 방법
- 두 프로그램이 서로 대화하기 위한 방법을 정의 
    - 예 : 작성한 문서를 디스크에 저장하고자 할 때 윈도우나 macOS는 디스크에 저장할 수 있는 API를 제공
- 웹기반 API
    - 웹서버에 접근하고 요청 웹 페이지를 브라우저에 보이게 하기 위한 API
    - HTTP 프로토콜을 사용하여 API를 만드는 것

<br/>

### OpenAPI

- 누구나 데이터에 접근하여 사용할 수 있도록 공개된 API
- 개발자나 사용자가 표준화한 데이터를 프로그램하거나 활용할 수 있는 형태의 개방 형식
- 업데이트가 빈번하고 활용도가 높은 대용량의 데이터 등에 활용
- 제공되는 형태 : JSON, XML, CSV 등

<br/>

### URL의 get방식

- HTTP의 GET 방식
    - 웹브라우저가 웹 서버에 요청할 때 URL에 파라미터 값이나 데이터를 전달하는 것
    - URL 구조 : 호출주소 + ? + 쿼리 스트링
    - 쿼리 스트링 : 조건 기술 (여러 개일 경우에는 &로 나열)
    - 예 : 네이버 이미지에서 동덕여자대학교 이미지를 검색했을 때 URL

<br/>

### openAPI 이용방법

1. 가져오고자 하는 데이터의 사이트에 접속하고 회원가입한다.
2. openAPI 인증키를 신청한다.
    - 인증키를 신청하면 바로 승인되는 사이트도 있지만 보통 1일 ~ 5일 소요됨
3. openAPI 인증키를 검색/확인한다.
4. 해당 데이터를 [활용신청]한다.
    - [활용신청] 없이 바로 활용할 수 있는 사이트도 있음
5. openAPI를 활용하고 어플리케이션을 제작한다.
    - 사용법을 모를 경우에는 샘플로 제공하는 python 프로그램을 활용
6. 어플리케이션을 등록한다.

<br/>

### openAPI로 JSON 읽어오는 과정

1. URL 생성 : url과 파라미터 변수에 저장
    - 해당 사이트의 openAPI에서 지정한 url 확인 필요
    - 해당 사이트에서 제공하는 파라미터 정보를 활용하여 검색 범위 지정
2. 변수명 = requests.get(url) : url을 HTTP get 방식으로 접속
    - url : 호출주소와 파라미터가 있는 문자열
    - 변수명 : requests.get()의 결과 메시지(오류 발생시 HTTP 오류 번호 반환)
3. requests.json(변수명) : get 방식으로 가져온 자료가 json인 경우 json으로 변환
4. pd.DatFrame(변수명) : 가져온 json을 리스트에 저장한 후 DataFrame으로 변환