## Трех компонентный луп

```go
sum := 0
for i := 1; i < 5; i++ {
	sum += i
}
fmt.Println(sum) // 10 (1+2+3+4)
```
- Шаблон: `начальное значение` ; `условие остановки` ; `пост-оператор`

## While

``` go
n := 1
for n < 5 {
	n *= 2
}
fmt.Println(n) // 8 (1*2*2*2)
```

## Бесконечный цикл

``` go
sum := 0
for {
	sum++ // повторяется вечно
}
fmt.Println(sum) // никогда не достигнет
```

## For-each

``` go
a := []string{"Foo", "Bar"}
for i, s := range a {
	fmt.Println(i, s)
}
```
**Result:**
``` 
0 Foo
1 Bar
```
- Проходит по элементам слайса, массива, мапы
- `i` - порядковый номер (ключ для мапы)
- `s` - значение
- Для пустого слайса кол-во итераций - 0

## Выход из цикла

``` go
sum := 0
for i := 1; i < 5; i++ {
	if i%2 != 0 { // skip odd numbers
		continue
	}
	if i%3 != 0 { // skip odd numbers
		break
	}
	sum += i
}
```
- `continue` начинает следующую итерацию. То же самое, что `i++`
- `break` выходит из `for`, `switch`, `select`