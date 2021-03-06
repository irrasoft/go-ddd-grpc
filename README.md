GRPC CRUD EXAMPLE USING POSTGRESS

# Creating SSL/TLS Certificates

 - server.key : a private RSA key to sign and authenticate the public key
	```shell
	openssl genrsa -out server.key 2048
	```

 - server.pem/ server.crt : self-signed x.509 public keys for distribution
	```shell
	openssl req -new -x509 -sha256 -key server.key -out server.crt -days 3650

	```
 - server.csr: a certificate signing request to access the CA(Certificate Authority)
	```shell
	openssl req -new -sha256 -key server.key -out server.csr

	```

	```shell
	openssl x509 -req -sha256 -in server.csr -signkey server.key -out server.crt -days 3650

	```
# App
  - Run Unit Test
    ```shell
    make test
    ```

  - Format Go Code
    ```shell
    make format
    ```

  - Run Server
    ```shell
    DB_USER=postgres DB_PASSWORD=12345 DB_HOST=localhost DB_NAME=gp go run main.go
    ```

  - Run Go Client,
    go to client folder
    ```shell
    cd /client
    ```

    ```shell
    SERVER_HOST=localhost:8080 go run main.go
    ```
  - Run NodeJs Client,
    go to client folder
    ```shell
    cd /client/nodeclient
    ```

    ```shell
    node index.js
    ```

# Docker environmet
  - Build the image
    ```shell
    make build
    ```

  - Run Container
    ```shell
    docker run --rm -p 8080:8080 -e DB_USER=db_user -e DB_PASSWORD=db_password -e DB_HOST=db_host -e DB_NAME=db_name wuriyanto/go-ddd-grpc
    ```
