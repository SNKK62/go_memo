# slice/map

## slice
```go
var a1 [3]int
var a2 = [3]int{1, 2, 3}
a3 := [...]int{1, 2}
len(a3) #2
cap(a3) #2

var s1 []int #slice
s2 := []int{}
len(s1) == len(s2) == 0
cap(s1) == cap(s2) == 0
fmt.Println(s1 == nil)  #true
fmt.Println(s2 == nil)  #false
s1 = append(s1, 1, 2, 3)
s3 := []int{4, 5, 6}
s1 = append(s1, s3...)

s4 := make([]int, 0, 2)
s5 := make([]int, 4, 6) #[0, 0, 0, 0]
s6 := s5[1:3]
s6[1] = 10
fmt.Printf(%v, s5) #[0, 0, 10, 0]
s6 = append(s6, 2)
fmt.Printf(%v, s5) #[0, 0, 10, 2]

sc6 := make([]int, len(s5[1:3]))
copy(sc6, s5[1:3])

s5 = make([]int, 4, 6)
fs6 := s5[1:3:3]
fs6[0] = 6
fs6[1] = 7
fs6 = append(fs6, 8)
fmt.Printf(%v, s5) #[0, 6, 7, 0]
fmt.Printf(%v, fs6) #[6, 7, 8]
s5[3] = 9
fmt.Printf(%v, s5) #[0, 6, 7, 9]
fmt.Printf(%v, fs6) #[6, 7, 8]

```
- s5[1:3:3] -> [start:end:メモリを共有する最大のindex]

## map
```go
var m1 map[string]int
m2 := map[string]int{}
fmt.Printf("%v %v \n", m1, m1 == nil) #map[] true
fmt.Printf("%v %v \n", m2, m2 == nil) #map[] false
m2["A"] = 0
m2["B"] = 10
m2["C"] = 0
delete(m2, "A")
v, ok := m2["A"] #0 false
v, ok = m2["C"]  #0 true

for k, v := range m2 {
    fmt.Printf("%v, %v \n", k, v)
}
```
