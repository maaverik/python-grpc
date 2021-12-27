# docker build -t recommendations -f Dockerfile ..  // build context set to parent folder
FROM python:3.10-slim

RUN mkdir /service
COPY protobufs/ /service/protobufs/
COPY recommendations/ /service/recommendations/
WORKDIR /service/recommendations

RUN python -m pip install --no-cache-dir -r requirements.txt && \
    python -m grpc_tools.protoc -I ../protobufs --python_out=. --grpc_python_out=. ../protobufs/recommendations.proto

# default gRPC port
EXPOSE 50051
ENTRYPOINT [ "python", "recommendations.py" ]