
# Big Data 6.1 — прогнозирование оттока

## Описание задачи

Конвейер для прогнозирования оттока абонентов:
загрузка данных, предобработка, обучение Random Forest,
оценка качества и сохранение результатов.

## Установка зависимостей

```bash
pip install -r requirements.txt
```

## Запуск в Google Colab

1. Откройте `InnopolisBigData6_1_HomeWork.ipynb`.
2. Разместите `out.zip` и `features.parquet` в `MyDrive/BigData/data/`.
3. Подключите Google Drive и выполните все ячейки по порядку.

## Архитектура

Схема конвейера представлена в [architecture.md](architecture.md).

## Docker

Для запуска нужны `features.parquet` и `churn_truth.csv`
из исходных данных. Разместите их в папке `project_6.1`.

Из этой папки выполните в Linux или Google Cloud Shell:

```bash
docker build -t bigdata61 .

mkdir -p model_outputs docker_results docker_logs
touch docker_logs/pipeline.log

docker run --rm \
  -v "$PWD/features.parquet:/content/processed/features.parquet:ro" \
  -v "$PWD/churn_truth.csv:/content/out/reference/churn_truth.csv:ro" \
  -v "$PWD/model_outputs:/content/processed/model_6.1" \
  -v "$PWD/docker_results:/app/results" \
  -v "$PWD/docker_logs/pipeline.log:/content/project_6.1/pipeline.log" \
  bigdata61
```

## Подтверждение работы Docker

Образ успешно собран и контейнер запущен в Google Cloud Shell
на 400 синтетических записях.

- [Выполненный notebook](../docker_run.ipynb)
- [Метрики контейнера](../metrics.json)

## Артефакты

- `config.json` — параметры конвейера
- `pipeline.log` — журнал выполнения
- `best_model.pkl` — обученная модель
- `scaler.pkl` — масштабирование признаков
- `features.json` — используемые признаки
- `metrics.json` — метрики качества
- `architecture.md` — архитектурная схема
- `refactoring_report.md` — отчёт по рефакторингу

В Colab модель сохраняется в `/content/processed/model_6.1/`.

## Результаты

На исходных данных:
- ROC-AUC: 0.9769
- F1: 0.7370

Docker дополнительно проверен на синтетических данных.
