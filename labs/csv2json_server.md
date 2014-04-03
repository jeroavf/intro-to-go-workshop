# csv2json-server

HTTP API to convert CSV to JSON

#### Create

    ${GOPATH}/src/github.com/${username}/csv2json-server

#### Edit

    ${GOPATH}/src/github.com/${username}/csv2json-server/main.go

-

	package main

	import (
		"log"
		"net/http"

		"github.com/kelseyhightower/csv2json"
	)

	var (
		columns = []string{"Name", "Date", "Title"}
	)

	func csv2JsonServer(w http.ResponseWriter, req *http.Request) {
		jsonData, err := csv2json.Convert(req.Body, columns)
		defer req.Body.Close()
		if err != nil {
			http.Error(w, "Could not convert csv to json", 503)
		}
		w.Write(jsonData)
	}

	func main() {
		http.HandleFunc("/csv2json", csv2JsonServer)
		err := http.ListenAndServe(":8080", nil)
		if err != nil {
			log.Fatal("ListenAndServe: ", err)
		}
	}

#### Build

    go build -o csv2json-server main.go

#### Run

    ./csv2json-server

## Exercise

### Make the listen port configurable via the environment

#### Hint

    import (
        "os"
        "net"
    )

    func main() {
        listenAddr := net.JoinHostPort(host, port)
    }

### Improve logging

#### Hint

    import (
        "log"
    )