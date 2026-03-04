# Обнаружение ботнетов с использованием машинного обучения

**Автор:** Timurmalik Djuraev (8562763) 
**Тема:** Кибербезопасность / Машинное обучение (супервизия, бинарная классификация)

## Описание проекта
Проект реализует **ML‑конвейер** для обнаружения **ботнет‑трафика** по **сетевым flow‑признакам**. Каждый сетевой поток описывается статистическими признаками (длительность, пакеты/байты, скорости и т.д.) и классифицируется как:

- **0 — нормальный трафик**
- **1 — ботнет / аномальный трафик** fileciteturn5file0

## Датасет
- CSV‑датасет на основе **CTU‑13**, где каждая строка — **двунаправленный сетевой flow** (признаки уровня CICFlowMeter). fileciteturn5file0  
- После объединения и минимальной очистки итоговый набор данных содержит **18,443 flow**, с бинарной меткой. fileciteturn5file0

## Подход (конвейер)
1. **Предобработка**
   - Удаление идентификаторов (IP, порты, временные метки, flow ID), чтобы снизить переобучение на конкретную среду. fileciteturn5file0  
   - One‑hot encoding категориальных признаков (если есть). fileciteturn5file0  
   - Разделение train/test: `test_size=0.2`, `stratify=y`, `random_state=42`. fileciteturn5file0  
   - Стандартизация `StandardScaler` с обучением scaler только на train (без leakage). fileciteturn5file0

2. **Модель**
   - **RandomForestClassifier** (100 деревьев, `random_state=42`, `n_jobs=-1`, глубина без жёсткого ограничения). fileciteturn5file0

3. **Оценка**
   - Accuracy, Precision, Recall, F1, Confusion Matrix. fileciteturn5file0  
   - Визуализация **UMAP** (2D): `n_neighbors=15`, `min_dist=0.1`, `random_state=42`. fileciteturn5file0

## Результаты (из отчёта)
Confusion matrix (test): fileciteturn5file0  
- TN: 10,646  
- FP: 17  
- FN: 12  
- TP: 7,768  

Метрики (примерно): fileciteturn5file0  
- Accuracy: ~99.84%  
- Precision (botnet): ~99.78%  
- Recall (botnet): ~99.85%  
- F1 (botnet): ~99.81%

## Файлы
- `botnet_detection.ipynb` — весь пайплайн (предобработка → обучение → оценка → графики). fileciteturn5file0  
- `CTU13_Attack_Traffic.csv` — ботнет/вредоносные flow. fileciteturn5file0  
- `CTU13_Normal_Traffic.csv` — нормальные flow. fileciteturn5file0  
- `docs/Botnet Detection using Machine Learning.docx` — отчёт.

## Зависимости
Python 3.x. Пакеты: fileciteturn5file0  
- `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `umap-learn`

Установка (пример):
```bash
pip install pandas numpy scikit-learn matplotlib umap-learn
```

## Как запустить (Jupyter / kernel)
Да — файл `.ipynb` открывается через **Jupyter Notebook** или **JupyterLab** с **Python kernel**.

1. Установи JupyterLab:
```bash
pip install jupyterlab
```
2. Запусти:
```bash
jupyter lab
```
3. Открой `botnet_detection.ipynb`
4. Убедись, что CSV лежат в **той же папке** (или поправь пути в первых ячейках). fileciteturn5file0  
5. Выполни все ячейки **сверху вниз**:
   - загрузка и предобработка
   - split + scaling
   - обучение Random Forest
   - метрики + confusion matrix + UMAP fileciteturn5file0

## Структура репозитория
```
.
├── botnet_detection.ipynb
├── CTU13_Attack_Traffic.csv
├── CTU13_Normal_Traffic.csv
├── docs/
│   └── Botnet Detection using Machine Learning.docx
└── README.md
```

## Источники (как в отчёте)
- Egor Zakharenko (2024). Bagging and Random Forest… (Habr). fileciteturn5file0  
- Faisal Malik (2022). CTU13-CSV-Dataset (GitHub). fileciteturn5file0  
- Документация scikit‑learn: RandomForest* API. fileciteturn5file0
