FROM python:3.11.2-alpine3.17

WORKDIR /backend

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

COPY . .

CMD [ "python3", "main.py" ]