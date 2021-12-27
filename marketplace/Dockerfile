# docker build -t marketplace -f Dockerfile ..  // build context set to parent folder
# docker run -p 127.0.0.1:5200:5000/tcp --network microservices -e RECOMMENDATIONS_HOST=recommendations --name market_run marketplace

FROM python:3.10-slim

RUN mkdir /service && mkdir /service/marketplace
COPY marketplace/requirements.txt /service/marketplace/
RUN python -m pip install --no-cache-dir -r /service/marketplace/requirements.txt 

COPY protobufs/ /service/protobufs/
COPY marketplace/ /service/marketplace/
WORKDIR /service/marketplace

RUN python -m grpc_tools.protoc -I ../protobufs --python_out=. --grpc_python_out=. ../protobufs/recommendations.proto

# port for flask
EXPOSE 5000

# required for flask
ENV FLASK_APP=marketplace.py
ENTRYPOINT  ["flask", "run", "--host=0.0.0.0"]