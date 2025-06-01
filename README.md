# Практическая работа 1 
## Выполнил Ибрагимов Р.А. ИВТ 2.2

### Описание проекта

Цель проекта — предсказать, откликнется ли клиент банка на предложение оформить срочный депозит, используя данные кампаний прямого маркетинга.

Была построена и сравнена серия моделей машинного обучения, лучшая из которых была сохранена и развёрнута через Flask API. Для взаимодействия с пользователем разработан простой HTML-интерфейс.

---

### Используемые данные

[База данных](https://github.com/karaylkin/ML/blob/main/bank-additional-full.csv)

Использован файл: `bank-additional-full.csv` — содержит 41188 строк и 21 признак + целевая переменная `y`.

---

### Анализ данных (EDA)

* Выполнен первичный анализ данных через `.info()`, `.describe()`.
* Построены гистограммы для категориальных признаков.
* Проанализировано распределение целевой переменной `y` (балансировка классов).

[Код проекта](https://github.com/karaylkin/ML/blob/main/Project1.ipynb)

---

### Предобработка

- Целевая переменная бинаризована: `yes → 1`, `no → 0`
- Числовые признаки: заполнение пропущенных значений + стандартизация
- Категориальные признаки: заполнение наиболее частым + OneHotEncoding
- Использован `ColumnTransformer` и `Pipeline` для объединения шагов

---

### Обучение моделей

Обучены три модели:

- Logistic Regression
- Random Forest Classifier
- Gradient Boosting Classifier

Каждая модель встроена в pipeline с предобработкой.

---

### Сравнение моделей

- Каждая модель оценивалась по:
+ classification report (precision, recall, f1-score)
+ ROC AUC
+ ROC-кривая
- Победитель: модель с наибольшим ROC AUC

![Pasted image 20250602010657](https://github.com/user-attachments/assets/1bcff897-15c2-4663-aee0-f20a737f271e)

![Pasted image 20250602010751](https://github.com/user-attachments/assets/98fe2694-732a-4857-a259-9e14a5814b8d)

---

### Развёртывание модели (API)

- Использован фреймворк **Flask**
- Реализовано два маршрута:
+ `GET /` — HTML интерфейс
+ `POST /predict` — JSON-запрос с признаками, возвращает `{'prediction': 0/1}`
- Загружается сохранённая модель `*.pkl`
![Pasted image 20250602010848](https://github.com/user-attachments/assets/2dd2e0e3-a800-429e-866a-c81ad5dbcf4d)

![Pasted image 20250602010937](https://github.com/user-attachments/assets/2806e3af-5b9a-4847-9553-aaa6c4b190a7)

---

### Фронтенд-приложение

- HTML форма с выпадающими списками и полями ввода
- Результат отображается без перезагрузки (JavaScript + fetch API)

![Pasted image 20250602011106](https://github.com/user-attachments/assets/b484c0a4-4c4e-4703-9e65-342c5679a01e)

![Pasted image 20250602011217](https://github.com/user-attachments/assets/cf780f0c-a018-4f6d-98ac-67126fe5ebfd)

---

### Выводы

- Logistic Regression показала хорошее поведение как базовая модель
- Random Forest и Gradient Boosting дали прирост точности
- Финальная модель развёрнута в виде API и доступна через HTML-интерфейс

Проект завершён в соответствии с требованиями: анализ, модели, API, frontend, отчёт.
