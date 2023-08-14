# function/closure

## function
```go
func funcDefer() {
    defer fmt.Println("main func final-finish")
    defer fmt.Println("main func semi-finish")
    fmt.Println("hello world")
}

func trimExtension(files ...string) []string {
    out := make([]string, 0, len(files))
    for _, f := range files {
        out = append(out, strings.TrimSuffix(f, ".csv"))
    }
}
files := []string{"file1.csv", "file2.csv", "file3.csv"}
fmt.Println(trimExtension(files...))

func fileChecker(name string) (string, error) {
    f, err := os.Open(name)
    if err != nil {
        return "", errors.New("file not found")
    }
    defer f.Close()
    return name nil
}

<!-- 無名関数 -->
func(i int) {
    fmt.Println(i)
}(i)  #即時実行
f1 := func(i int) int {
    return i + 1
}

func addExt(f func(file string) string, name string) {
    fmt.Println(f(name))
}

func multiply() func(int) int {
    return func(n int) int {
        return n * 1000
    }
}
```
- defer は関数を抜けるタイミングで実行（stak?）
- ...string で可変長
- files... で展開
- 無名関数は引数にできる
- 無名関数は返り値にできる

## closure
```go
func coutUp() func(int) int {
    count := 0
    return func(n int) int {
        count += n
        return count
    }
}

f4 := countUp()
for i := 1; i <= 5; i++ {
    v := f4(2)
    fmt.Printf("%v \n", v)
}
#2
#4
#6
#8
#10
```
- closureを使うことによってglobal変数のような変数が作れる
