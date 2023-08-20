# Errors

```go
err01 := errors.New("something  wrong")
fmt.Printf("%[1]p %[1]T %[1]V \n", err01)

err0 := fmt.Errorf("add info: %w", errors.New("original error"))
fmt.Printf("%[1]p %[1]T %[1]v \n", err0)  # add info: original error
fmt.Println(errors.Unwrap(err0)) # original error

ErrCustom := errors.New("not found")
err2 := fmt.Errorf("in repository layer: %w", ErrCustom)
err2 = fmt.Errorf("in service layer: %w", err2)
fmt.Println(err2)  #in service layer: in repository layer: not found

if errors.Is(err2, ErrCustom) {
    fmt.Println("matched")
}
```
- printlnはErrorを実装しているかもcheckしている
- %w -> wrap
- ``errors.Unwrap`` でwrapされたerrorをunwrapできる
- `errors.Is` でunwrapを繰り返し含まれるかcheck
