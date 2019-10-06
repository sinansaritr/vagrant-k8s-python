FROM alpine:3.7

WORKDIR /code

COPY requirements.txt .

RUN apk add --no-cache python py-mysqldb && \
   python -m ensurepip && \
   rm -r /usr/lib/python*/ensurepip && \
   pip install --upgrade pip setuptools && \
   pip install --no-cache-dir -r requirements.txt && \
   rm -r /root/.cache

ENV MYSQL_INSTANCE_NAME mysql 
ENV MYSQL_PORT_3306_TCP_ADDR 127.0.0.1
ENV MYSQL_PORT_3306_TCP_PORT 3306
ENV MYSQL_USERNAME root
ENV MYSQL_PASSWORD my-secret-pw

COPY src src

EXPOSE 3000

CMD python src/app.py 