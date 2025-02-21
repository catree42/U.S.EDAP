# U.S EDAP

<p>United States Economy Data Analysis Program</p>

## Description

### 개요
<p>개발 기간 : 2024.07.11 ~ 2024.07.19(presentation)</p>
<ul> 
    <li>현재까지 기록된 미국의 여러 경제지표 데이터를 크롤링하고 다중 차트로 시각화한다.</li>
    <li>또한 Google Trends에서 특정 연도에 해당하는 상위 검색어를 추출해 워드 클라우드로 시각화한다.</li>
    <li>이러한 기능들을 활용해 경제지표 간의 상호 연관성과 경제 위기가 발생했을 때 경제지표가 어떻게 반응하는지 분석했다.</li>
</ul>

### Structure
![image](https://github.com/user-attachments/assets/ec16f079-b213-4996-b457-21df0cfcd42f)  

  
#### Crawler
    
![image](https://github.com/user-attachments/assets/57980013-9ead-45a0-820b-498250223845)
![image](https://github.com/user-attachments/assets/d8c8a611-d431-4aca-8422-c5759e489884)
<ul>
    <li>Feds 결정금리, CPI 물가지수, 13 week T-bill 채권 수익률, S&P500 주가지수, Bitcoin, Gold 시세 총 6가지 경제지표를 데이터가 존재하는 가장 긴 기간만큼 크롤링하는 클래스를 작성했고 각각의 모듈로 만들었다.</li>
    <li>각 클래스는 crawl() 메서드를 가지며 해당 메서드는 각자가 가진 url을 크롤링해 dataFrame에 저장하고 csv파일을 생성한다. 크롤링한 데이터가 저장된 dataFrame을 반환한다.</li>
    <li>금리, 물가지수는 Investing.com 에서 Json파일을 크롤링했고, 이 외에 경제지표는 yahoo finance 웹사이트에서 Beatiful Soup 라이브러리를 이용해 크롤링하였다.</li>
</ul>
    
#### Trends Crawler
![image](https://github.com/user-attachments/assets/d59b3618-8c58-40dc-a498-dbd031b93f56)
<ul>
    <li>Feds 결정금리가 급락했을 때 어떠한 사회적·경제적 이슈가 있었는지 보기위해 Google Trends 검색어를 가져오는 클래스이자 모듈이다.</li>
    <li>crawl() 메서드를 가지며 파라미터로 연도(year)를 받아 Google Trends에서 입력받은 연도의 상위 검색어 10개를 가져와 dataFrame을 만든다.</li>
    <li>검색어 10개를 워드클라우드 이미지로 만들어 시각화한다.</li>
</ul>
  
 #### Main

 ![image](https://github.com/user-attachments/assets/656c7f38-34d3-4ad9-8322-4394d11c479f)
 <ul>
     <li>Jupyter notebook 형식의 파일로 Google colab에서 실행해야한다. clone github, install requirement, import Crawler module 하는 코드들이 선행된다. </li>
     <li>각 크롤러의 crawl 메서드를 실행해 각 경제지표들의 dataFrame을 만들고 비교 분석을 원하는 경제지표들을 차트로 시각화한다.</li>
     <li>차트로 시각화 하는 함수는 create_Chart() 함수로 dataFrames, titles를 담은 dictionary를 키워드인자로 받는다. 키워드 인자로 경제지표들의 데이터프레임을 받아 최소 1개, 최대 4개의 경제지표를 한 차트에 시각화가 가능하게 했다. </li>
     <li>차트 시각화는 plotly 라이브러리를 이용했다. plotly가  matplot 라이브러리보다 디자인이 예쁘고 cursor hover 시 데이터 정보를 볼 수 있어서 UX가 더 좋다고 느꼈다. </li>
 </ul>

 ## 실행 및 주요 분석 결과
 #### 실행 코드 : create_Chart() 함수에 원하는 경제지표들의 dataFrame, titles 딕셔너리에 담아서 인자로 주면 된다.
 ![image](https://github.com/user-attachments/assets/69180535-9afc-49cf-a290-c77046f8947a)
   
   
 #### 금리-물가 간 연관성 : 물가상승률이 상승하면 금리를 인상해 인플레이션을 조정한다. 물가가 상승했을 때 금리를 인하하거나 동결한 시기는 경기 불황에 빠졌을 때다.
 ![금리-물가](https://github.com/user-attachments/assets/ec17c569-0acd-416b-9311-bebd201248be)  

    
 #### 금리-채권 : 단기 채권은 금리 결정에 많은 영향을 받아서 금리와 거의 동일하게 움직인다.
 ![금리-채권](https://github.com/user-attachments/assets/f0f057f3-7855-43d6-8a5c-b2eab6de1014)  

       

 #### 금리-주가 : 2007년 금리를 인하하고 낮은 금리 유지하면서 주가가 상승했다. 2021년 금리를 인상하자 주가가 하락했다.<br> 금리를 낮추면 민간·기업의 소비·투자가 활발해지면서 주가가 오르고 경기가 회복된다. 경기가 과열되어 인플레이션률이 오를 때 금리를 인상하여 소비여력을 낮춰서 인플레이션률 완하시킴. 이 과정에서 주가가 하락한다.
 ![금리-주가](https://github.com/user-attachments/assets/e6a6c76e-a553-4d9d-9d22-de6000e3d323)  
   
  
 #### 주가-비트코인 : 비트코인 증시의 hedge성 자산으로 주가와 반대방향으로 움직일 거라 생각했지만 비슷한 방향으로 움직였다. 비트코인을 증시의 hedge로 투자하지 않는다는 것을 알 수 있다.<br> *hedge : 가격변동의 위험을 상쇄하는 자산 즉 주 투자종목과 반대로 움직이는 보험성을 가지고 있음
 ![주가-비트코인](https://github.com/user-attachments/assets/1016c5a3-6afb-41a2-807a-6a28735f1598)   

    
 #### 경제 위기 발생 시 금리 변동 : 금리가 급락한 시기는 2000년, 2008년, 2020년이며 낮은 금리를 유지한 시기는 2008 ~ 2015, 2019 ~ 2021이다.<br> 대표적으로 2008년을 Trends Crawler에 넣어 워드클라우드를 만들어보았다. 2008년의 구글 검색 트렌드를 시각화한 결과 서브프라임모기지 사태와 그로 인한 경기 침체 사태에 대한 키워드들이 검색량 상위에 있는 것을 확인할 수 있다. 
 ![금리](https://github.com/user-attachments/assets/241f22f3-afca-407c-8ec0-395a673bc934) 
 ![Image](https://github.com/user-attachments/assets/9dd449e5-1e36-4509-bedb-c2602a820753)

    
 #### 경제 위기 발생 시 금 시세 변동 : 금리가 급락한 시기에 금 시세가 급등했다. 경제가 불황에 빠질 때 금 수요가 상승함. 금은 어디서나 가치가 통용되기때문이다.
 ![금리-금](https://github.com/user-attachments/assets/33e4c2b6-ce15-4952-bb1e-56c752099c9e)  

    
 ## 향후 발전 계획 
 다가오는 9월 미국의 금리를 결정하는 연방준비기금, Feds의 금리인하는 거의 확정적인 상태다. 그래서 Regression Machine Leaning 모델에 위 경제지표 데이터들을 학습해 금리를 0.25bp, 0.5bp 등으로 내렸을 때 어떠한 변동이 올 지 예측하는 프로그램을 만들고 싶다. 
 
 ## Getting Started

### Dependencies
<ol>
    <li>Execution Environment : Google Colab</li>
     <li>Language : Python</li>
    <li>Library
        <ol>
            <li>Crawling Data : Beautiful Soup, pytrends</li>
            <li>Data Visualizing : plotly, tqdm.notebook, wordcloud, cv2, google.colab.patches</li>
            <li>Google Trends : pytrends</li>
        </ol>
    </li>   
</ol>
<!--
* Describe any prerequisites, libraries, OS version, etc., needed before installing program.
* ex. Windows 10
-->

### Installing
<p>
    I already wrote codes in main.ipynp to install packages on requirements.txt and clone this repository. So you can just go to the next section : )
</p>
<!--
* How/where to download your program
* Any modifications needed to be made to files/folders
-->

### Executing program
<ol>
    <li>Please just copy this url and paste on the website to execute the program. I found a problem to use this link below : (    
        <a href src="https://colab.research.google.com/github/catree42/U.S.EDAP/blob/main/main.ipynb">
            https://colab.research.google.com/github/catree42/U.S.EDAP/blob/main/main.ipynb    
        </a>
    </li>
    <li>
        Uncomment codes for cloning github, cd(chage directory), import TrendsCrawler.  
        I comment out these codes to execute the program on Pycharm but they need to be uncomment to be executed on Google colab.
    </li>
    <li>I hope you have fun with our program : )</li>
</ol>

<!--
* How to run the program
* Step-by-step bullets
```
code blocks for commands
```
-->

<!--
## Help

Any advise for common problems or issues.
```
command to run if program contains helper info
```
-->

## Authors

|담당|내용|Contact|    
|:--:|--|--|
|Giuk|기획, Feds·CPi· Trends Crawler, Data Visualiztion|catree42@gmail.com|
|김창회<br>|SPX Crawler|cdkghl852@naver.com|
|김현승<br>|T-bill Crawler|unchaincom@naver.com|
|송요섭<br>|Gold Cralwer|sys1554@naver.com|
|정현두<br>|Bitcoin Crawler|jhd6290@gmail.com|

<!--
## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under the [NAME HERE] License - see the LICENSE.md file for details

## Acknowledgments

Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)
-->
