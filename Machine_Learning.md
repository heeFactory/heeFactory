 Hands-On Machine Learning with Scikit-Learn & TensorFlow
========================================================
Sohee Hwang, Start: 2019/8/8 Last Modified: 2019/11/18
--------------------------------------------------------

# Chapter1. 한눈에 보는 머신러닝

## 1.1. 머신러닝이란?
> 머신러닝이란, 명시적인 프로그래밍 없이 컴퓨터가 학습하는 능력을 갖추게 하는 연구 분야다.<br>
> 어떤 작업 T에 대한 컴퓨터 프로그램의 성능을 P로 측정했을 때 경험 E로 인해 성능이 향상됐다면, 이 컴퓨터 프로그램은 작업 T와 성능 측정 P에 대해 경험 E로 학습한 것이다.

## 1.2. 왜 머신러닝을 사용하는가?
> 머신러닝 기술을 적용하게 되면 대용량의 데이터를 분석하면 겉으로는 보이지 않던 패턴을 발견할 수 있기 때문이다.
>> * Ex1. 스팸 필터를 예로 들었을 때, 자주 등장하는 단어를 직접 업데이트 해주지 않아도, 자동으로 스팸을 분류해줌.<br>
>> * Ex2. Speech recognition의 경우, 'one'과 'two'의 사운드를 구분하는 프로그램을 작성할 때, 전통적인 방식으로는 하드코딩이 답이지만 머신러닝을 사용하면 간단해짐.

## 1.3. 머신러닝 시스템의 종류
총 3가지의 분류 기준으로 분류 가능
1. 사람의 감독 하에 훈련하는 것인지 그렇지 않은 것인지
2. 실시간으로 점진적인 학습을 하는지 아닌지
3. 단순하게 알고 있는 데이터 포인트와 새 데이터 포인트를 비교하는 것인지 아니면 훈련 데이터셋에서 과학자들처럼 패턴을 발견하여 예측 모델을 만드는지

> ### 1.3.1 지도학습과 비지도학습<br>
>> **학습하는 동안의 감독 형태나 정보량** 이 기준<br>
>>> #### 지도학습<br>
>>> * 알고리즘에 주입하는 훈련 데이터에 레이블이라는 원하는 답이 포함됨<br>
>>> * **분류**가 가장 대표적인 지도학습 작업(스팸필터)<br>
>>> * **회귀**가 그다음으로 대표적인 지도학습 작업 (예측변수라 부르는 특성(feature)을 사용해 타겟 수치를 예측하는 것)<br>
>>> * k-NN / Linear Regression / Logistic Regression / SVM / Decision Tree / Random Forest / Neural Network<br>
>>> #### 비지도학습<br>
>>> 훈련데이터에 레이블이 없어서 시스템이 아무런 도움 없이 학습해야하는 방법<br>
>>> * Clutsering (K-Means, HCA, Expectation Maximization)<br>
>>> * Visualizaition & dimensionality reduction(PCA, Kernel PCA, LLA, t=SNE)<br>
>>> * Association rule learning(Apriori, Eclat)<br>
##### 이어해라



> ### 1.3.2 배치학습과 온라인 학습


>>

> ### 1.3.3 사례 기반 학습과 모델 기반 학습
>> 머신러닝 시스템은 어떻게 **일반화** 되는가를 기준<br>
>> 주어진 훈련 데이터로 학습하지만 훈련 데이터는 본적 없는 새로운 데이터로 일반화 되어야 한다는 뜻

>>> #### 사례 기반 학습
>>> 시스템이 사례를 기억함으로써 학습하는 것
>>> Ex1. 스팸 필터에서 메일 사이의 유사도를 측정해서 스팸을 분류하는 것 <br>
>>> #### 모델 기반 학습
>>> 샘플로부터 일반화 시키는 다른 방법은 이 샘플들의 모델을 만들어 예측에 사용하는 것
>>> 데이터를 분석-> 모델 선택 -> 훈련 데이터로 모델을 훈련 -> 새로운 데이터에 모델을 적용해 예측하고 일반화되길 기대


