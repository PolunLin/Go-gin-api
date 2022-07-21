# Go-Gin-Api
| This repo is for go gin api .


## Table of contents
- [Go-Gin-Api](#go-gin-api)
  - [Table of contents](#table-of-contents)
  - [How to Create](#how-to-create)
  - [Repository Struct](#repository-struct)
  - [Run the application](#run-the-application)
  - [Result](#result)
  - [Reference](#reference)
## How to Create

1. Create Database
    ```bash
    psql -U postgres # open psql CLI with user postgres
    CREATE DATABASE go-gin-api;
    \l # list all databases
    \q #CLI exit
    ```
2. Clone the project
    ```bash
    git clone https://github.com/PolunLin/go-gin-api.git
    cd go-gin-api
    code .
    go mod init github.com/YOUR_USERNAME/go-gin-api
    ```
3. Install Modules
    ```
    go get github.com/spf13/viper
    go get github.com/gin-gonic/gin
    go get gorm.io/gorm
    go get gorm.io/driver/postgres
    ```
4. Environment Variable

    in ``` common/envs/.env```
    ```
    PORT=:3000
    DB_URL=postgres://DB_USER:DB_PASSWORD@DB_HOST:DB_PORT/go-gin-api
    ```

## Repository Struct

```bash
    tree /f
    go-gin-api
    │  go.mod
    │  go.sum
    │  Makefile
    │  README.MD
    │
    ├─cmd
    │      main.go
    │
    └─pkg
        ├─books
        │      add_book.go
        │      controller.go
        │      delete_book.go
        │      get_book.go
        │      get_books.go
        │      update_book.go
        │
        └─common
            ├─config
            │      config.go
            │
            ├─db
            │      db.go
            │
            ├─envs
            │      .env
            │
            └─models
                    book.go
```

## Run the application
```bash
    make server # or 
    go run cmd/main.go
```
## Result
1. POST:add a new Book
    ```bash
    curl --request POST \
    --url http://localhost:3000/books/ \
    --header 'Content-Type: application/json' \
    --data '{
        "title": "Book A",
        "author": "Author",
        "description": "Some cool description"
    }'
    ```
2. GET: Get All Books
    ```bash
    curl --request GET --url http://localhost:3000/books/
    ```
3. GET: Get Book by ID
    ```bash
    curl --request GET --url http://localhost:3000/books/1/
    ```
4. PUT: Update Book by ID
    ```bash
    curl --request PUT \
    --url http://localhost:3000/books/1/ \
    --header 'Content-Type: application/json' \
    --data '{
    "title": "Updated Book Name",
    "author": "Another author",
    "description": "Updated description"
    }'
    ```
5. DELETE: Delete Book by ID
    ```bash
    curl --request DELETE --url http://localhost:3000/books/1/
    ```
## Reference
   1. https://betterprogramming.pub/build-a-scalable-api-in-go-with-gin-131af7f780c0
   2. https://gin-gonic.com/