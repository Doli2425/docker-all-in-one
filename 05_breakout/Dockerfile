FROM golang:1.16
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

WORKDIR /go/app
RUN git clone https://github.com/SaraSanchezL/2D-breakout-game.git .
RUN printf '%s\n' \
'package main' \
'' \
'import ("log"; "net/http")' \
'' \
'func main(){' \
'  fs := http.FileServer(http.Dir("."))' \
'  http.Handle("/", fs)' \
'  log.Println("Serving Breakout on :8080")' \
'  log.Fatal(http.ListenAndServe(":8080", nil))' \
'}' > /go/app/main.go

EXPOSE 8080
CMD ["go","run","/go/app/main.go"]
