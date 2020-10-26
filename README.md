평점 기반 도서 추천
=======================
본 내용은 요약본입니다.        
자세한 내용은 블로그에서 확인하실 수 있습니다.             
https://w-storage.tistory.com/33      
1.데이터 수집
-----------------         
kaggle dataset을 사용했다.
https://www.kaggle.com/bahramjannesarr/goodreads-book-datasets-10m             
2.추천 시스템의 종류
------------------
1) 콘텐츠 기반 필터링                       
> 사용자가 선호하는 아이템을 확인하고 아이템과 유사한 특성을 갖는 다른 아이템을 추천한다.                  
2) 최근접 이웃 협업 필터링                       
> 최근점 이웃 협업 필터링은 타겟 사용자와 유사도가 높은 다른 사용자의 평을 보고 추천 유무를 결정하는 시스템이다.                  

3.데이터수집 및 전처리
----------------------------             
본 프로젝트에서는 user_rating_0_to_1000.csv파일 1개만을 사용했다.          
해당 데이터는 1,000명의 사용자 평점 데이터를 갖고 있다.                   
<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwaG8Y%2FbtqLSOF85M8%2F0EuBt9RxOoa0t0P1xlakyk%2Fimg.png"></img>                   
1) ID                     
0~999ID를 갖는 1,000명의 사용자가 존재                   
사용자 빈도수 그래프              
<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFUebV%2FbtqLRkS5GsJ%2FhgkqzKa7x3htVeC68UrEKk%2Fimg.png"></img>                  

2) Name            
도서명이다. 중복되는 이름의 도서가 존재할 수 있다.

3) Rating              
사용자가 매긴 평점이다. 'This user doesn't have any rating', 'did not like it', 'it was ok', 'liked it', 'really liked it', 'it was amazing'로 구성되어있다.                       
문자열은 사용하기 불편하기에 각각 0, 1, 2, 3, 4, 5점으로 치환했다.       
평점 구성
<img ars= "(https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhJmy4%2FbtqLIInEFww%2FaeBkHvpRPmi4pKt7ZnOzIk%2Fimg.png"></img>                     
                 
4.도서 추천 알고리즘 개발
------------------------------------------
1) 코사인 유사도를 사용하여 도서들간의 유사도를 측정했다.                
<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbYmVop%2FbtqLQbIS3qV%2FUZWgg5IRZ0VSSzCFkRfmDk%2Fimg.png"></img>                  
2) 아래 공식을 이용해 예측 평점을 계산했다.                   
<img src= "https://user-images.githubusercontent.com/25631105/97192518-51ad5700-17eb-11eb-96b4-8a5c1de8d1ea.gif"></img>                    
3) 수행결과 MSE는 약7.48이 나왔다.                 
4) 모델 개선을 위해 특정 아이템을 비교할 때 유사도가 높은 아이템만 비교했다.                 
5) 개선된 모델의 MSE는 약 3.89가 나왔다.                      
6) 1번 유저에게 도서 추천                          
<img src= "https://user-images.githubusercontent.com/25631105/97192836-aa7cef80-17eb-11eb-94b8-3b6318f2b85e.png"></img>                

5. 결론
---------------------------
사용자가 도서에 매긴 평점을 기반으로 추천 시스템을 만들었다.                    
추천된 도서를 실제로 사용자가 읽었는지, 평점을 매겼는지 알 수 없기에 MSE를 평가 지표로 삼았다.                    
입력 데이터의 일부를 제거하여 추천 도서에 제거된 데이터가 있는지 확인하는 방식으로 정확도를 계산할 수 있을 것 같다.                    
향후 행렬분해방식, 콘텐츠 기반 추천 서비스를 이용하는 프로젝트도 진행해보고 싶다.                    

6. 아쉬운 점, 더 해봐야 할 것들
----------------------------------------------
1) 새로운 사용자, 새로운 도서가 추가된다면 4에서 수행한 작업을 다시 수행해야 한다. 사용자, 도서의 추가, 제거에 따른 유연한 대처 방법은 없을지 고민해보고 싶다.                    
2) 행렬분해, 콘텐츠기반 등 다른 추천 방식을 이용했을 때 차이를 확인해보고 싶다.                    
3) 신경망을 이용한 추천 프로젝트를 진행하고 차이점을 확인해보고 싶다.                           