## Обработка ошибок

``` go
type errorString struct {
    s string
}

func (e *errorString) Error() string {
    return e.s
}

func New(text string) error {
    return &errorString{text}
}
```
- Создание кастомной ошибки и ее конструктора
``` go
func Sqrt(f float64) (float64, error) {
    if f < 0 {
        return 0, errors.New("math: square root of negative number")
    }
    // implementation
}
```
- Применение кастомной ошибки

``` go
f, err := Sqrt(-1)
if err != nil {
    fmt.Println(err)
}
```
- Обработка ошибки

``` go
func SetUserAge(u *db.User, age int) error {
    if err := db.SetAge(u, age); err != nil {
      return fmt.Errorf("SetUserAge: failed executing db update: %w", err)
    }
}
```
- `Errorf` - специальный вывод для ошибок в пакете `fmt`

