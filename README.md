# Progect
# Рекомендация тарифов
# В вашем распоряжении данные о поведении клиентов, которые уже перешли на эти тарифы (из проекта курса «Статистический анализ данных»).
# Нужно построить модель для задачи классификации, которая выберет подходящий тариф. Предобработка данных не понадобится — вы её уже сделали.
# Постройте модель с максимально большим значением *accuracy*. Чтобы сдать проект успешно, нужно довести долю правильных ответов по крайней мере до 0.75.
# Проверьте *accuracy* на тестовой выборке самостоятельно.
## Откройте и изучите файл
import pandas as pd
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.dummy import DummyClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.metrics import accuracy_score
import seaborn as sns
from scipy import stats as st
import matplotlib.pyplot as plt
import numpy as np
from joblib import dump
from sklearn.metrics import f1_score
data=pd.read_csv('/datasets/users_behavior.csv')
# вывожу первые 5 строчек датафрейма data на экран
data.head()
# вывожу основную информацию о датафрейме с помощью метода info()
data.info()
# построем общую гистограмму для всех числовых столбцов датафрейма
data.hist(figsize=(15, 20))
plt.show()
# посмотрим информацию по нечисленным типам данных(узнать есть ли отрицательные числа)
data.describe(include='all')
# посмотрим на таблицу в разнобой
data.sample()
# посмотрим на последние строчки датафрейма
data.tail()
# Изучив данные видно, что выбросов нет, пропусков тоже,что иследовательский анализ сделан, следовательно
# можно приступить к прогнозу, точнее попробовать его сделать.
data.corr(method='spearman')
# найдем медиану, она как раз посередине
data['is_ultra'].median()
# получается мы уже разделили наш датафрейм на нули и едининицы, точнее он уже сам разделен
# так как is_ultra — каким тарифом пользовался в течение месяца («Ультра» — 1, «Смарт» — 0)
#будем отталкиваться от этого
# извлеките признаки
features = data.drop(['is_ultra'], axis=1)
# извлеките целевой признак(тот, который нужно предсказать)
target = data['is_ultra']
# < разделите данные на обучающую и валидационную выборки >
data_train, data_valid = train_test_split(data, test_size=0.20, random_state=1)
# features_train,target_train,train,valid, data_valid=train_test_split(features_train,target_train, test_size=0.25,random_state=1)
data_train,data_test=train_test_split(data_train, test_size=0.25,random_state=1)  
features_train = data_train.drop(['is_ultra'], axis=1) 
target_train = data_train['is_ultra']
features_valid = data_valid.drop(['is_ultra'], axis=1) 
target_valid = data_valid['is_ultra']
features_test = data_test.drop(['is_ultra'], axis=1) 
target_test = data_test['is_ultra']
## Исследуйте модели
# Чтобы выбрать лучшую модель из модели лесу, будем менять кол-во деревьев
# Обучим модели случайного леса с числом деревьев от 1 до 5.

best_model = None
best_result = 0
for est in range(1, 6):
    model = RandomForestClassifier(random_state=1, n_estimators=est) # обучим модель с заданным количеством деревьев
    model.fit(features_train,target_train) # обучим модель на тренировочной выборке
    result = model.score(features_valid, target_valid) # посчитаем качество модели на валидационной выборке
    if result > best_result:
        best_model =model # сохраним наилучшую модель
        best_result = result#  сохраним наилучшее значение метрики accuracy на валидационных данных

print("Accuracy наилучшей модели на валидационной выборке:", best_result)
# Обучим модели случайного леса с числом деревьев от 1 до 10.

best_model = None
best_result = 0
for est in range(1, 11):
    model = RandomForestClassifier(random_state=1, n_estimators=est) # обучим модель с заданным количеством деревьев
    model.fit(features_train,target_train) # обучим модель на тренировочной выборке
    result = model.score(features_valid, target_valid) # посчитаем качество модели на валидационной выборке
    if result > best_result:
        best_model =model # сохраним наилучшую модель
        best_result = result#  сохраним наилучшее значение метрики accuracy на валидационных данных

print("Accuracy наилучшей модели на валидационной выборке:", best_result)
# Обучим модели случайного леса с числом деревьев от 1 до 15.

