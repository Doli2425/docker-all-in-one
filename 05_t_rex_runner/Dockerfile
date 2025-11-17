FROM golang:1.16

# git 설치
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

WORKDIR /go/app

# 소스: enthus1ast/chromeTrip → public/에 배치
RUN git clone https://github.com/zouariste/corona-runner.git ./public

# 초간단 정적 서버 (8080)
RUN printf '%s\n' \
'package main' \
'' \
'import ("log"; "net/http")' \
'' \
'func main(){' \
'  fs := http.FileServer(http.Dir("./public"))' \
'  http.Handle("/", fs)' \
'  log.Println("Serving ChromeTrip on :8080")' \
'  log.Fatal(http.ListenAndServe(":8080", nil))' \
'}' > /go/app/main.go

EXPOSE 8080
CMD ["go","run","/go/app/main.go"]
