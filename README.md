# Netflix_original_project 

## 1. Introduction
### This project was done to review what i learned in terms of 'EDA Analysis','Data Visualization' and 'Statistical Hypothesis Test'. The main focus of this project is to analyze the data of 'Netflix Original Series' and to test if the hypotheses are agreeable by utilizing 'T-test' method. 
### The dataset was retrieved from Kaggle 'Netflix Original Films &amp; IMDB Scores'(link: https://www.kaggle.com/datasets/luiscorter/netflix-original-films-imdb-scores).


![nf](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/de53d1a0-ad7b-4deb-bee9-ef75b1f0de7c)



## 2. EDA Analysis & data visualization
### **1. 컬럼 파악**:
   
![dtypes](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/0db869af-ccbc-406f-bbeb-ce47f73f37c2)

총, 6가지 컬럼으로 구성



### **2. 결측치**
   
   (1) 116번째 row에 [Language]의 값이 null이고, [IMDB Score]가 'English'로 잘 못 표시된 row를 제거.
 ![ng_row](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/8e491339-7b72-4bd8-9966-af55c9507eb3)
   ```
    df = df.drop(116)
   ```

   (2) 그 외에는 결측치가 존재하지 않으며 아래의 코드로 확인해 본 결과 모든 컬럼의 값은 0이 되었다
   
   ```
   df.isnull().sum()
   ```


### **3. 컬럼제거**

   (1) [Premiere]컬럼의 값들을 value_counts()로 확인해 본 결과, 1~5의 값을 골고루 가지며, 특정일자에 집중된다던지 하는 현상이 보이지 않았다. 따라서, '개봉일자'는 평점에 큰 영향을 주지 않는다고 판단하여, 컬럼을 제거하기로 결정 하였다.
    
   ```
   df["Premiere"].value_counts()
   ```

### **4. 컬럼 특성 파악**
   
   (1) 컬럼 [Language] & [Genre] value_counts()에 10 이상이라는 조건을 달아 본 결과, [Language]컬럼은 'English'에 ["Genre"]컬럼은 'Documentary'컬럼에 쏠려 있는 현상을 볼 수 있었다 

   ```
   df["Genre"].value_counts()[df['Genre'].value_counts() >= 10]
   df["Language"].value_counts()[df['Language'].value_counts() >= 10]   
   ```

   ![1](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/43474e0f-ac76-4820-af21-d8ae74c13c49)


   ![2](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/b6051e80-d431-4e49-8e1c-24db34673dc7)


   (2) 컬럼 [Runtime]: hisplot을 그려본 결과 100분대의 영화가 압도적인 수를 차지한 것을 확인 할 수 있다. 

   ```
   df["Runtime"].hist()
   ```

   ![3](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/7960bb24-7606-4047-ac3d-6783dd84a72f)


   (3) df.info()를 통해 [IMDB Score]컬럼은 Dtype이 object였으므로, T통계량 계산을 위해 Dtype을 float로 변경


   ```
   df["IMDB Score"] = df["IMDB Score"].astype(float)
   ```

   

## 3. T-test(One-sample, two-sample, pair-sample)

   ** T-test에 앞서 ["Genre"]와 ["Language"]컬럼은 수치 데이터의 형태가 아니므로, LabelEncoder()를 활용해 수치화 작업 실시 **

   ```
   df["is_genre"] = label_encoder.fit_transform(df["Genre"])
   df["is_language"] = label_encoder.fit_transform(df["Language"])
   ```
   

   **(가설1) 장르별 1위 Documentary장르와 2위 Drama장르의 차이는 유의미 한지?**
   
   
   ```
   # Documentary의 label encoding 한 수는 45
   genre_docu = df[df["is_genre"] == 45]["IMDB Score"]
   # Drama의 label encoding 한 수는 46
   genre_drama = df[df["is_genre"] == 46]["IMDB Score"]
   ```
   
   각 변수로 지정해 준 이후 T통계량과 Pvalue를 계산

   ```
   from scipy.stats import ttest_ind

   t_statistic, pvalue = ttest_ind(genre_docu, genre_drama)
   
   print(f"T통계량: {t_statistic}")
   print(f"Pvalue: {pvalue}")
   ```

   결과:
      T통계량: 5.2295343458734544
      Pvalue: 3.767793451079555e-07

   <통계적 가설 검정 >
   1. 귀무가설, 대립가설, 유의수준 설정
    - 귀무가설: 1위 Documentary와 2위 Drama의 차이는 없다
    - 대립가설: 1위 Documentary와 2위 Drama의 차이는 유의미 하게 있다
    - 허용가능한 1종 오류의 최대수준(유의수준): 0.05
 
   2. 검정통계량 계산
    -  5.2295343458734544
   
   3. P-value계산
    - 3.767793451079555e-07
   
   4. 통계적 의사결정
    - p-value가 유의수준 0.05보다 작으크로 기무가설을 기각하고, 대립가설을 채택한다. 즉, 1,2위의 차이는 유의미 하다

   

   **(가설2) 언어별 1위 English와 2위 Hindi언어의 차이는 유의미 한지?**




## 4. Implication & recommendation on new Netflix original Series production




## 5. Insights




## 6. Difficulty & Limitation



