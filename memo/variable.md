# 変数

```go
var i int
or
i := 1
```

varの場合の初期化
| type    | default |
| ----    | ----    |
| bool    | false   |
| gint    | 0       |
| string  | ""      |
| pointer | nil     |
- varは関数外でも使える（0値で初期化する）
- := は関数内でしか使えない

```go
var i = 2
ui := uint16(2)
fmt.Printf("i: %[1]v %[1]T ui: %[2]v %[2]T, i, ui")
pi, title := 3.14, "Go"
const secret = "abc"
type Os int
const (
    Mac Os = iota + 1      #1
    Windows                #2
    Linux                  #3 
)
var (
    a int
    b string
    c bool
)
```
- varでも初期化は可能
- := でも型の明示は可能
- %vは値
- %Tは型
- 分割代入可能
- type で独自の型を定義
- iotaで自動割り当て
- varやconstで一括定義可能
