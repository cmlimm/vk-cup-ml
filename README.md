# [vk-cup-ml](https://cups.online/ru/tasks/1417)
## Условие
Сообщества ВКонтакте могут принадлежать одной из нескольких заранее заданных категорий. Но даже среди спортивных сообществ есть достаточно сильное разделение по тематикам! Одни и те же авторы могут писать только об одном виде спорта или сразу о большом количестве.
По заданному набору постов определите тематику — какой именно вид спорта обсуждается в выбранном сообществе?

## Скоринг
Обратите внимание, что в этой задаче вас ждёт нестандартная метрика:
- За каждый правильный ответ вы получите +1.
- За каждый неправильный ответ вы получите −1.

Таким образом, вы можете отправлять решения, в которых категория отмечена не для каждого сообщества.

## Решение
Шаги для решения:
1. Лемматизация токенов
2. Удаление стоп-слов (предлоги, союзы, часто встречающиеся слова, не влияющие на смысл поста)
3. Создание матрицы фичей TF-IDF с n-граммами длиной до 3-ёх
4. Кросс-валидация для поиска оптимального параметра регуляризации для метода опорных векторов.
Для каждой тематики отдельная модель, предсказывающая, принадлежит пост данной тематике или нет.
5. У каждого поста есть ID сообщества к которому он принадлежит, поэтому для каждого сообщества суммируется
количество постов по каждой тематике, каждое значение делится на общее количество постов, после чего было
использовано два подхода:
	- тематика выбирается та, у которой значение больше 0.6
	- тематика определяется по максимальному получившемуся значению

По итогу первый подход получил скор `0.953` на публичном датасете, второй получил `0.965`, на приватном датасете
оба получили одинаковый скор `0.957`.

Итоговое место: 153/473.
