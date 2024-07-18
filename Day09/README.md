# AI와 데이터 기초2 - 4일차

## 인터렉티브 시각화(plotly)

### 인터렉티브 시각화란

- 마우스 움직임에 따라 실시간으로 모양이 변하는 그래프
- 그래프를 자유롭게 조작하면서 관심 부분을 자세히 살펴볼 수 있음
- HTML 포맷으로 저장하면 일반 사용자도 웹 브라우저에서 그래프 조작이 가능
- 인터렉티브 시각화를 지원하는 라이브러리
    - import plotly

<br/>

### plotly 라이브러리

- 인터렉티브 시각화를 지원하는 라이브러리
- JavaScript 기반 시각화 라이브러리
- 마우스를 차트에 올려놓으면 툴팁처럼 실제 데이터 값을 확인할 수 있음
- 그래프를 확대/축소 가능함
- HTML로 변환하여 웹 상에서도 확인 가능함
- 약 40여종의 차트를 지원함

<br/>

### plotly를 활용하여 그래프를 그리는 방법

- graph_objects 모듈을 사용하는 방법
    - 그래프를 세세하게 구성할 때 사용
    - low-level interface 툴 제공
    - 코드가 길고 문법이 복잡
- express 모듈을 사용하는 방법
    - 간단한 코드로 쉽게 표현 가능한 high-level interface를 제공
    - 정해진 템플릿 외에 세세한 표현 어려움
    - 세세한 표현을 위해서는 graph_objects와 병행해서 사용

<br/>

### plotly 라이브러리 사용

- 라이브러리 설치
    - colab의 경우 이미 설치되어 있음
        - pip install plotly
        - pip install jupyter-dash
- plotly 라이브러리 선언
    - express 모듈 선언
        - import plotly.express as px
    - graph_objects 모듈 선언
        - import plotly.graph_objects as go

<br/>

### seaborn 라이브러리의 iris 데이터셋

```python
import seaborn as sns
iris = sns.load_dataset('iris')
iris
```
- sepal_length : 꽃받침의 길이
- sepal_width : 꽃받침의 너비
- petal_length : 꽃잎의 길이
- petal_width : 꽃잎의 너비
- species : 붓꽃 종류

<br/>

### scatter 차트

- px.scatter(data_frame=표이름, x='x축 열이름', y='y축 열이름')
    - data_frame=표이름 : 차트를 생성할 데이터 프레임 선택(생략 가능)
    - x='x축 열이름' : 수치형 데이터를 갖는 x축 열이름
    - y='y축 열이름' : 수치형 데이터를 갖는 y축 열이름
   
<br/>
 
### scatter 차트에서 종류 구분하기

- px.scatter(data=표이름, x='x축 열이름', y='y축 열이름', color='열이름')
    - color='열이름' : 종류를 구분하기 위한 데이터의 열이름
        - 열이름이 범주형일 경우에는 색상으로 표시
        - 열이름이 수치형일 경우에는 그라데이션으로 표시

<br/>

### 차트 꾸미기

- fig.update_layout(title_text='')
    - title_text='' : 차트 제목
- fig.update_xaxes(title='')
    - x축 레이블 속성 변경
    - title_text='' : x축 제목 설정
- fig.update_yaxes(title='')
    - y축 레이블 속성 변경

<br/>

### line 차트

- px.line(data_frame=표이름, x='x축 열이름', y='y축열이름, markers=True)
    - data_frame=표이름 : 차트를 생성할 데이터 프레임 선택 (생략 가능)
    - x='x축 열이름' : 수치형 데이터를 갖는 x축 열이름
    - y='y축 열이름' : 수치형 데이터를 갖는 y축 열이름
    - markers=True : 선차트에 marker 표시

<br/>

### line 차트 선 변경하기

- fig.update_traces(선의 속성들)   
    - line_color='' : 선 색 설정
    - line_width=2 : 선의 두께 설정
    - line_dash='dash' : 서 종류 설정(dash, dot, dashdot)

<br/>

### bar 차트

- px.bar(data_frame=표이름, x='x축 열이름', y='y축열이름, 속성들)
    - data_frame=표이름 : 차트를 생성할 데이터 프레임 선택 (생략 가능)
    - x='x축 열이름' : 수치형 데이터를 갖는 x축 열이름
    - y='y축 열이름' : 수치형 데이터를 갖는 y축 열이름
    - color = '열이름' : 종류를 구분하기 위한 데이터의 열이름
    - text_auto=True : 막대차트 내에  데이터 값 표시

<br/>

### pie 차트

- px.pie(values=데이터, names='레이블명들')
    - values = 데이터 : 데이터의 구성비를 확인하기 위한 데이터
    - names='레이블명들' : 각 영역의 값을 나타내는 레이블 문자열

<br/>

### pie 차트 도넛 모양으로 변경하기

- fig.update_traces(hole=실수)
    - 도넛 모양의 차트 설정
    - hole=실수 : 0~1 사이의 실수로 가운데 도넛 모양의 크기

<br/>

### 차트 여러 개 그리기

- graph_objects 모듈을 사용하여 여러 개의 차트 생성
- 생성 방법
```python
fig = go.Figure()
fig.add_trace(graph_objects의 차트 종류)
...
fig.add_trace(graph_objects의 차트 종류)
fig.show()
```
- graph_objectes의 차트 종류
    - go.Scatter() : scatter 차트
    - go.Bar() : bar 차트
    - go.Scatter(mode='lines') : line 차트

<br/>

### HTML로 저장하기

- fig.write_html('html파일명') : 차트를 HTML로 저장
    - 'html 파일명' : *.html

<br/>

### 버튼을 활용하여 인터렉티브 차트 생성하기

```python
fig.update_layout(
    updatemenus=[
        dict(
            type="buttons",
            buttons=list([
                dict(label="문자열", method='수행할 기능', args=[수행동작들]),
                dict(label="문자열", method='수행할 기능', args=[수행동작들]),
                dict(label="문자열", method='수행할 기능', args=[수행동작들])
            ])
        )
    ]
)
```
- label='문자열' : 버튼에 보여질 텍스트
- method='수행할 기능' : 버튼을 클릭했을 때 진행할 기능(restyle, relayout, update, animate)
- args=[] : method에 따라 구체적으로 수행할 동작들