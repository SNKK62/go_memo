# Pointer
```go
var ui1 uint16
fmt.Printf("memory address of ui1: %p\n", &ui1)
var p1 *uint16
p1 = &ui1
fmt.Printf("value of dereference of p1: %v", *p1)
*p1 = 1
fmt.Printf("size of p1: %d[bytes]\n", unsafe.Sizeof(p1))
```
- pointerはC言語と同じ
- \* はdereference
- pointerのサイズは８bytes


double pointer
```go
var ui1 uint16
var p1 *uint16 = &ui1
var pp1 **uint16 = &p1
```

shadowing
```go
ok, result := true, "A"
if ok {
    result := "B"
    println(result)
} else {
    result := "C"
    println(result)
}
println(result)

#>> B
#>> A
```
- scope内で再定義したものは別変数
