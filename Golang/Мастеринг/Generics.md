## [[Функции]]

```go
func Index[T comparable](s []T, x T) int {
	for i, v := range s {
		// v and x are type T, which has the comparable
		// constraint, so we can use == here.
		if v == x {
			return i
		}
	}
	return -1
}

func main() {
	// Index works on a slice of ints
	si := []int{10, 20, 15, -10}
	fmt.Println(Index(si, 15))

	// Index also works on a slice of strings
	ss := []string{"foo", "bar", "baz"}
	fmt.Println(Index(ss, "hello"))
}
```
- С помощью дженериков (`type parameters`) функции могут работать с разными типами данных

## [[Struct|Структуры]]

```go
type List[T any] struct {
	next *List[T]
	val  T
}
```
- Можно так же создавать кастомные [[Новые структуры данных|структуры данных]]