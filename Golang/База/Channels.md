- Нужны для передачи данных между [горутинами](obsidian://open?vault=obsidian_vault&file=Golang%2F%D0%91%D0%B0%D0%B7%D0%B0%2FGoroutines)
## Объявление

```go
ch := make(chan int)
```
- **Дефолтное значение** - `nil`
- **Тип данных канала** - тип данных, которые он передает

## Инициализация

```go
ch := make(chan int)
go func() {
	ch <- 1
	ch <- 2
	time.Sleep(500 * time.Microsecond)
}()
fmt.Println(<-ch)
fmt.Println(<-ch)
```
- Каждая операция записи в канал блокирует [[Goroutines|горутину]]

## Чтение

```go
ch := make(chan int)
go func() {
	for i := range 10 {
		ch <- i
		time.Sleep(500 * time.Microsecond
	}
	close(ch)
}()
for {
	val, open := <- ch
	if !open {
		break
	}
	fmt.Println(val)
}
```
- `open` - показывает открыт или закрыт канал, необязательный аргумент
- `close()` - закрытие канала  для избежания `deadlock` в бесконечном цикле


## Deadlock

```go
fatal error: all goroutines are asleep - deadlock!
```
- происходит, когда из-за чтения или записи в канал происходит блокировка, однако ни одна [[Goroutines|горутина]] никогда не прочитает из него данные

# Однонаправленные каналы

## Объявление

```go
roc := make(<-chan int)
soc := make(chan<- int)
```
- `roc` канал для чтения, а `soc` канал для записи
- Использование однонаправленного канала улучшает безопасность типов в программe

# Buffered Channels

## Объявление

```go
ch := make(chan string, 2)
```
- Буферизированный канал обладает длиной

## Инициализация

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
fmt.Println(<-ch)
ch <- 3
fmt.Println(<-ch)
fmt.Println(<-ch)
```
- Позволяют писать в себя без блокировок
- Одновременно в канале могут находиться столько элементов, сколько задали при объявлении канала. **НО** можно прочитать канал и продолжить запись в него


# Select

```go
ch1 := make(chan string)
ch2 := make(chan string)

go func() {
	for {
		time.Sleep(500 * time.Millisecond)
		ch1 <- "Прошло пол секунды"
	}
}()

go func() {
	for {
		time.Sleep(2000 * time.Millisecond)
		ch2 <- "Прошло 2 секунды"
	}
}()

for {
	select {
	case msg := <-ch1:
		fmt.Println(msg)
	case msg := <-ch2:
		fmt.Println(msg)
	default:
		fmt.Println("Нисколько не прошло")
		time.Sleep(1 * time.Millisecond)
	}
}
```
- Позволяет производить неблокирующее чтение из нескольких каналов
- `default` - то же самое что и в [[if-else, switch-case#Switch-case|switch/case]]

