## Создание модели с помощью машинного обучения , которая будет отправлять токсичные комментарии на модерацию


## Описание проекта
Интернет-магазин «Викишопs» запускает новый сервис. Теперь пользователи могут редактировать и дополнять описания товаров, как в вики-сообществах. То есть клиенты предлагают свои правки и комментируют изменения других. Магазину нужен инструмент, который будет искать токсичные комментарии и отправлять их на модерацию.

## Навыки и инструменты
python  
pandas  
numpy  
scipy  
sklearn.model_selection.cross_val_score  
sklearn.metrics.mean_squared_error  
sklearn.metrics.mean_absolute_error  
sklearn.preprocessing.StandardScaler  
sklearn.linear_model.LogisticRegression    
sklearn.tree.RandomForestClassifier    
sklearn.CatBoost     
matplotlib  
## Общий вывод
В качестве моделей использованы LogisticRegression, RandomForestClassifier и CatBoost. Самой лучший результат показала модель LogisticRegression.
