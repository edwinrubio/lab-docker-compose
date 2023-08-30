FROM python:3.8-slim-buster

WORKDIR /app

COPY requeriments.txt requeriments.txt

RUN pip3 install -r requeriments.txt

COPY . .

EXPOSE 1000

CMD ["python3", "-m", "flask", "run", "--host=0.0.0.0", "--port=7000"]
