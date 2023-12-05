# Netflix_original_project 

## 1. Introduction
### This project was done to review what i learned in terms of 'EDA Analysis','Data Visualization' and 'Statistical Hypothesis Test'. The main focus of this project is to analyze the data of 'Netflix Original Series' and to test if the hypotheses are agreeable by utilizing 'T-test' method. 
### The dataset was retrieved from Kaggle 'Netflix Original Films &amp; IMDB Scores'(link: https://www.kaggle.com/datasets/luiscorter/netflix-original-films-imdb-scores).


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

### **3. 컬럼제거**

   (1) [Premiere]컬럼의 값들을 value_counts()로 확인해 본 결과, 1~5의 값을 골고루 가지며, 특정일자에 집중된다던지 하는 현상이 보이지 않았다. 따라서, '개봉일자'는 평점에 큰 영향을 주지 않는다고 판단하여, 컬럼을 제거하기로 결정 하였다.
    
   ```
   df["Premiere"].value_counts()
   ```

### **4. 컬럼 특성 파악**
   
   (1) 컬럼 [Language] & [Genre] value_counts()에 10 이상이라는 조건을 달아 본 결과, [Language]컬럼은 'English'에 ["Genre"]컬럼은 'Documentary'컬럼에 쏠려 있는 현상을 볼 수 있었다 

   ```
   df["Language"].value_counts()[df['Language'].value_counts() >= 10]
   df["Genre"].value_counts()[df['Genre'].value_counts() >= 10]
   ```

   ![1](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/43474e0f-ac76-4820-af21-d8ae74c13c49)


   ![2](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/b6051e80-d431-4e49-8e1c-24db34673dc7)


   (2) 컬럼 [Runtime]: hisplot을 그려본 결과 100분대의 영화가 압도적인 수를 차지한 것을 확인 할 수 있다. 

   ```
   df["Runtime"].hist()
   ```

   ![3](https://github.com/ryeonbeenkang/NF_original_project/assets/47935123/7960bb24-7606-4047-ac3d-6783dd84a72f)

   

## 3. T-test(One-sample, two-sample, pair-sample)



## 4. Implication & recommendation on new Netflix original Series production




## 5. Insights




# Difficulty & Limitation



