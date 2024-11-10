
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
fmt.Println(<-ch)
```
- Позволяют писать в себя без блокировок