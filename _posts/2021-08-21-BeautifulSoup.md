---
title:  "[스크레이핑] BeautifulSoup"
excerpt: "BeautifulSoup로 웹 사이트 스크레이핑하기"

categories:
  - crawling
last_modified_at: 2021-08-21T08:06:00-05:00
---
## Reference
- [파이썬을 이용한 머신러닝, 딥러닝 실전개발 입문]
![jpg](https://wikibook.co.kr/images/cover/m/9791158391799.png  )

### 이전 글
- [crawling-1](https://lee040118.github.io/crawling/crawling/)

## BeautifulSoup로 스크레이핑하기
- HTML과 XML을 분석해주는 라이브러리
- 다운로드 기능은 없음

### 기본 사용법
~~~python
from bs4 import BeautifulSoup

# HTML을 문자열로 만들어서 사용해보기
html = """
<html><body>
    <h1>스크레이핑이란?</h1>
    <p>웹 분석</p>
    <p>본문...</p>
</body></html>
"""

soup = BeautifulSoup(html, 'html.parser')

# 원하는 부분 추출하기
h1 = soup.html.body.h1
p1 = soup.html.body.p
p2 = p1.next_sibling.next_sibling

# 요소의 글자 출력
print("h1 = "+h1.string)
print("p = "+p1.string)
print("p = "+p2.string)

# 출력
# h1 = 스크레이핑이란?
# p = 웹 분석
# p = 본문...
~~~

### id로 요소를 찾는 방법
~~~python
html = """
<html><body>
    <h1 id="title">스크레이핑이란?</h1>
    <p id="body">웹 분석</p>
    <p>본문...</p>
</body></html>
"""
soup = BeautifulSoup(html, 'html.parser')
title = soup.find(id="title")
body = soup.find(id="body")

print("#title = "+ title.string)
print("#body = "+ body.string)
~~~

### 여러 개의 요소 추출하기 
- find_all()
    - 여러 개의 태그를 한번에 추출하고 싶을 때
- ex) \<a> 태그 추출

~~~python
html = """
<html><body>
    <ul>
        <li><a href = "www.naver.com">naver</a></li>
        <li><a href = "www.daum.net">daum</a></li>
    </ul>
</body></html>
"""
soup = BeautifulSoup(html, 'html.parser')

links = soup.find_all("a")

for a in links:
    href = a.attrs['href']
    text = a.string
    print(text, ">", href)

# 출력
# naver > www.naver.com
# daum > www.daum.net
~~~

### urlopen()과 BeautifulSoup 조합하기
- urlopen() 함수의 리턴값을 통해 지정
- urlopen()을 사용해 "기상청 RSS"에서 특정 내용 추출
~~~python
from bs4 import BeautifulSoup
import urllib.request as req

url = "http://www.kma.go.kr/weather/forecast/mid-term-rss3.jsp"

# urlopen 으로 데이터 가져오기
res = req.urlopen(url)

soup = BeautifulSoup(res, "html.parser")

# 원하는 데이터 추출
title = soup.find('title').string
wf = soup.find('wf').string

print(title)
print(wf)
~~~

### CSS 선택자 사용하기
- BeautifulSoup는 자바스크립트 라이브러리인 jQuery처럼 CSS 선택자를 지정해서 원하는 요소를 추출하는 기능 제공

|**메서드**|설명|
|-----------|---|
|soup.select_one(\<선택자>|CSS 선택자로 요소하나를 추출|
|soup.select(\<선택자>)|CSS 선택자로 요소 여러 개를 리스트로 추출|

~~~python
from bs4 import BeautifulSoup
html = """
<html><body>
<div id="meigen">
    <h1>위키북스 도서</h1>
    <ul class='items'>
        <li>유니티 게임 이펙트 입문</li>
        <li>아이폰 앱 개발 교과서</li>
        <li>웹사이트 디자인의 정석</li>
    </ul>
</div>
</body></html>
"""
soup = BeautifulSoup(html, 'html.parser')

# 필요한 부분을 CSS쿼리로 추출하기
# 타이틀 추출
h1 = soup.select_one("div#meigen > h1").string
print('h1 = ', h1)

li_list = soup.select("div#meigen > ul.items > li")
for li in li_list:
    print('li = ', li.string)
~~~

### 실제 환율 정보 추출
~~~python
from bs4 import BeautifulSoup
import urllib.request as req

# HTML 가져오기
url = 'https://finance.naver.com/marketindex/'
res = req.urlopen(url)

# HTML 분석하기
soup = BeautifulSoup(res, "html.parser")

#원하는 데이터 추출
price = soup.select_one("div.head_info > span.value").string
print('usd/krw = ', price)

# usd/krw =  1,183.50
~~~


