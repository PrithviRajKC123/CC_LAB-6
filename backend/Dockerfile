FROM gcc:latest

WORKDIR /app
COPY app.cpp .
RUN g++ app.cpp -o app

RUN apt-get update && apt-get install -y python3

EXPOSE 8080

CMD python3 -m http.server 8080
