## Обработка ошибок
### Пример 1:

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

### Пример 2:

``` go
func Sqrt(f float64) (float64, error) {
    if f < 0 {
        return 0, errors.New("math: square root of negative number")
    }
    // implementation
}
```
- Применение кастомной ошибки

### Пример 3:

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
- `Errorf` - специальный вывод для ошибок в [[Полезные пакеты#fmt|пакете]] `fmt`

## Panic

```go
import "os"

func main() {
    _, err := os.Create("/tmp/file")
    if err != nil {
        panic(err)
    }
}
```
- `panic` используют для быстрого отказа при ошибках, которые не должны возникать во время нормальной работы
- Работает как **прерывание**: вызовет панику, распечатает сообщение об ошибке и трейс выполнения и завершит работу с ненулевым статусом.

## Recover

```go
func getRecover() {
    recover()
}

func throwPanic() {
    defer getRecover()
    panic("Lets panic!")
}

func main() {
    throwPanic()
    fmt.Println()
}
```
- для перехвата сигнала паники используется `recover`
- работает только при вызове отложенной функции 