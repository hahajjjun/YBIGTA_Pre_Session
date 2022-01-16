# Session 4. Pandas and Numpy

# Pandas Cheatsheet

## 1. Pandas Series

- **Define Series**
    
    ```python
    series1 = pd.Series([1,6,7,3]) #시리즈 생성
    series1_ = pd.Series([1,6,7,3], index = ["A","B","C","D"]
    series2 = pd.Series({'A': 90, 'B': 80}) #딕셔너리로 생성
    ```
    
- **Methods of Series**
    
    ```python
    series1.values #값 확인
    sereis1.index #인덱스 확인
    series1.dtypes #자료형
    series2.name = '학점 기준'
    series2.index.name = '학점' #시리즈 이름, 인덱스 이름 설정
    series1.index = ['W','X','Y','Z'] #인덱스 변경
    ```
    
    ```python
    # Indexing
    series1['X']
    series1.X
    series1[['X','Z']]
    series1[[0,2]] # 0th, 2nd index values
    series1[0:2] # offset index
    series1['W':'Y'] # slicing by index values
    ```
    
    ```python
    # Data Filtering
    series1[series1 > 5]
    
    # Series 연산
    series_1 = pd.Series([1,2,3,4])
    series_2 = pd.Series([5,6,7,8])
    print(series_1 + series_2) # element-wise operation
    print(series_1 / series_2) # datatype이 자동으로 바뀜
    
    # pd.Series가 숫자로 구성될 경우 numpy array처럼 취급
    # s = np.subtract(s1, s2)도 가능
    # s = s1.sub(s2) 역시 가능
    
    # 모든 연산은 인덱스 기준으로 같은 인덱스끼리 element-wise하게
    # 인덱스가 다르면 s1 + s2 : concat처럼 뒤에 붙음
    ```
    
- **pd.concat**
    
    ```python
    S1 = pd.Series([1,2,3])
    S2 = pd.Series([4,5,6])
    
    pd.concat([S1,S2]) # default axis = 0(세로로 더하기)
    
    # Returns [1,2,3,4,5,6] with index [0,1,2,0,1,2]
    # S1 + S2 gives [5,7,9]
    
    pd.concat([S1,S2], axis = 1) #axis = 1(가로로 더하기)
    ```
    
- **pd.drop()**
    
    ```python
    S = S1.drop(0) # 여기서 0은 0번째가 아니라, index 번호 의미
    S.index = ['a','b'] # 인덱스 변경
    S.drop(0) # raise Error
    ```
    
- **결측치 채우기**
    
    ```python
    S = pd.Series([3,4,np.nan,5,6,np.nan])
    S.isnull() # check NaN
    S[S.notnull()] # NaN 아닌 값들만 추출
    S.dropna() # S에서 NaN 제거한 Series 반환, S에 직접 영향을 주지는 X
    S.fillna(S.mean()) # 평균으로 결측치 채움, S에 직접 영향 주지 않음
    ```
    

## 2. Pandas DataFrame

- **데이터프레임 생성**
    
    ```python
    df1 = pd.DataFrame(columns = ['Food', 'Price']) # 컬럼명만 전달
    df1['Food'] = ['마라샹궈', '마라탕']
    df1['Price'] = [15000,8000] # 리스트로 생성
    
    #딕셔너리로 생성
    food = ['A','B'] #컬럼명
    price = [100,200]
    dic = {'food' : food, 'price' : price}
    df2 = pd.DataFrame(dic, index = [0,1]) #인덱스명
    
    # 컬럼을 인덱스로 설정
    df2.set_index('food')
    ```
    
- **데이터프레임 인덱싱**
    
    ```python
    # indexing, slicing 방법 외에..
    df2.loc['A'] # index의 값으로 찾기
    df2.iloc[0] # index 순서로 찾기(번째)
    df2.iloc['A'] # raise error
    # 조건으로 접근하는 것도 가능
    
    df.loc[3] = ['a',700] # 이렇게 새로운 row를 추가, 변경
    df['price'][3] = 100 # 변경
    df = df.drop(2, axis = 0) #2번째 row drop, axis = 0(default)
    
    # 해당 데이터프레임에서 삭제 : inplace = True
    df.drop(1, inplace = True)
    df_ = df.reset_index(drop = True) # 인덱스를 0,1,2..로 리셋, 원래 index는 삭제함
    ```
    
- **pd.concat()**
    
    ```python
    pd.concat([df1,df2], axis=0) #default axis = 0
    pd.concat([df1,df2], axis=1, join='inner') #join : inner(index 교집합만 concat), outer(index 합집합 concat)
    # size가 같지 않아도 index 기준으로 합침, 빈 곳은 NaN 채움
    ```
    
- **pd.merge()**
    
    ```python
    # 특정 column 값을 기준으로 merge 가능
    pd.merge(df1, df2, how = 'left', on = 'food') # 'left', 'right', 'inner', 'outer'
    ```
    
- **pd.join()**
    
    ```python
    # index 기준으로 merge하는 것과 유사하게 수행
    pd.join(df1, df2, how = 'left')
    ```
    
- **df.apply(lambda x : f(x))**
    
    ```python
    df.apply(lambda x : x**2)
    
    # 혹은 함수를 따로 정의해 사용할 수도
    def lambda_func(...):
    	...
    
    df.apply(lambda_func)
    ```
    
- **df.info() : 데이터프레임 컬럼별 속성(datatype, 결측치 여부..) 확인**
- **df.describe() : 수치형 변수 컬럼별 통계량 확인**
- **df.sort_values()**
    
    ```python
    df.sort_values('Price', ascending = False) # df 자체를 변화시킬 순 없음
    df = df.sort_values('Price') # 이렇게 대입해줘야 함
    ```
    
- **df.unique().value_counts()**
    
    ```python
    df.unique() # 집합화
    df.unique().value_counts() # 몇 개 종류의 데이터로 구성되어 있는지 확인
    ```
    
- **df.groupby()**
    
    ```python
    df.groupby(["Pclass", "Sex"]).size() # 두 개 컬럼에 대해 그룹화 가능, size()로 개수 확인
    df.groupby(["Pclass", "Sex"])['Fare'].mean() # "Plass", "Sex"로 그룹화한 다음 그룹별 'Fare'의 평균 구하기
    df.groupby("Pclass").agg((["min","max","mean"]))
    ```