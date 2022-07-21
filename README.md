# Go Gin example
| This repo is for Go Gin example .


## Table of contents

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
mkdir go-gin-api
cd 
code .
go mod init github.com/YOUR_USERNAME/go-example
```
3. Install Modules
```
go get github.com/spf13/viper
go get github.com/gin-gonic/gin
go get gorm.io/gorm
go get gorm.io/driver/postgres
```
4. Create Folders and files
```bash
mkdir -p cmd pkg/books pkg/common/db pkg/common/envs pkg/common/models pkg/common/config
touch Makefile cmd/main.go pkg/books/add_book.go pkg/books/controller.go pkg/books/delete_book.go pkg/books/get_book.go pkg/books/get_books.go pkg/books/update_book.go pkg/common/db/db.go pkg/common/envs/.env pkg/common/models/book.go pkg/common/config.go
```
5. Add Variable in .env
```
PORT=:3000
DB_URL=postgres://DB_USER:DB_PASSWORD@DB_HOST:DB_PORT/go-gin-api
```
6. Add Configuration in config
```pkg/common/db/db.go```
```
package config

import "github.com/spf13/viper"

type Config struct {
    Port  string `mapstructure:"PORT"`
    DBUrl string `mapstructure:"DB_URL"`
}

func LoadConfig() (c Config, err error) {
    viper.AddConfigPath("./pkg/common/config/envs")
    viper.SetConfigName("dev")
    viper.SetConfigType("env")

    viper.AutomaticEnv()

    err = viper.ReadInConfig()

    if err != nil {
        return
    }

    err = viper.Unmarshal(&c)

    return
}
```
7. Database Initialization
```pkg/common/db/db.go```
```bash
package db

import (
    "log"

    "github.com/PolunLin/go-gin-api/common/models"
    "gorm.io/driver/postgres"
    "gorm.io/gorm"
)

func Init(url string) *gorm.DB {
    db, err := gorm.Open(postgres.Open(url), &gorm.Config{})

    if err != nil {
        log.Fatalln(err)
    }

    db.AutoMigrate(&models.Book{})

    return db
}
```
## Project Struct
```
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
```python
python manage.py runserver
```
## Reference
1. https://betterprogramming.pub/build-a-scalable-api-in-go-with-gin-131af7f780c0
2. https://gin-gonic.com/docs/quickstart/