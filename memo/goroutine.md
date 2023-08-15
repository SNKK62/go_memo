# GoRoutine

```go
var wg sync.WaitGroup
wg.Add(1)
go func() {
    defer wg.Done()
    fmt.Println("goroutine invoked")
}()
wg.Wait()
fmt.Printf("num of working goroutines: %d \n", runtime.NumGoroutine())
fmt.Println("main func finish")
```
- `runtime.NumGoroutine()` でthreadの数を取得できる
- `wg.Add(1)` でカウンタを+1
- `wg.Done()` でカウンタを-1
- `wg.Wait()` でカウンタが0になるまで待機

## tracer
逐次処理
```go
func main() {
    f, err := os.Create("trace.out")
    if err != nil {
        log.Fatalln("Error: ", err)
    }
    defer func() {
        if err := f.Close(); err != nil {
            log.Fatalln("Error", err)
        }
    }()
    if err := trace.Start(f); err != nil {
        log.Fatalln("Error:", err)
    }
    defer trace.Stop()
    ctx, t := trace.NewTask(context.Background(), "main")
    defer t.End()
    fmt.Println("The number of logical CPU Cores:", runtime.NumCPU())

    task(ctx, "Task1")
    task(ctx, "Task2")
    task(ctx, "Task3")
}
func task(ctx context.Context, name string) {
    defer trace.StartRegion(ctx, name).End()
    time.Sleep(time.Second)
    fmt.Println(name)
}
```
- `trace.StartRegion(ctx, name).End()` は先に実行されてchainの最後が最後に実行される(defer の仕様)
- `go tool trace [trace.out]` で結果を確認できる

並列処理(goroutine)
```go
func main() {
    f, err := os.Create("trace.out")
    if err != nil {
        log.Fatalln("Error: ", err)
    }
    defer func() {
        if err := f.Close(); err != nil {
            log.Fatalln("Error", err)
        }
    }()
    if err := trace.Start(f); err != nil {
        log.Fatalln("Error:", err)
    }
    defer trace.Stop()
    ctx, t := trace.NewTask(context.Background(), "main")
    defer t.End()
    fmt.Println("The number of logical CPU Cores:", runtime.NumCPU())

    var wg sync.WaitGroup
    wg.Add(3)
    ctask(ctx, &wg, "Task1")
    ctask(ctx, &wg, "Task2")
    ctask(ctx, &wg, "Task3")
    wg.Wait()
    fmt.Println("main func finish")
}

func ctask(ctx context.Context, wg *sync.WaitGroup, name string) {
    defer trace.StartRegion(ctx, name).End()
    defer wg.Done()
    time.Sleep(time.Second)
    fmt.Println(name)
}
```

注意
```go
s := []int{1, 2, 3}
// 間違い
for _, i := range s {
    wg.Add(1)
    go func() {
        defer wg.Done()
        fmt.Println(i)
    }
}
// 正解
for _, i := range s {
    wg.Add(1)
    go func(i int) {
        defer wg.Done()
        fmt.Println(i)
    }(i)
}
wg.Wait()
```
- 順番は前後する
