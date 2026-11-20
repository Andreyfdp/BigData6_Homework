FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY runner.ipynb /app/runner.ipynb
COPY config.json /content/project_6.1/config.json

RUN mkdir -p /content/processed/model_6.1 /content/out/reference /app/results

CMD ["jupyter", "nbconvert", "--execute", "--to", "notebook", "--ExecutePreprocessor.timeout=1200", "--output", "/app/results/run.ipynb", "/app/runner.ipynb"]
