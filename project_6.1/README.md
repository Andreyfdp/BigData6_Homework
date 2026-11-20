# Big Data 6.1 — прогнозирование оттока

## Задача
Конвейер: загрузка признаков и меток, разделение данных, масштабирование,
обучение Random Forest, оценка качества, сохранение модели и метрик.

## Установка и запуск в Google Colab
1. Откройте `InnopolisBigData6_1_DZ_cells_fixed.ipynb`.
2. Положите `out.zip` и `features.parquet` в `MyDrive/BigData/data/`.
3. Выполните все ячейки по порядку.

## Артефакты
- `/content/project_6.1/config.json` — параметры конвейера
- `/content/project_6.1/pipeline.log` — логи
- `/content/processed/model_6.1/` — модель, scaler, признаки, метрики
- `architecture.md` — схема; `refactoring_report.md` — отчёт

## Docker
Ячейка 4 ДЗ создаёт `runner.ipynb` (код из функций практики) и `Dockerfile`.
После установки Docker выполните `docker build -t bigdata61 .` в папке проекта.
Для запуска нужны три монтирования: файл `features.parquet` в
`/content/processed/features.parquet`, файл `churn_truth.csv` в
`/content/out/reference/churn_truth.csv`, папка для модели в
`/content/processed/model_6.1`.
Пример запуска — в исходном коде ячейки 4 ДЗ.
