### Алгоритм метода k-means

1. Заранее определяется k - число кластеров.
2. Выбирается k точек — центры кластеров. (Процедуру для определения числа кластеров обсудим позднее.)
3. (Итеративно) Объект приписывается к тому кластеру, чей центр ближайший.
4. (Итеративно) Центр кластера переносим в центр тяжести кластера.

Для определения схожести используется только евклидово расстояние. Недостаток исправляется в других вариантах метода к-средних: k-медоиды

**Результат кластеризации зависит от расположения начальных центров кластеров!**

![Объекты](/images/lect_3/bad_choice_middles.png)

#### Начальное расположение кластеров

1. **Forgy.** Случайным образом выбираются k наблюдений. Они и будут начальными центрами кластеров.
2. **Случайное разбиение (Random Partition).** Каждое наблюдение случайным образом приписывается к одному из кластеров. Находятся центры тяжести кластеров. Они и будут начальными центрами.
3. **K-means++** 
	+ Фанатики метода считают подход самостоятельным способом кластеризации
	+ Отличается от K-means только процедурой cоздания начального расположения центров
	+ Популярен среди пользователей Питона
	
#### Алгоритм K-means++

1. Случайное наблюдение равновозможно выберите в качестве первого центроида.
2. Вычислите расстояние от каждого наблюдения до ближайшего из ранее выбранных центроидов.
3. Выберите очередной центроид среди наблюдений случайным образом. Вероятность выбора наблюдения прямо пропорциональна ее расстоянию до ближайшего из уже выбранных центроидов. В результате максимальные шансы быть выбранной очередным центроидом у той точки, чье расстояние до ближайшего центроида максимально.
4. Повторите шаги 2 и 3, пока не будут выбраны k центроидов.

#### Определение числа кластеров

Задаем разное число кластеров

k = 2, 3, …, 100

k = 2, 4, 8, …, 512
 
Строим график каменистая осыпь. Выбираем лучшую кластеризацию. Там, где есть измлом.

Объем вычислений возрастает в 100 раз...

#### Математическая модель

$$W_S = \sum_{i=1}^k\sum_{x \in S_i}\parallel x - \overline{x_i} \parallel^2$$

$$S_{optim} = argmin \sum_{i=1}^k\sum_{x \in S_i}\parallel x - \overline{x_i} \parallel^2$$

Мы определяем 100 раз число кластеров и для каждого 300 раз центры кластеров, чтоб не зависеть от центра кластеров. Итого, 30 000 раз.

#### Недостатки

1. Только евклидово расстояние.
2. Решение зависит от начальных центров.
3. Надо определять число кластеров
4. Слишком много вычислений расстояний.
5. На поздних итерациях мало точек меняют кластер, вычисления для "определившихся" точек можно исключить. Только как?

#### Родственники k-means

+ Х-means
+ C-means (Нечеткий алгоритм кластеризации)
+ Форель (FOREL) Новосибирск, Загоруйко
+ Mini Batch K-Means (Питон)