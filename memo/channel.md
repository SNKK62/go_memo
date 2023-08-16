# Channel

Goroutine間のデータのやりとり
```go
func main() {
    // Pattern1
    ch := make(chan int)
    var wg sync.WaitGroup
    wg.Add(1)
    go func() {
        defer wg.Done()
        ch <- 10
        time.Sleep(500 * time.Millisecond)
    }()
    fmt.Println(<-ch)
    wg.Wait()

    // Pattern2
    ch1 := make(chan int)
    go func() {
        fmt.Println(<-ch1)
    }()
    fmt.Printf("num of working goroutines: %d \n", runtime.NumGroutine())
    // Goroutine Leak
}
```
- `ch <- [ ]` : write
- `<-ch` : read
- `<- ch` は値が入れられるまでdeadlock 
```go
package main

import (
    "testing"

    "go.uber.org/goleak"
)

func TestLeak(t *testing.T) {
    defer goleak.VerifyNone(t)
    main()
}
```
buffer付き
```go
// NG
ch2 := make(chan int, 1)
ch2 <- 2
ch2 <- 3
fmt.Println(<-ch2)
```
- bufferの数まで入れられる

## Closed
```go
ch1 := make(chan int)
var wg sync.WaitGroup
wg.Add(1)
go func() {
    defer wg.Done()
    fmt.Println(<-ch1)
}()
ch1 <- 10
close(ch1)
v, ok := <-ch1
fmt.Printf("%v %v \n", v, ok) // 0 false
wg.Wait()

ch2 := make(chan int, 2)
ch2 <- 1
ch2 <- 2
close(ch2)
v, ok = <-ch2
fmt.Printf("%v %v \n", v, ok) // 1 true
v, ok = <-ch2
fmt.Printf("%v %v \n", v, ok) // 2 true
v, ok = <-ch2
fmt.Printf("%v %v \n", v, ok) // 0 false
```

## capsel
```go
func main() {
    ch3 := generateCountStream()
    for v := range ch3 {
        fmt.Println(v)
    }

    // 通知専用Channel
    nCh := make(chan struct{})
    for i :- 0; i < 5; i++ {
        wg.Add(1)
        go func(i int) {
            defer wg.Done()
            fmt.Printf("goroutine %v started \n", i)
            <-nCh
            fmt.Println(i)
        }(i)
    }
    time.Sleep(2 * time.Second)
    close(nCh)
    fmt.Println("unblocked by manual close")

    wg.Wait()
    fmt.Println("finish")
}
func generateCountStream() <- chan int {
    ch := make(chan int)
    go func() {
        defer close(ch)
        for i := 0; i <= 5; i++ {
            ch <- i
        }
    }()
    return ch
}
```
- `<- chan int` 読み込み専用のchannelの型
- `sturct{}` は０バイトしか消費しないので通知専用のchannelに適している
- 通知専用channelではcloseするまで処理を止めている（closeした瞬間に一気に処理が走る）
