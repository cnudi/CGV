# Community-Enhanced Graph Visualization Using Triangulation

삼각 분할을 이용한 군집 강조 그래프 시각화

*   참여 인원: 정수환, 박종민, 임성수 (충남대학교 [데이터인텔리전스 연구실](https://www.cnudi.com/))
*   관련 논문: [그래프 클러스터링을 위한 삼각 분할 기반 임베딩](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE09301897), [KSC 2019](https://www.kiise.or.kr/conference/main/index.do?CC=KSC&CS=2019)
*   연구 지원: 충남대학교 [바이오AI융합연구센터](https://bioai.cnu.ac.kr/*bioairc*/index.do)
*   코드 문의: 정수환 integerhwan@gmail.com

<br>

# 목표

본 프로그램은 주어진 그래프 데이터에 대해 군집 구조를 강조하여 표현해주는 그래프 시각화를 수행하는 것을 목표로 한다. 이를 위해 Python 3로 작성되었고 networkx, fa2l, matplotlib, scipy, numpy 패키지를 활용하여 소스코드를 작성하였다. 인터랙티브한 결과 도출을 위해 파이썬 노트북으로 작성한 코드로 배포하고자 한다

우리는 관심 있는 대상들과 이들 사이의 관계를 점과 선으로 단순화시켜서 그래프로 표현할 수 있다. 예를 들면, 소셜 네트워크의 각 구성원을 노드, 친교 관계를 링크로 나타낼 수 있다. 그래프의 구조를 분석하는 대표적인 방법으로 내부에서 밀집하게 연결되어 있는 부분 구조인 군집 구조를 찾는 클러스터링 문제가 있다. 밀집도를 정의하기 위하여 서로 다른 세 노드가 상호 연결되어 있는 삼각 구조가 얼마나 많은지 평가하는 방식이 널리 쓰이지만, 그래프 내부에는 수많은 삼각 구조가 존재하여 처리하기에 까다롭다. 본 프로그램은 그래프 시각화를 개선하여 그래프의 연결 구조를 보존하는 삼각 분할을 찾고, 이를 통해 군집 구조를 강조하는 그래프 시각화를 얻도록 했다.

그래프 시각화를 통해 주어진 그래프에 대한 단순화된 표현을 찾는 동시에 삼각 분할을 통해 그래프를 대표하는 삼각형 구조들을 찾는다. 이들의 장점을 취하여 주어진 그래프로 부터 삼각형들로 이루어진 희소 그래프 구조를 찾고, 각 삼각형의 강도는 주어진 그래프의 연결 유사도에 의해 정의되는 변환을 수행한다. 최종적으로 얻어지는 그래프 시각화는 군집 구조를 알아보기 쉽다는 특징을 가져서 유용하다.

<br>

# 기능

1. 프로그램 실행을 위한 준비 과정
프로그램 실행을 위하여 파이썬에서 활용 가능한 패키지를 설치 및 사용할 수 있다: networkx, fa2l, matplotlib, scipy, numpy. 이 중 networkx는 그래프 데이터를 입력, 저장, 분석하는데 필요한 패키지이며, fa2l은 기초 그래프 시각화를 위해 필요한 ForceAtlas2 실행을 위해 필요하다. 후자의 세 패키지는 파이썬 데이터 분석을 위해 사용하는 주요 패키지들로, 데이터의 표현 및 연산, 시각화 등에 있어서 다양한 기능을 제공한다. 오픈-소스 프로그래밍 언어 및 패키지의 다양한 기능을 활용하였다. 자세한 기능은 하단의 2~5에서 설명한다.

2. 그래프 데이터 입력 및 사용하기
networkx 패키지를 사용하여 그래프 데이터를 입력 받는 함수를 사용할 수 있다. 그래프의 연결 리스트를 파일로 입력 받고 이를 그래프로 변환해줄 수 있는 코드를 제공한다. 그래프의 연결 리스트는 각 줄마다 연결 형태를 두 개의 노드 번호가 나오며, 줄의 수가 전체 연결의 수와 같다. 또한 기본적으로 방향성이 없는 그래프를 가정하였다. 추가적으로 그래프 출력을 위한 코드를 제공한다.

3. 기초 그래프 시각화: 파이썬 그래프 시각화
파이썬 그래프 시각화에서 널리 쓰이는 ForceAtlas2의 시각화 방식인 LinLog 시각화를 수행하는 함수를 제공한다. 이는 LinLog 시각화를 통한 그래프 시각화 결과는 각 노드의 위치 정보를 반환하며, 각 노드의 위치를 positions에 저장하여 활용할 수 있게 해준다. 또한, 각 노드의 위치를 평면 상에 점으로 표현하고, 연결을 선으로 표현하여 그래프를 출력할 수 있도록 해준다.

4. 삼각 분할: 그래프 시각화 결과에 삼각 분할 적용
Delaunay 삼각 분할을 사용하여 노드 위치 정보에 삼각 분할을 적용하는 코드를 제공한다. 이를 위해 networkx를 통해 얻은 positions를 Delaunay에 입력 가능한 형태로 변환하는 방법을 설명한다. 그 결과, 기존의 그래프와 달리 삼각 구조로 연결이 이루어지는 희소화된 그래프 형태가 반환되는 것을 알 수 있다. 이를 통해 삼각 구조 기반의 그래프를 얻을 수 있다.

5. 최종 그래프 시각화: 유사도를 고려한 군집 강조 시각화
앞의 4에서 얻은 결과는 삼각 구조 기반의 그래프를 보여주고 있다. 이 중 주요 연결, 강한 군집 구조를 나타내는 연결을 시각적으로 알아보기 쉽게 표현하기 위해서 연결의 유사도를 계산할 수 있도록 한다. Jaccard 유사도를 활용하여 연결된 두 노드 간 유사도를 통해 정의하고, 높을수록 굵고 진하게 표현하였다.
