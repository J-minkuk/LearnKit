# URL 분석
* 프로토콜
* 도메인
* 파일 디렉토리 경로와 파일명
* 파라미터(Query String)
* 프래그먼트/해시태그/앵커

예시
http://music.naver.com/listen/top100.nhn?domain=OVERSEA&duration=1h#content

---

## 프로토콜
http://music.naver.com/listen/top100.nhn?domain=OVERSEA&duration=1h#content
* 프로토콜은 ```http```
* 컴퓨터 간 정보를 주고 받을 때 통신 방법에 대한 규칙을 표기하는 것입니다.
* 일반적인 url 에서 많이 사용되는 대표적인 프로토콜은 ```http 와 https``` 입니다.

### HTTP
* 웹 상에서 정보, 주로 html 문서를 주고 받을 수 있는 프로토콜이며, 일반적인 웹 사이트에서 가장 많이 사용됩니다.
* 해당 프로토콜을 통해 클라이언트와 서버 사이에 이루어지는 요청과 응답을 주고 받습니다.

### HTTPS
* HTTP 의 보안이 강화된 버전입니다.
* 통신에서 주고 받는 요청과 응답 데이터를 일반 텍스트가 아닌 SSL 또는 TCL 을 통해 암호화 한 세션 데이터로 주고 받습니다.
* 보안이 필요한 서비스(예: 은행, 카드 등)에서 주로 쓰입니다.

---

## 도메인
http://music.naver.com/listen/top100.nhn?domain=OVERSEA&duration=1h#content
* ```music.naver.com```
* 도메인은 네트워크상의 컴퓨터 주소를 의미합니다.
* 도메인은 상위도메인, 도메인이름, 호스트명으로 구성됩니다.
    * 상위 도메인: ```com```
    * 도메인 이름: ```naver```
    * 호스트 이름: ```music``` 
    * 도메인 전체에는 국가나 기관의 정보, 도메인 이름과 도메인에 속한 호스트 정보가 기입
    * 각 정보는 점(.)으로 구분할 수 있으며, 뒤에서부터 순차적으로 확인

### 호스트 이름
* 예를 들어 ```news.naver.com``` 라는 url 에서 도메인 이름은 ```naver.com```, 호스트 이름은 ```news``` 가 됩니다.
* 호스트 이름은 ```m.news.naver.com``` 에 붙은 ```m.news``` 와 같이 2개 이상 사용할 수도 있습니다.
* ```m.news.naver.com``` 은 news.naver.com 하위에 속한 추가 호스트 주소를 갖고 있는 다른 url 로 해석할 수도 있습니다.

---

## 파일 디렉토리 경로와 파일명
http://music.naver.com/listen/top100.nhn?domain=OVERSEA&duration=1h#content
* 해당 페이지는 ```music.naver.com``` 라는 도메인에 해당하는 웹 서버의 ```listen``` 라는 폴더에 저장된 ```top100.nhn``` 파일로 제공됩니다.
* 도메인에 해당하는 웹 서버를 기준으로, 제공하고자 하는 페이지가 속한 폴더명과 해당 파일명을 나타냅니다.

---

## 파라미터 (Parameter, Query String)
http://music.naver.com/listen/top100.nhn?domain=OVERSEA&duration=1h#content
* 해당 URL 은 ```~top100.nhn``` 를 보여줄 때, domain 과 duration 이라는 파라미터의 값을 각각 OVERSEA, 1h 로 설정하여 제공한다고 해석할 수 있습니다.

### 가변적인 컨텐츠를 처리하기 위한 정보
* 파라미터는 Query String 이라고도 하며, 정보에 따라 페이지의 컨텐츠가 가변적일 때 사용합니다.
* 검색 결과 페이지를 보면 하나의 페이지에서 검색어에 따라 다른 컨텐츠로 구성됩니다.
    * 페이지 url 에서 검색어같은 정보를 구분할 수 있도록 url 뒤에 파라미터라는 매개변수를 추가하여 검색어 정보를 url 에 함께 전달합니다.
    * 파라미터는 url 의 파일명 뒤 물음표 이후에 나열되며, 이름과 값으로 구성된 세트가 1개 이상 존재할 수 있습니다.
    * 이 세트는 & 기호로 구분됩니다.
    
### URL 을 구분하기 위한 정보
한 페이지 url 을 상황에 따라 구분하기 위해 파라미터를 사용할 수도 있습니다.
* 한 페이지의 url 을 여러 매체에 홍보하고, 추후 url 에 유입된 사용자가 홍보를 통해 들어온 사용자인지,
 홍보를 통해 들어온 사용자라면 어떤 매체를 통해 들어왔는지 확인해야 하는 상황이라면
    * url 을 배포할 때 정보를 구분할 수 있는 파라미터 값을 각각 추가하고
        > ex: 파워링크 영역의 링크는 ```~?t=pl``` 와 같은 파라미터 추가
    * 나중에 url 에 접근되는 사용자의 파라미터 값을 분석한다면 각각의 기준으로 사용자를 구분할 수 있습니다.
    
### 파일 디렉토리 및 파일명 역할을 하기 위한 정보
파라미터는 동일한 페이지의 일부 정보를 구분하기 위한 용도 외에도, 파일 디렉토리 및 파일명과 유사한 역할로 사용할 수 있습니다.
* ```http://www.mediatoday.co.kr/?mod=main&act=index```
* ```http://www.mediatoday.co.kr/?mod=company&act=introduce```

---

## 프래그먼트 (Fragment)
http://music.naver.com/listen/top100.nhn?domain=OVERSEA&duration=1h#content
* 해당 페이지에서 content 영역을 지시
    > content 영역으로 스크롤된 페이지를 바로 확인할 수 있습니다.
* Ex1) ```https://www.w3.org/TR/WCAG20/#operable```
    > WCAG2.0 이라는 가이드 문서 중, operable 항목을 지시하고 싶을 때 사용된 경우
* Ex2) ```http://www.kinoz.com/#portfolio```
    > 한 페이지에 여러 메뉴 컨텐츠가 구성된 사이트에서 porfolio 메뉴에 해당하는 영역으로 이동하고자 할 때 사용된 경우