## 1.4. 머신러닝의 주요 도전 과제

> #### 충분하지 않은 양의 훈련 데이터
> - 간단한 문제도 수천 개의 데이터가 필요 

> #### 대표성이 없는 훈련 데이터
> - sampling bias를 조심해야 함

> #### 낮은 품질의 데이터
> - outlier 최소화

> #### 관련 없는 특성
> - garbage in, garbage out<br>
> - Feature Engineering이 중요
>> + Feature selection: 가지고 있는 특성중에 훈련에 가장 유용한 특성을 선택
>> + Feature Extraction: 특성을 결합하여 더 유용한 특성을 만듬

> #### 훈련 데이터 과대적합
> 훈련 데이터에 너무 잘 맞지만 일반성이 떨어지는 경우
> Ex1. 택시운전사가 내 물건을 훔쳤을 때, 모든 택시운전기사를 도둑이라고 생각하는 것
> 훈련 데이터에 있는 잡음의 양에 비해 모델이 너무 복잡할 때 일어남
>> 해결법1. 파라미ㅌ 수가 적은 모델을 선택하거나, 훈련 데이터에 있는 특성 수를 줄이거나 모델에 제약을 가해 단순화
>> 해결법2. 훈련 데이터를 더 많이 모은다
>> 해결법3. 훈련데이터의 bias를 줄인다.

> #### 훈련 데이터 과소적합
> 과대적합의 반대
> 모델이 너무 단순해서 데이터의 내재된 구조를 학습하지 못할 때 일어나는 현상

# Chapter2. 머신러닝 프로젝트 처음부터 끝까지

## 2.1. 실제 데이터로 작업하기
> 여기에서 사용하는 데이터는 캘리포니아 주택가격 데이터 셋을 사용

## 2.2. 큰 그림 보기
> ### 2.2.1. 문제 정의
>> 비즈니스의 목적이 정확히 무엇인가요?
>> 현재 솔루션은 어떻게 구성되어 있나요?
>> 지도학습/비지도학습/강화학습 중 무엇일까요?
>> 분류나 회귀인가요 아니면 다른 어떤 작업인가요?
>> 배치학습과 온라인학습 중 어떤 것을 사용해야 하나요?
>> * 현재 예시에서는 레이블된 training set이 있기에 지도 학습이며 값을 예측해야하므로 회귀문제입니다. 데이터에 연속적이 흐름이 없으므로 빠르게 변하는 데이터에 적응하지 않아도 되고, 데이터가 메모리에 들어갈 마ㄴ큼 충분히 작기 때문에 일반적인 배치 학습이 적절합니다.

> ### 2.2.2. 성능 측정 지표 선택
>> 회귀 문제의 전형적 성능지표: RMSE(평균 제곱근 오차)
>> 이상치로 보이는 구역이 많을 경우: MAE(평균 절대 오차)

> ### 2.2.3. 가정 검사
>> 지금까지 만든 가정을 검사!
>> 예를 들어, 가격이 입력으로 들어가게 되는데, 이를 카테고리화(저렴,보통,고가) 같은 거로 바꾸는게 더 좋을지 검사

## 2.3 데이터 가져오기
> ### 2.3.1. 작업환경 만들기
> ### 2.3.2. 데이터 다운로드
> ### 2.3.3. 데이터 구조 훑어보기
>> pandas 
>> * head(): 첫 다섯 행
>> * info(): 데이터에 대한 간략한 설명과 전체 행 수, 각 특성의 데이터 타입과 널이 아닌 값의 개수
>> * value_counts(): 타입이 텍스트 타입일 경우 사용. 카테고리의 종류, 카테고리의 양 확인
>> * describe(): 숫자형 특성의 요약 정보
>> hist(): 막대그래프

