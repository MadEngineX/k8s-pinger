FROM python:3.6-alpine3.8
COPY node-ping.py /app/
WORKDIR /app
RUN pip3 install --upgrade --trusted-host pypi.org --trusted-host files.pythonhosted.org pip prometheus_client better_exchook  && apk add --no-cache fping
ENTRYPOINT ["python3", "/app/node-ping.py"]