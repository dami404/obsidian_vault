```go
import (
    "fmt"
    "time"
)

func say(s string) {
    for i := 0; i < 3; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s)
    }
}

func main() {
    go say("world")

    go func(msg string) {
        fmt.Println(msg)
    }("going")
    
    say("hello")
}
```
**Вывод:**
```
going
world
hello
world
hello
world
hello
```
- Реализация асинхронности
- **Формат** - `go функция()`
- Можно использовать с [[Функции#Анонимные функции|анонимными функциями]]