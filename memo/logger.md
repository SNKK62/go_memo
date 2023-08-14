# Logger

```go
func main() {
    file , err := os.Create("log.txt")
    if err != nil {
        log.Fatalln(err)
    }
    defer file.Close
    flags := log.Lshortfile | log.LstdFlags
    warnLogger := log.New(io.MultiWriter(file, os.Stderr), "WARN: ", flags)
}
```
- `log.Fatalln` はlogを生成した後に強制終了
- `log.Lshortfile` は行数を表示
- `logLstdFlags` は時刻情報を追加
- `io.MultiWriter` で同時に出力
