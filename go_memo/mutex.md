# Mutex

```go
var wg sync.WaitGroup
var mu sync.Mutex
var i int
wg.Add(2)
go func() {
    defer wg.Done()
    mu.Lock()
    defer mu.Unlock()
    i++ // データ競合
    i = 1 // race condition
}()
go func() {
    defer wg.Done()
    mu.Lock()
    defer mu.Unlock()
    i++ // データ競合
    i = 2 // race condition
}
wg.Wait()
fmt.Println(i)
```
- `go run -race [main.go]` でデータ競合をcheck
- race condition は検知できない
## RWMutex
```go
func main() {
    var wg sync.WaitGroup
    var rwMu sync.RWMutex
    var c int

    wg.Add(4)
    go write(&rwMu, $wg, &c)
    go read(&rwMu, &wg, &c)
    go read(&rwMu, &wg, &c)
    go read(&rwMu, &wg, &c)

    wg.Wait()
    fmt.Println("finish")
}
func read(mu *sync.RWMutex, wg *sync.WaitGroup, c *int) {
    defer wg.Done()
    time.Sleep(10 * time.Millisecond)
    mu.RLock()
    defer mu.RUnlock()
    fmt.Println("read lock")
    fmt.Println(*c)
    time.Sleep(1 * time.Second)
    fmt.Println("read unlock")
}
func write(mu *sync.RWMutex, wg *sync.WaitGroup, c *int) {
    defer wg.Done()
    mu.Lock()
    defer mu.Unlock()
    fmt.Println("write lock")
    *c += 1
    time.Sleep(1 * time.Second)
    fmt.Println("write unlock")
}

```

## Atomic
```go
var wg sync.WaitGroup
var c int64

for i := 0; i < 5; i++ {
    wg.Add(1)
    go func() {
        defer wg.Done()
        for j := 0; j < 10; j++ {
            atomic.AddInt64(&c, 1)
        }()
    }
}
wg.Wait()
fmt.Println(c)
fmt.Println("finish")
```
