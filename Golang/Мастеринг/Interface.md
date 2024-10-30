## Реализация интерфейса
```go
type geometry interface {
    area() float64
    perim() float64
}

type rect struct {
    width, height float64
}

type circle struct {
    radius float64
}

func (r *rect) area() float64 {
    return r.width * r.height
}

func (r *rect) perim() float64 {
    return 2*r.width + 2*r.height
}

func (c *circle) area() float64 {
    return math.Pi * c.radius * c.radius
}

func (c *circle) perim() float64 {
    return 2 * math.Pi * c.radius
}

func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}
  
func main() {
    r := rect{width: 3, height: 4}
    c := circle{radius: 5}
    measure(&r)
    measure(&c)
}
```
- **Интерфейс** - это набор сигнатур методов
- Чтобы реализовать интерфейс, надо реализовать все его методы
- Если переменная имеет тип интерфейса(`geometry`), то мы можем вызывать методы, которые находятся в именованном интерфейсе. См. универсальную функцию `measure`
- Если структуры реализуют интерфейс, то можно использовать ее экземпляры в универсальной функции или использовать методы интерфейса - `экземпляр.метод()`
## Пустой интерфейс

```go
func main() {
	var i interface{}
	describe(i)

	i = 42
	describe(i)

	i = "hello"
	describe(i)
}

func describe(i interface{}) {
	fmt.Printf("(%v, %T)\n", i, i)
}
```
- Интерфейс, который не представляет ни одного метода - **пустой**
- Пустой интерфейс может содержать любой тип