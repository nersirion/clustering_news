# Clustering news
Класификация новостей и построение тематической модели. Опробованы способы:
1. Tfidf + SVD + KMeans
2. CountVectorizer + LDA
3. Word2Vec (обученый на данных и предобученый), FastTexz(обученые на данных)
В качетсве датасета использовалось 25000 новостей из датасета lenta-news
https://www.kaggle.com/yutkin/corpus-of-russian-news-articles-from-lenta/
Предобученный Word2Vec от https://rusvectores.org/
## Содержание проекта
- ### src
#### utils.py
основные функции используемые в проекте
#### preprocessing_text.py
Скрипт запускающий обработку текста и распаралеривающий лемматизацию.
#### pipeline.py
Скрипт запускающий предсказания моделей. Принцип:
1. Новости для предсказания загружаются из папки dataset. Название файла должно быть to_lda_analyze.csv
2. Проверяется, что количество новостей меньше порогового. По умолчанию стоит 100.
3. Текст проходит чистку и лемматизацию
4. Загружаются 9 моделей (4 связки CountVectorizer + LDA и один Knn)
5. Делаются предсказания всеми моделями.
6. Итоговое предсказание выдает knn из полученных четырех от LDA.
#### app.py
Простое приложение на dash. 
Запускает скрипт из pipeline.py.
Получает предсказания
Cтроит Bar plot
Выводит график и таблицу с 10 ключевыми словами каждого кластера.
- ## /
#### Clustering_news_Tfidf+SVD+KMeans.ipynb
#### Clussering_w2v_and_fasttext.ipynb
#### Clustering_news_LDA.ipynb
Нотебуки с EDA по каждому методу. Лучший результат показал LDA, поэтому только этим методом и обучались модели. Модели различались количество n_gram в мешке слов: (1, 1), (1, 2), (1, 3), (2, 3)
