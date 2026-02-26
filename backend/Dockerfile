FROM gcc:latest

WORKDIR /app
COPY app.cpp .
RUN g++ app.cpp -o app

CMD ["sh", "-c", "./app && tail -f /dev/null"]
