# docker build -t recommendations -f Dockerfile ..  // build context set to parent folder
# docker run -it -p 127.0.0.1:50051:50051/tcp --name rec_run recommendations

FROM python:3.10-slim

RUN mkdir /service && mkdir /service/recommendations
COPY recommendations/requirements.txt /service/recommendations/
RUN python -m pip install --no-cache-dir -r /service/recommendations/requirements.txt 

COPY protobufs/ /service/protobufs/
COPY recommendations/ /service/recommendations/
WORKDIR /service/recommendations

RUN python -m grpc_tools.protoc -I ../protobufs --python_out=. --grpc_python_out=. ../protobufs/recommendations.proto

# default gRPC port
EXPOSE 50051
ENTRYPOINT [ "python", "recommendations.py" ]