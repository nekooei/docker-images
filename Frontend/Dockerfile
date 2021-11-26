FROM alpine:latest

ENV PYTHONUNBUFFERED=1
RUN apk update
RUN apk add --update --no-cache git nodejs npm python3 python3-dev build-base libffi-dev
RUN ln -sf python3 /usr/bin/python

RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools

RUN npm install --global yarn

RUN git clone https://github.com/kartevonmorgen/kartevonmorgen-v1 /frontend
WORKDIR /frontend

RUN yarn install

# Install Frontend
WORKDIR /frontend/scripts/python
RUN python3 -m venv venv
RUN . ./venv/bin/activate
RUN pip3 install -r requirements.txt

RUN python3 tag-frequency-cron.py --dev --sync-once --log-level debug

RUN npm install pm2 -g

WORKDIR /frontend
RUN yarn run build:dev


CMD ["yarn", "run", "start:production"]
#CMD ["pm2-runtime", "start", "'yarn run start:production'", "--name", "kartevonmorgen"]