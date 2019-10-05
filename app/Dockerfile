FROM alpine:3.7

WORKDIR /code

COPY requirements.txt .

RUN apk add --no-cache python && \
   python -m ensurepip && \
   rm -r /usr/lib/python*/ensurepip && \
   pip install --upgrade pip setuptools && \
   pip install --no-cache-dir -r requirements.txt && \
   rm -r /root/.cache

COPY src/ src/

EXPOSE 3000

CMD python src/app.py
