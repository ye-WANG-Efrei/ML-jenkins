# Dockerfile to build a flask app
FROM python:3
WORKDIR /usr
COPY   . .
RUN pip3 install -r requirements.txt
EXPOSE 5000
CMD ["python","-m","flask","run"]
