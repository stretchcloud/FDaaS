FROM python:2.7.14-alpine3.7
WORKDIR /root/

ADD https://github.com/openfaas/faas/releases/download/0.6.9/fwatchdog /usr/bin
RUN chmod +x /usr/bin/fwatchdog

ENV PATH=$PATH:/root/.local/bin/
RUN pip install --upgrade pip
RUN pip install awscli --upgrade --user
RUN pip install boto3
RUN apk add --no-cache less groff

RUN mkdir /root/.aws
ADD ./config /root/.aws/
ADD ./credentials /root/.aws/
ADD ./aws-boto-test.py /root/

ENV fprocess="python /root/aws-boto-test.py"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]