best_model = None
best_result = 0
for est in range(1, 16):
    model = RandomForestClassifier(random_state=1, n_estimators=est) # обучим модель с заданным количеством деревьев
    model.fit(features_train,target_train) # обучим модель на тренировочной выборке
    result = model.score(features_valid, target_valid) # посчитаем качество модели на валидационной выборке
    if result > best_result:
        best_model =model # сохраним наилучшую модель
        best_result = result#  сохраним наилучшее значение метрики accuracy на валидационных данных

print("Accuracy наилучшей модели на валидационной выборке:", best_result)
 # Чтобы подобрать модель решающие дерево - будем менять параметр глубину.
 # Дерево решений

depth=1
model = DecisionTreeClassifier(random_state=1, max_depth=depth)# < создадим модель, указав max_depth=depth >
model.fit(features_train, target_train)# < обучим модель >

predictions_valid =model.predict(features_valid) # < найдем предсказания на валидационной выборке >

  
print(accuracy_score(target_valid, predictions_valid)) 
# < сделаем цикл для max_depth от 1 до 5 >
for c in range(1, 6):
    model = DecisionTreeClassifier(random_state=1, max_depth=c)
    model.fit(features_train, target_train)

    predictions_valid =model.predict(features_valid) 

    print("max_depth =", depth, ": ", end='')
    print(accuracy_score(target_valid, predictions_valid)) 
# Чтобы наша модель дерево, давало более точные прогнозы надо брать параметр max_depth=5.
model= LogisticRegression(random_state=1, solver='lbfgs', max_iter=900000)
model.fit(features_train, target_train)
model.score(features_valid,target_valid) 
iter=1
model = LogisticRegression(random_state=1, max_iter=iter)# < создадим модель, указав max_depth=depth >
model.fit(features_train, target_train)# < обучим модель >

predictions_valid =model.predict(features_valid) # < найдем предсказания на валидационной выборке >

  
print(accuracy_score(target_valid, predictions_valid)) 
for c in range(9999, 100000):
    model = LogisticRegression(random_state=1, solver='lbfgs',max_iter=c) 
    model.fit(features_train, target_train)# < обучим модель >

    predictions_valid =model.predict(features_valid) # < найдем предсказания на валидационной выборке >
    
    print("iter =", c, ": ", end='')
    print(accuracy_score(target_valid, predictions_valid))  
# Делаем общий вывод, что самая лучшая модель это случайный лес в котором от1 до 15 деревьев.
# Изучив данные модели, можно отметить, чтобы наша модель дерево, давало более точные прогнозы надо брать
# параметр max_depth=5.Можно еще отметить чем ближе к единице тем правельнее будет наш прогноз, приблизиться
# к единице нам позволело дерево решений, поэтому в нашем проэкте следует использовать его.
## Проверьте модель на тестовой выборке
# Чтобы знать точно, что модель не вызубрила ответы, возьмём новый датасет — тестовый набор данных, или тестовую выборку.
# Файл с данными назовём test_data.csv. Проверим, как модель с ними справится.
# Отличается ли accuracy на обучающей и тестовой выборках? Посчитайте значения и напечатайте на экране

# Берем самую лучшую модель дерево решений

depth=1
model = DecisionTreeClassifier(random_state=1, max_depth=4)# < создадим модель, указав max_depth=depth >
model.fit(features_train, target_train)# < обучим модель >

predictions_valid =model.predict(features_valid) # < найдем предсказания на валидационной выборке >


# < напишем здесь код расчёта на обучающей выборке >
train_predictions = model.predict(features_train)
train=accuracy_score(target_train, train_predictions)

test_predictions = model.predict(features_test)
test = accuracy_score(target_test, test_predictions)
print("Accuracy")
print("Обучающая выборка:",train)
print("Тестовая выборка:",test) 

best_model = None
best_result = 0
for est in range(1, 16):
    model = RandomForestClassifier(random_state=1, n_estimators=est) # обучим модель с заданным количеством деревьев
    model.fit(features_train,target_train) # обучим модель на тренировочной выборке
    result = model.score(features_valid, target_valid) # посчитаем качество модели на валидационной выборке
    if result > best_result:
        best_model =model # сохраним наилучшую модель
        best_result = result#  сохраним наилучшее значение метрики accuracy на валидационных данных

test_predictions = model.predict(features_test)
test = accuracy_score(target_test, test_predictions)
print("Accuracy")
print("Обучающая выборка:",train)
print("Тестовая выборка:",test)
# По данному иследованию я могу посоветовать тариф "Смарт".
