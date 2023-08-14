# if/for/switch

## if
```go
a := -1
if a == 0 {
    fmt.Println("zero")
} else if a > 0 {
    fmt.Println("positive")
} else {
    fmt.Println("negative")
}
```

## for
```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}

<!-- 無限ループ -->
for {
    if i > 3 {
        break
    }
    fmt.Println("working")
    time.Sleep(2 * time.Second)
}
```

## switch
```go
loop:
    for i := 0; i < 10; i++ {
        switch i {
        case 2:
            continue
        case 3:
            continue
        case 8:
            break loop
        default:
            fmt.Printf("%v ", i)
        }
    }
    fmt.Printf("\n")
```

## for range
```go
items := []item{
    {price: 10.},
    {price: 20.},
    {price: 30.},
}
for _, i := range items {
    i.price *= 1.1
}
type item struct {
    price float32
}
```