> ### 2.3.4. 테스트 세트 만들기
>> * sklearn.model_selection import train_test_split 사용하면 편해
>> * skleran.model_selection import StratifiedShuggleSplit : 계층 샘플링 (예) 남/여 비율 맞춰서 샘플링

## 2.4. 데이터 이해를 위한 탐색과 시각화
> ### 2.4.1. 지리적 데이터 시각화
>> * 기본 scatter plot

<pre><code>
housing.plot(kind="scatter", x="logitude", y="latitude", alpha=0.1)

</code></pre>

>> * 옵션 들어간 scatter plot
>> 1. s / 원의 반지름은 구역의 인구 수
>> 2. c / 색깔은 가격

<pre><code>
housing.plot(kind='scatter', x='longitude', y='latitude', alpha=0.4,
             s=housing['population']/100, label='population', figsize=(10,7),
             c='median_house_value', cmap=plt.get_cmap('jet), colorbar=True, shareex=False)

</code></pre>

> ### 2.4.2. 상관관계 조사
> 데이터 셋이 너무 크지 않으므로 모든 특성 간의 표준 상관계수(피어슨의 r) 를 corr()로 계산

<pre><code>
corr_matrix = housing.corr()
corr_matrix['median_house_value'].sort_values(ascending=False)

</code></pre>
> 특성 간의 관계를 확인하기 위해 산점도를 그려줄 수 있음

<pre><code>
from pandas.plotting import scatter_matrix

attributes = ["median_house_value", "median_income", "total_rooms", "housing_median_age"]
scatter_matrix(housing[attributes], figsize=(12,8))

</code></pre>

> ### 2.4.3. 특성 조합으로 실험

## 2.5. 머신러닝 알고리즘을 위한 데이터 준비
> ### 2.5.1. 데이터 정제
>> dropna(), drop(), fillna()
>> * scikit learn의 Imputer: 누락된 값 손쉽게 다루기

<pre><code>
from sklearn.preprocessing import Imputer

imputer = Imputer(strategy='median')
imputer.fit(housing_num)

imputer.statisctics_ #각 특성의 중간값을 계산해서 저장해놓은 것
X = imputer.transform(housing_num)

housing_tr = pd.DataFrame(X, columns=housing_num.columns, index=list(housing.index.values))
</code></pre>

> ### 2.5.2. 텍스트와 범주형 특성 다루기
>> * pandas.factorize() : 카테고리를 텍스트에서 숫자로 바꿔줌
<pre><code>
housing_cat_encoded, housing_categories = housing_cat.factorize()
housing_cat_encoded = [1, 0, 2, ... ]
housing_categories = ['<1H OCEAN', 'NEAR OCEAN', ... ]

</code></pre>

>> * OneHotEncoder: One-hot encoding
<pre><code>
from sklearn.preprocessing import OneHotEncoder

# 얘는 텍스트->숫자->원핫 벡터 과정을 사용
encoder = OneHotEncoder()
housing_cat_1hot = encoder.fit_transform(housing_cat_encoded.reshape(-1,1))
housing_cat_1hot.toarray()

# 변환 한번에 해버리기
import sklearn.preprocessing import CategoricalEncoder
cat_encoder = CategoricalEncoder() # 밀집 행렬을 원할 경우, CategoricalEncoder(encoding='onehot-dense')

housing_cat_reshaped = housing_cat.values.reshape(-1, 1)
housing_cat_1hot = cat_encoder.fit(transform(housing_cat_reshaped)

cat_encoder.categories_ = ['1H OCEAN', 'INLAND', 'NEAR BAY', ...]
</pre></code>

> ### 2.5.3. 나만의 변환기
!! 이건 하고 싶을 떄 다시봐랏

> ### 2.5.4 특성 스케일링
>> *min-max 스케일링*과 *표준화(standardization)* 가 대표적
>> 1. min-max 스케일링(normalization)<br>
>>> scikitlearn-> MinMaxScaler 변환기 제공 (0~1 사이가 싫다면, feature_range로 수정 가능)<br>
>> 2. 표준화(standardiation)<br>
>>> 평균을 빼고 표준편차로 나누어서 결과 분포의 분산이 1이 되도록 만듬<br>
>>> 범위의 상/하한이 없지만, 이상치에 영향을 덜받아 좋음<br>
>>> scikitlearn -> StandarScaler<br>

>>> *훈련 데이터에 대해서만 fit() / 테스트 데이터에 대해서는 transform()*

> ### 2.5.4. 변환 파이프라인
>> 모든 과정은 변환 단계가 많으며, 정확한 순서대로 실행되어야 함
>> scikit-learn 에는 Pipeline Class가 존재함

<pre><code>
from skleran.pipeline import Pipeline
frim sklearn.preprocessing import StandardScaler

num_pipline = Pipeline([
      ('imputer', Imuputer(startegy='median')),
      ('attribs_adder', CombinedAttrivutesAdder()),
      ('std_scaler', StandardScaler()),
])

housing_num_tr = num_pipeline.fit_transform(housing_num)
</pre></code>

>> * Pipeline은 연속된 단계를 나타내는 이름/추정기 쌍의 목록을 입력 받음
>> * 마지막 단계에는 변환기와 추정기를 모두 사용할 수 있고, 그 외에는 모두 변환기여야 함(즉, fit_trainsform()을 가지고 있어야 함)

<pre><code>
from sklearn.base import BaseEstimator, TransformerMixin

class DataFrameSelector(BaseEstimator, TransformerMixin):
  def __init__(self, attribute_names):
    self.attribute_names = attribute_names
    
  def fit(self, X, y=None):
    return self
    
  def transform(self, X):
    return X[self.attribute_names].values
    
</code></pre>
>>>!!! 더보고싶으면 봐라!!!


## 2.6. 모델 선택과 훈련

> ### 2.5.1. 훈련 세트에서 훈련하고 평가하기

>> * 선형 회귀모델 훈련 시키기
<pre><code>
from sklearn.linear_model import LinearRegression

# 훈련
lin_reg = LinearRegression()
lin_reg.fit(housing_prepared, housing_labels)

# test
test_prepro = full_pipeline.transform(test)
lin_reg.predict(test_prepro)

# mean_square_error
from sklearn.metrics import mean_squared_error

housing_prediction = lin_reg.predict(test_prepro)
lin_mse = mean_squared_error(housing_labels, housing_predictions)
lin_rmse = np.sqrt(lin_mse)
</code></pre>

>> * Decision Tree Regression 훈련 시키기

<pre><code>
from skleanr.tree import DecisionTreeRegressor

# 훈련
tree_reg = DecisionTreeRegressor()
tree_reg.fit(housing_prepared, housing_labels)

# test
housing_predictions = tree_reg.predict(housing_prepared)
tree_mse = mean_squared_error(housing_labels, housing_predictions)
tree_rmse = np.sqrt(tree_mse)

</code></pre>

> ### 2.6.2. 교차 검증을 사용한 평가
>> 역시나 sckit-learn 에는 교차검증 기능이 있다!<br>
>> K-fold-cross-validation: 훈련 세트를 fold라 불리는 10개의 subset으로 무작위 분할하고, 10번 훈련/평가 한다! <br>

<pre><code>
from sklearn.model_selection import cross_val_score

scores = cross_val_score(tree_reg, housing_prepared, housing_labels,
                         scoring='neg_mean_squared_error', cv=10)
tree_rmse_scores = np.sqrt(-scores)
</code></pre>

>> * Random Forest 훈련 시키기

<pre><code>
form skleanr.ensemble import RandomForestRegressor

forest_reg = RandomForestRegressor()
forest_reg.fit(housing_prepared, housing_labels)
[....]

</code></pre>


>> 실험한 모델들을 모두 저장해두는 것이 좋은데, 역시 sckit-learn은 또 제공합니다!
<pre><code>
from sklearn.externals import joblib

# save
joblib.dump(my_model, 'my_model.pkl')
# load
my_model_loaded = joblib.load('my_model.pkl')
</code></pre>

## 2.7. 모델 세부 튜닝
> ### 2.7.1. 그리드 탐색
>> 가장 쉬운거는 그냥 다 수동으로 조정하는 것이지요<br>
>> 근데 또 scikit-learn은 가지고 있다! GridSearchCV!!!!!

<pre><code>
from sklearn.model_selection import GridSearchCV

param_grid = [
  {'n_estimators': [3, 10, 30], 'max_features': [2, 4, 6, 8]},
  {'bootstrap': [False], 'n_estimators': [3, 10], 'max_features': [2, 3, 4]},
]

forest_reg = RandomForestRegressor()

grid_search = GridSearchCV(forest_reg, param_grid, cv=5,
                           scoring='neg_mea_squared_error',
                           retrun_train_score=True)
                           
grid_search.fit(housing_prepared, housing_labels)

# best estimator
grid_search.best_estimator_

# score
cvres = grid_search.cv_results_
for mean_score, params in zip(cvres['mean_test_score'[, cvre['params']):
    print(mp.sqrt(-mean_score), params)

</code></pre>

> ### 2.7.2. 랜덤 탐색
>> 그리드 탐색은 비교적 적은수 조합일 때 좋고, 그 이상일 때는 랜덤 탐색!
>> 또 scikit-learn에 있대! RandomizeSerachCV


> ### 2.7.3. 앙상블 방법
>> 하나의 모델말고 여러 모델을 붙여서 사용해봅시다. 더 성능이 좋을 수도 있어요

> ### 2.7.4. 최상의 모델과 오차 분석
>> RandomForestRegressor는 각 특성의 상대적인 중요도를 알려준다.<br>
>> feature_importances = grid_search.best_estimator_.feature_importances<br>

> ### 2.7.5. 테스트 세트로 시스템 평가하기

## 2.8. 론칭, 모니터링, 그리고 시스템 유지 보수

# Chapter3. 분류

## 3.1. MNIST
> scikit-learn 에서 MNIST 받을 수 있다!
<pre><code>
from sklearn.datasets import fetch_mldata

mnist = fetch_mldata('MNIST original')
</code></pre>

## 3.2. 이진 분류기 훈련
> 문제를 단순화 해서 '5-감지기'를 만들어 봅시다.

<pre><code>

# prepare dataset 
y_train_5 = (y_train==5)
y_test_5 = (y_test ==5)

# training with SGD
from sklearn.linear_model import SGDClassifier

sgd_clf = SGDClassifier(max_iter=5, random_state=42)
sgd_clf.fit(X_train. y_train_5)

# predict 
sgd_clf.predict([some_digit])

</code></pre>

## 3.3. 성능 측정 
> ### 3.3.1. 교차 검증을 사용한 정확도 측정<br>
>> * 교차 검증 직접 구현하기!<br>
<pre><code>
from sklearn.model_selection import StartifiedKFold
from sklearn.base import clone

# StratifiedFold는 클래스별 비율이 유지되도록 폴드를 만들기 위해 계층적 샘플링을 수행
skfolds = StratifiedKFold(n_splots=3, randome_state=42)

from train_index, test_index in skfolds.split(X_train, y_train):
    clone_clf = clone(sgd_clf)
    X_train_folds = X_train[train_index]
    Y_train_folds = y_train[train_index]
    X_test_fold = X_train[test_index]
    Y_test_fold = Y_train[test_index]
    
   clone_clf.fit(X_train_folds, y_train_folds)
   y_pred = clone_clf.predict(X_test_fold)
   n_correct = sum(y_pred == y_test_fold)
   print(n_correct / len(y_pred))
</code></pre>

>> * scikit-learn 으로 교차검증 하기!

<code><pre>
from sklearn.model_selection import cross_val_score
cross_val_score(sgd_clf, X_train, y_train, cv=3, scoring='accuracy')
</code></pre>

>> * 더미 분류기 만들기! 

> ### 3.3.2. 오차 행렬
>> cross_val_predict 을 이용하면 구할 수 있다
<code><pre>
from skleanr.model_selection import cross_val_predict
from sklearn.model_selection import confusion_matrix

y_train_pred = cross_val_predict{(sgd_clf, X_train, y_train_5, cv=3)
confusion_matrix(y_train_5, y_train_pred)

</code></pre>

>> 오차행렬


> ### 3.3.5. ROC 곡선
>> ROC(Receiver Operating Characteristic) 
>> ROC 곡선은 거짓양성비율(FPR)에 대한 진짜 양성 비율(TPR)의 곡선<br>
>> FPR = 1-TNR (TNR은 진짜 음성 비율/특이도(specificity))<br>
>> 즉, ROC 곡선은 재현율에 대한 1-특이도 그래프<br>
>> * 그니까, ROC 곡선은 양성이라고 예측한 것들을 가지고, 거짓 양성 비율과 진짜 양성 비율을 그린 것!<br>

<code><pre>
from sklearn.metrics import roc_curve

FPR, TPR, thresholds = roc_curve(y_train_5, y_scores)
</pre></code>

>> AUC는 ROC curve로 생기는 아래 면적의 크기!! 얘가 크면(<1) 분류기가 잘된거지~ 완전 랜덤 분류기는 0.5<br>
>> * ROC curve vs PR curve : 양성 클래스가 드물거나 거짓음성보다 거짓 양성이 중요할 때 PR곡선! 아닐 때는 다 ROC<br>

## 3.4. 다중 분류
> 다중 분류는 둘 이상의 클래스를 구별하는 것<br>
> 이진 분류기(서포트 벡터 머신, 선형)를 여러개 사용하거나 다중 분류기(랜덤 포레스트, 나이브 베이즈) 사용<br>

## 3.5. 에러 분석
> 오차 행렬을 확인하기

<pre><code>
y_train_pred = cross_val_predict(sgd_clf, X_train_scaled, y_train, cv=3)
conf_mx = confusion_matrix(y_train, y_train_pred)

 # mat plot으로 그려보기
plt.matshow(conf_mx, cmap=plt.cm.gray)

 # 에러 비율 plot 그리기
row_sums = conf_mx.sum(axis=1, keepdims=True)
norm_conf_mx = conf_mx/row_sums

plt_matshow(norm_conf_mx, cmap=plt.cm.gray)
 
</code></pre>


## 3.6. 다중 레이블 분류
> 하나의 데이터가 여러개의 label을 가질 경우<br>
> 여기서 사용한 방법은 KNN 알고리즘<br>
> 여기서는 이진 분류를 여러개로 해야하는 것이니까, 1번째 분류법: 숫자가 큰지 2번째 분류법: 홀수인지 <br>


<pre><code>
from sklearn.neighbors import KNeighborsClassifier

y_train_large = (y_train>=7)
y_train_odd = (y_train%2 ==1)
y_multilabel = np.c_[y_train_larget, y_train_odd]

knn_clf = KNeighborsClassifier()
knn_clf.fit(X_train, y_multilabel)

knn_clf.predict(test)

y_train_knn_pred = cross_val_predict(knn_clf, X_train, y_multilabel, cv=3, n_jopbs=-1)
f1_score(y_multilabel, y_train_knn_pred, average='macro')

</code></pre>


> 만약 label 별로 가진 데이터 갯수가 다를 경우, label class의 support의 가중치를 줄수 있다! <br>
>> f1_score(y_multilabel, y_train_knn_pred, averag='wieghted')


## 3.7. 다중 출력 분류




    








 






                         







