DBSCAN Clustering Project
Описание проекта
Проект по кластеризации данных с использованием алгоритма DBSCAN (Density-Based Spatial Clustering of Applications with Noise). Реализована полная pipeline обработки данных: от нормализации до визуализации результатов кластеризации.
​

Технологии
Python 3.x
pandas - работа с данными
scikit-learn - машинное обучение (DBSCAN, StandardScaler, MinMaxScaler)
seaborn - визуализация
matplotlib - построение графиков
numpy - численные вычисления

Основные этапы анализа
1. Предобработка данных
scaler = StandardScaler()
scalerX = scaler.fit_transform(df)
Применяется StandardScaler для стандартизации признаков.​

2. Нормализация с MinMaxScaler
scaler = MinMaxScaler()
data = scaler.fit_transform(cat_means)
scaled_means = pd.DataFrame(data, cat_means.index, cat_means.columns)
Масштабирование данных в диапазон для корректной работы алгоритма.​

3. Подбор параметра epsilon
Реализован цикл для определения оптимального значения eps:
for eps in np.linspace(0.001, 3, 50):
    dbscan = DBSCAN(eps=eps, min_samples=2*scalerX.shape[1])
    dbscan.fit(scalerX)
    perc_outliers = 100 * np.sum(dbscan.labels_ == -1) / len(dbscan.labels_)
Анализируется процент выбросов для разных значений eps.
​

4. Визуализация
Pairplot - попарные зависимости признаков с группировкой по регионам
Heatmap - тепловые карты нормализованных данных:
sns.heatmap(scaled_means.loc[[0,1]], annot=True)

Особенности реализации
min_samples установлен как 2 * количество_признаков для адаптивного определения минимального размера кластера​
Диапазон поиска eps: [0.001, 3] с 50 точками для детального анализа
Использование двух типов нормализации (StandardScaler и MinMaxScaler) для разных целей

Результаты
Notebook содержит анализ влияния параметра eps на процент выбросов, что позволяет выбрать оптимальное значение для качественной кластеризации данных на основе плотности.
