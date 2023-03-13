FROM python:3.9

# Some default values
ENV HOST="http://localhost:8080/" \
    SILENT=1 \
    NUM_CLIENTS=1000000 \
    ERROR=1 \
    RUN_TIME=24h
    

WORKDIR /load

COPY requirements.txt /load/

RUN pip install -r requirements.txt

COPY entrypoint.sh /load/
COPY robot-shop.py /load/

CMD ["./entrypoint.sh"]

