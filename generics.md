# Generics

```go
type customConstraints interface {
    ~int | int16 | float32 | float64 | string
}
type NewInt int
func add[T customConstraints](x, y T) T {
    return x + y
}

func min[T constraints.Orderd](x, y T) T {
    if x < y {
        return x
    }
    return y
}

m1 := map[string]uint {
    "A": 1,
    "B": 2,
    "C": 3,
}
m2 := map[int]float32{
    1: 1.23
    2: 4.56
    3: 7.89
}
func[K int | string, V constraints.Float | constraints.Integer](m map[K]V) V {
    var sum V
    for _, v := range m {
        sum += v
    }
    return sum
}
```
- ~int でintを元に作った型も含まれるようになる
