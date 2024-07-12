# AI와 데이터 기초1 - 5일차

## 텍스트 시각화

### 워드클라우드(WordCloud)

- 텍스트에서 단어들을 분석하여 인기도 및 중요도에 따라 글자 색상, 크기 및 굵기의 형태로 시각적 이미지로 표현하는 것
- 인기도 및 중요도는 빈도수로 표현될 수 있음

<br/>

### WordCloud 준비하기

- 설치하기
    - pip install wordcloud
- 코랩(colab)에는 이미 설치되어 있으
- 라이브러리 선언
    - WordCloud는 matplotlib 라이브러리를 기반으로 하고 있으므로 함께 선언
        ```python
        from wordcloud import WordCloud
        import matplotlib.pyplot as plt
        ```

<br/>

### 라이브러리 설치 및 한글 폰트 설치

- 자연어 처리를 위한 라이브러리 설치하기
    - pip install konlpy
- Colab 한글 폰트 설치
    ```bash
    !sudo apt-get install -y fonts-nanum
    !sudo fc-cache-fv
    !rm ~/.cache/matplotlib -rf
    ```

<br/>

### 텍스트 파일과 이미지 파일 불러오기

- 명령어를 통하여 파일 업로드 하기
```python
from google.colab import files
files.upload()
```

<br/>

### 필요한 라이브러리들 로딩하기

- **워드 클라우드 생성에 필요한 라이브러리(wordcloud, STOPWORDS, matplotlib)**
```python
from wordcloud import WordCloud
from wordcloud import STOPWORDS
import matplotlib.pyplot as plt
```
- **마스크 이미지 처리를 위해 필요한 라이브러리들(Image, numpy)**
```python
from PIL import Image
import numpy as np
```

<br/>

### 관련 파일들 open 하고 저장하기

- **텍스트 파일을 열어 읽어오기**
    - 파일변수명 = open('파일명', 'r', encoding='인코딩방식')
    - 텍스트파일명 = 파일변수명.read()
        - 파일에 저장되어 있는 본문을 읽음
- **CSV 파일 읽어오기**
    - 변수명=pd.read_csv('파일명', encoding='인코딩방식' skiprows=[행번호])
- **마스크 이미지 파일을 읽어와서 array로 변경하기**
    - 마스크변수명 = np.array(Image.open('마스크이미지파일명'))
        - 마스크 이미지를 읽어와서 Array 자료형으로 변환

<br/>

### 자연어 처리

- **한글 자연어처리를 위한 konlpy 라이브러리 로딩하기**
    - from konlpy.tag import Okt
- **Okt 라이브러리를 사용하기 위한 객체 생성**
    - 변수명 = Okt()
- **문자열에서 명사만 추출하기**
    - 변수명.nouns(문자열)

<br/>

### 워드 클라우드 속성 저장하기

- **불용어 처리를 위한 단어 추가하기**  
    - 변수명 = STOPWORDS.union({'단어들'})
        - 단어들 : 불용어로 처리하고자 하는 단어들을 쉼표(,)로 분리하여 기술
- **워드 클라우드 속성 설정하기**
    ```python
    변수명 = WordCloud(width=정수, height=정수, 
                        stopwords=불용어변수명,
                        font_path=폰트경로,
                        mask=마스크변수명,
                        background_color='배경색')
    ```

<br/>

### 워드 클라우드 생성하기

- **문자열을 활용하여 워드 클라우드 생성하기**
    - 변수명.generate(문자열변수명)
- **딕셔너리 데이터를 활용하여 워드클라우드 생성하기**
    - 변수명.generate_from_frequencies(dictionary변수명)

<br/>

### 워드 클라우드 출력 및 눈금 숨기기

- **워드 클라우드 이미지 출력하기**
    - plt.imshow(변수명)
- **x, y축 눈금 숨기기**
    - plt.axis('off') : x, y축에 표시되는 눈금 제거

<br/>

## 지도 시각화

### folium

- leaflet.js 기반으로 만들어진 지도 시각화에 특화된 라이브러리
    - 자바 스크립트 기반으로 만들어져서 웹에서 출력 용이
- 무료로 사용 가능
- 지도 생성, 마커 표시, 행정구역 경계선 및 색상 표현, html 파일로 내보내기 등 다양한 기능 제공
- 다양한 plugin을 제공함으로써 좀 더 복잡하고 시각적인 표현 가능
- folium 설치
    - colab의 경우 이미 설치되어 있음
        - pip install folium
- folium 선언
    - import folium

<br/>

### folium을 이용한 지도 시각화 순서

1. folium을 활용한 Map 그리기
2. 지도에 Marker 표시하기
3. 지도에 여러 Marker 표시하기
4. MarkerCluster로 표현하기

<br/>

### 지도 그리기

- folium.Map(속성들)
    - 지도를 그려주는 객체
    - location=[위도, 경도] : 지도의 중심 좌표를 지리 좌표계인 [위도, 경도] 또는 (위도, 경도)로 나타냄
    - zoom_start=정수 : 지도를 처음 그릴 때 확대 정도
    - zoom_control=True : zoom in/out 버튼 표시 여부
    - control_scales=False : 스케일 컨트롤 버튼 표시 여부
    - tiles='스타일' : 지도 스타일을 지정

<br/>

### 지도상에 Marker와 MarkerCluster 표시하기

- **지도상에 일반 Marker 표시하기**
    - folium.Marker(속성들).add_to(MarkerCluster변수명)
        - location=[위도, 경도] : marker가 표시되는 위치정보(위도, 경도)
        - popup='문자열' : marker를 클릭했을 때 나타나는 메세지(문자열)
        - tooltip='문자열' : marker에 마우스를 올렸을 때 나타나는 메세지(문자열)
        - icon='모양' : marker의 모양을 설정
- **MarkerCluster 표현하기**
    - 변수명 = MarkerCluster().add_to(지도변수명)
- **DataFrame의 각 행의 정보 읽어오기**
    - df.iterrow() : DataFrame에 저장된 데이터를 index 단위로 읽어옴
