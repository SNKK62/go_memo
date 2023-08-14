Go package
```go
$ go mod init module_name
```
でmoduleを初期化

```go
$ go mod tidy
```
でpackageをinstallできる

````go
$ go build -o bin_file
````
でbuildできる

変数は同じpackageでは共有される
privateな変数・関数は小文字
publicな変数・関数は大文字で始める
