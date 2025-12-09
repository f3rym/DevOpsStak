FROM python:3.11.5-alpine3.18

RUN apk add --update  
RUN apk add curl 
RUN rm -rf /var/cache/apk/*

RUN adduser -D worker
USER worker
WORKDIR /app

COPY --chown=worker:worker requirements.txt requirements.txt
RUN pip install --user --no-cache-dir -r requirements.txt

ENV PATH="/home/worker/.local/bin:${PATH}"

COPY --chown=worker:worker app/ ./app/

EXPOSE 8000

ENTRYPOINT [ "uvicorn", "app.main:app", "--host", "0.0.0.0" ]