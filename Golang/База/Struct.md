## Объявление

```go
type Vertex struct {
	X int
	Y int
}
```
- Структура - это коллекция полей
- **Формат** - `type название stuct {поле тип данных}`

## Заполнение

```go
v := Vertex{1, 2}
v.X = 4

dog := struct {
	name   string
	isGood bool
}{
	"Rex",
	true,
}

```
- **Формат** - `переменная := имя структуры{значение поля}`
- Для доступа к полям структуры используется точка
- Можно сразу объявить и заполнить структуру

## Указатели

```go
v := Vertex{1, 2}
p := &v
p.X = 1e9
```
- Поля структуры могут быть доступны через [[Указатели|указатели]]
- `(*p).X` = `p.X`

## [[Функции]]

``` go
type person struct {
    name string
    age  int
}

func newPerson(name string) *person {
	p := person{name: name}
	p.age = 42
	return &p
}

func main(){
    fmt.Println(newPerson("Jon")) // &{Jon 42}
}
```
- Функция может возвращать структуру