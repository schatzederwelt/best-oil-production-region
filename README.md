# Предсказание прибыльного региона нефтедобычи

**ПРОБЛЕМА:**

В добывающей компании необходимо принять решение, в каком **из 3-х регионов** бурить новую скважину.

В каждом регионе `10 000 месторождений`, где измерили **качество** нефти в каждой скважине и **объём** её запасов. 

**ЦЕЛЬ ПРОЕКТА:**

Построить модель машинного обучения, которая поможет определить `лучший регион`:

- c **наибольшей прибылью** от добычи нефти
- c учетом оценки `возможных рисков`

В нашем распоряжении `3 датасета` с пробами нефти в каждом из регионов.

---

**ЛИЧНЫЕ ЦЕЛИ:**

- Научиться `интерпретировать качество` моделей с помощью метрики **RMSE**
- На практике связать модели ML с **бизнес-задачами**  
- Применить знания по технике `Bootstrap` для оценки **прибыли** и **рисков**

[Посмотреть проект](Predict_best_oil_production_region_v1.ipynb)

## Новые навыки

<div class="alert alert-success">
<br> ✔️ Регрессия  ✔️ Интерпретация ошибок RMSE </br>
<br> ✔️ Графики корреляций для оценки предсказаний </br>
<br> ✔️ Bootstrapping ✔️ ML для оценки прибыли и рисков </br>
<br> ✔️ Доверительные интервалы </br>
</div>

## Этапы исследования

1. Провели сравнительный анализ объемов `запасов нефти` и других характеристик скважин для **разных регионов**

2. Построили для каждого региона модель **Линейной Регрессии** для предсказания `объемов нефти`

  - сделали оценку `среднего запаса` сырья, который модель **предсказывает** в каждом регионе
  - использовали визуализацию **корреляций** для интерпретации метрик `RMSE`
  
3. Расчета прибыли для каждого региона
4. Bootstraping

7. Оценили вероятность **прибыли** и **рисков** в каждом регионе.

## Результат проекта

Определили для Заказчика наиболее прибыльный **регион для разработки скважин**.

1. Исключили регионы №1 и №3, в которых вероятность `убытков меньше 2.5%`:

    - доля случаев с отрицательной прибылью `3.7%` и `8%`
    - для оценки использовали **bootstrapping** и доверительный интервал

3. Выбрали `регион №2` с наибольшей **средней прибылью**:
    - риск убытков: `0.2%`
    - вероятная средняя выручка: `580 255 тыс.руб`

В выбранном регионе наша линейная модель **предсказывает запасы сырья** в скважинах с низким уровнем ошибок `RMSE = 0.89`

Средний запас **предсказанного сырья** в регионах: `69.750 тыс. баррелей` (реальные запасы 69.751 тыс. баррелей)

Бизнес-цель успешно достигнута.

## Исходные данные

Для каждого региона отдельный набор данных c **характеристиками** `100 000 скважин`:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right">
      <th></th>
      <th>id</th>
      <th>f0</th>
      <th>f1</th>
      <th>f2</th>
      <th>product</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>txEyH</td>
      <td>0.705745</td>
      <td>-0.497823</td>
      <td>1.221170</td>
      <td>105.280062</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2acmU</td>
      <td>1.334711</td>
      <td>-0.340164</td>
      <td>4.365080</td>
      <td>73.037750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>409Wp</td>
      <td>1.022732</td>
      <td>0.151990</td>
      <td>1.419926</td>
      <td>85.265647</td>
    </tr>
    <tr>
      <th>3</th>
      <td>iJLyR</td>
      <td>-0.032172</td>
      <td>0.139033</td>
      <td>2.978566</td>
      <td>168.620776</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Xdl7t</td>
      <td>1.988431</td>
      <td>0.155413</td>
      <td>4.751769</td>
      <td>154.036647</td>
    </tr>
    <tr>
      <th>5</th>
      <td>wX4Hy</td>
      <td>0.969570</td>
      <td>0.489775</td>
      <td>-0.735383</td>
      <td>64.741541</td>
    </tr>
    <tr>
      <th>6</th>
      <td>tL6pL</td>
      <td>0.645075</td>
      <td>0.530656</td>
      <td>1.780266</td>
      <td>49.055285</td>
    </tr>
  </tbody>
</table>

- `id` — уникальный **идентификатор** скважины
- `f0, f1, f2` — три признака точек (их значение не разглашают, но специалисты уверяют -  сами признаки значимы)
- `product` — **объём запасов** в скважине. (!) `тысяч баррелей`
