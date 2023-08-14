# interface

```go
type controller interface {
    speedUp() int
    speedDown() int
}
type vehicle struct {
    speed       int
    enginePower int
}
type bycycle struct {
    speed      int
    humanPower int
}
func (v *vehicle) speedUp() int {
    v.speed += 10 * v.enginePower
    return v.speed
}
func (v *vehicle) speedDown() int {
    v.speed -= 5 * v.enginePower
    return v.speed
}
func (b *bycycle) speedUp() int {
    b.speed += 10 * b.humanPower
    return b.speed
}
func (b *bycycle) speedDown() int {
    b.speed -= 5 * b.humanPower
    return b.speed
}

func speedUpAndDown(c controller) {
    fmt.Println(c.speedUp())
    fmt.Println(c.speedDown())
}
v := &vehicle{0, 5}
speedUpAndDown(v)

var i1 interface{}
var i2 any

func checkType(i any){
    switch i.(type) {
    case nil:
        fmt.Println("nil")
    case int:
        fmt.Println("int")
    case string:
        fmt.Println("string")
    default:
        fmt.Println("unknown")
    }
}
```
- interface の関数を全て実装したstructは自動的にinterfaceと見なされる
- interface{} と any は同じ
- String() を実装すればStringer interfaceとなり，println で使える
