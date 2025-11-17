# 1) 과제 요구: golang 1.16 고정
FROM golang:1.16

# 2) 2048 소스 가져올 도구 설치 (git)
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# 3) 앱 작업 디렉토리
WORKDIR /go/app

# 4) 2048 소스 클론 (루트에 index.html 등 정적 파일 존재)
RUN git clone https://github.com/gabrielecirulli/2048.git ./

# 5) 초간단 정적서버 main.go 생성
#    (현재 디렉토리(/go/app)의 정적 파일들을 그대로 서빙)
RUN printf '%s\n' \
'package main' \
'' \
'import ("log"; "net/http")' \
'' \
'func main(){' \
'  fs := http.FileServer(http.Dir("."))' \
'  http.Handle("/", fs)' \
'  log.Println("Serving 2048 on :8080")' \
'  log.Fatal(http.ListenAndServe(":8080", nil))' \
'}' > /go/app/main.go

# 6) 네트워킹/실행
EXPOSE 8080
CMD ["go", "run", "/go/app/main.go"]

