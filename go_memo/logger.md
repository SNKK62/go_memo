# Logger

```go
func main() {
    file , err := os.Create("log.txt")
    if err != nil {
        log.Fatalln(err)
    }
    defer file.Close()
    flags := log.Lshortfile | log.LstdFlags
    warnLogger := log.New(io.MultiWriter(file, os.Stderr), "WARN: ", flags)
    errLogger := log.New(io.MultiWriter(file, os.Stderr), "ERROR: ", flags)

    warnLogger.Println("A")
    errLogger.Fatalln("B")
    #WARN: 2023/08/15 11:22:44 main.go:58: A
    #ERROR: 2023/08/15 11:22:44 main.go:59: B
}
```
- `log.Fatalln` はlogを生成した後に強制終了
- `log.Lshortfile` は行数を表示
- `logLstdFlags` は時刻情報を追加
- `io.MultiWriter` で同時に出力
