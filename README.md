# tableau_practice

여지껏 태블로나 다른 BI툴을 거의 사용한 적이 없이 항상 파이썬 내장 패키지나 plotly를 이용해서 시각화를 해 왔었기에 태블로를 처음부터 배울겸 태블로 자격증 공부도 같이 하기로 하였다.
무료 버전인 태블로 퍼블릭을 이용

* 태블로에는 SQL의 조인 기능이 있지만, 그와 유사한 '블렌딩'과 '관계' 라는 기능도 있었다. 둘 다 조인과 유사하지만 또 한편으로는 매우 다른데, 조인은 물리적으로 테이블들을 합치는 것이지만, 이 둘은 그렇지 않다. 블렌딩의 경우 만약 서로 다른 2개의 데이터 소스를 이용하여 시각화를 할 경우, 만약 그 2개의 데이터 소스 사이에 공유하는 컬럼이 있다면 하나의 데이터 소스로 합치지 않고도 연결하여 시각화를 할 수 있다. 만약 실시간으로 들어오는 데이터와 기존에 가지고 있는 어떤 파일을 동시에 이용하여 시각화를 하고자 한다면, 블렌딩을 이용하면 좋을 것 같다. 관계의 경우, 블렌딩과 유사하지만 태블로의 데이터 원본 탭에서 처음부터 데이터들간의 관계를 등록하고 이 데이터들을 불러온 채로 진행하는 것이다.  
태블로에서는 조인을 되도록이면 지양하는 편이 좋은 이유가, 조인의 경우 처음부터 물리적으로 테이블을 합치므로 시간과 데이터의 용량이 크게 늘어날 수도 있지만, 관계나 블렌딩의 경우 시각화를 하는 단계에서만 결합을 한 뒤에 집계를 하여 시각화를 하므로 시간과 용량 측면에서 훨씬 절약이 가능하기 때문이다.

* 태블로를 학습하다가 직접 이것저것 시도해 보던 중, 원하는 정보를 시각화 하는것이 쉽지 않았다. 원하는대로 데이터가 필터링 되는 느낌이 아닌 듯한 느낌이 들어 찾아보니, 태블로에는 기본적으로 어떤 순서로 작동하는지에 대한 Order of Operations가 있다고 한다. 마치 SQL에서 select가 첫 문장에 오지만 순서로는 from, where, group by, having 다음에 오는 것처럼, 화면에 보이는 데이터에 대해서 적용하는 것처럼 보여도, 그 뒤나 그 전에 필터가 적용되어서 원하는 필터를 적용하지 못한 것 같다.  
* 
![OrderofOperations-1](https://github.com/jihun0423/tableau_practice/assets/131629615/e5772c1c-11bc-4a8a-ac4d-227cda2b9f2b)



* 어제에 이어서 Order of Operations에 대해 학습하였다. 아무래도 이걸 이해하는 것이 앞으로 태블로 활용에 있어서 가장 큰 단계일 것 같다. set(집합)으로 설정한것이 먼저 작동한뒤, 필터가 적용된다. 예를들어 매출 상위 10개의 제품이 IN에 포함되게 하는 집합을 생성했고, 그 뒤에 제품의 카테고리가 악세서리 인 품목만 가져오게 필터를 적용했을 시, 필터가 나중에 적용되어 10개보다 적은 항이 나올 수 있다는 뜻이다.
만약 악세사리인 품목들 중 상위 10개를 가져오고 싶다면, 악세사리 필터를 컨텍스트 필터로 바꿔주면 된다. (컨텍스트 필터는 데이터 원본 전체에서 먼저 적용되는 필터이다)

* 그래프에 참조선, 추세선을 추가하는 방법에 대하여 학습을 하였다. 추세선이 단순 1차 회귀선이 아닌 다항회귀도 지원하며, 심지어 F값의 p-value와 R^2값까지 나와서 놀라웠다. 오랜만에 통계량들을 봐서 반가웠다.

* nested sort (중첩 정렬) 에 대해 유의할 필요가 있다. 만약 나라별 카테고리별 판매수를 막대그래프로 나타냈을 때, 카테고리를 컬러에 올릴 경우 기본적으로 비중첩 정렬 (각 나라마다 막대의 색깔 순서가 똑같음) 상태이고, 필드(카테고리)에서 정렬 버튼을 눌렀을 때 역시 비중첩 정렬 상태이다. 카테고리들의 이름의 알파벳 순서로 정렬이 되기 때문이다.  값이 있는 축에서 정렬을 할 경우, 값에 따라 오름차순이나 내림차순으로 중첩 정렬이 된다. 이 경우에는 막대의 색깔이 나라마다 제각각이다.

* 매개변수와 동작, 필터 등을 어떻게 잘 활용하는 지가 태블로 실력의 가장 큰 부분 같다. 대시보드에 만든 여러개의 시트들을 옮긴 뒤, 매개변수나 필터를 적용해 그 시트들이 한번에 촤르륵 바뀌는게 뭔가 속이 시원했다. plotly도 이런 기능이 가능은 했다만, 코딩할 때 따로 뭔가를 추가해 주기도 해야하고 매우 번거로웠는데 태블로는 너무 간편하게 이런 기능도 추가가 가능해서 놀라웠다.

* 대시보드의 경우 같은 시트를 여러번 사용하는 것은 불가능한 반면, 스토리의 경우는 가능했다. 만약 어떤 시트에 대해서 전체적으로 보여준 뒤, 필터를 적용해서 더 강조하고 싶은 부분을 정해서 보여준다던지 하는 방법으로 활용이 가능할 것 같다. (1년간의 달 마다의 전체 매출을 보여준 후, 다음 화면에서 그 중 특정 카테고리의 매출을 보여준다던가 하는 방법으로..) 
