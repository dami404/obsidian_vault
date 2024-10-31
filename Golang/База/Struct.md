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

## Теги

```go
type Config struct {	
	Env         string `yaml:"env" env-default:"local"` // struct tags
	StoragePath string `yaml:"storage_path" env-required:"true"`
	HTTPServer  struct {
		Address     string        `yaml:"address" env-default:"localhost:8082"`
		Timeout     time.Duration `yaml:"timeout" env-default:"4s"`
		IdleTimeout time.Duration `yaml:"idle_timeout" env-default:"60s"`
	} `yaml:"http_server"`
}
```
- Тег для поля позволяет прикрепить к нему метаинформацию, которую можно получить с помощью пакета `reflection`
- **Формат** - `` `тег:значение` ``
- Можно использовать свои теги
### Примеры:

| Тег                         | Пакет                                                                                                                                  | Документация / Примеры                                                                                                                               |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`json`](../Мастеринг/JSON) | [`encoding/json`](https://golang.org/pkg/encoding/json/)                                                                               | [`json.Marshal()`](https://golang.org/pkg/encoding/json/#Marshal)                                                                                    |
| `xml`                       | [`encoding/xml`](https://golang.org/pkg/encoding/xml/)                                                                                 | [`xml.Marshal()`](https://golang.org/pkg/encoding/xml/#Marshal)                                                                                      |
| `bson`                      | [gobson](https://labix.org/gobson) \| [mongo-go](https://github.com/mongodb/mongo-go-driver)                                           | [`bson.Marshal()`](http://godoc.org/gopkg.in/mgo.v2/bson#Marshal) \| [bson package](https://pkg.go.dev/go.mongodb.org/mongo-driver/bson#hdr-Structs) |
| `protobuf`                  | [`github.com/golang/protobuf/proto`](http://godoc.org/github.com/golang/protobuf/proto)                                                |                                                                                                                                                      |
| `yaml`                      | [`gopkg.in/yaml.v2`](https://godoc.org/gopkg.in/yaml.v2)                                                                               | [`yaml.Marshal()`](https://godoc.org/gopkg.in/yaml.v2#Marshal)                                                                                       |
| `db`                        | [`github.com/jmoiron/sqlx`](https://godoc.org/github.com/jmoiron/sqlx) \| [`github.com/go-gorp/gorp`](https://github.com/go-gorp/gorp) |                                                                                                                                                      |
| `orm`                       | [`github.com/astaxie/beego/orm`](https://godoc.org/github.com/astaxie/beego/orm)                                                       | [Models – Beego ORM](https://beego.me/docs/mvc/model/overview.md)                                                                                    |
| [`gorm`](../ORMs/GORM)      | [`gorm.io/gorm`](https://gorm.io/)                                                                                                     | [docs](https://gorm.io/docs/)                                                                                                                        |
| `valid`                     | [`github.com/asaskevich/govalidator`](https://github.com/asaskevich/govalidator)                                                       | [Examples](https://github.com/asaskevich/govalidator)                                                                                                |
| `datastore`                 | [`appengine/datastore`](https://cloud.google.com/appengine/docs/go/datastore/reference)                                                | [Properties](https://cloud.google.com/appengine/docs/go/datastore/reference#hdr-Properties)                                                          |
| `schema`                    | [`github.com/gorilla/schema`](http://godoc.org/github.com/gorilla/schema)                                                              |                                                                                                                                                      |
| `asn1`                      | [`encoding/asn1`](https://golang.org/pkg/encoding/asn1/)                                                                               | [`asn1.Marshal()`](https://golang.org/pkg/encoding/asn1/#Marshal) \| [`asn1.Unmarshal()`](https://golang.org/pkg/encoding/asn1/#Unmarshal)           |
| `csv`                       | [`github.com/gocarina/gocsv`](https://github.com/gocarina/gocsv)                                                                       |                                                                                                                                                      |
| `env`                       | [`github.com/caarlos0/env`](https://github.com/caarlos0/env)                                                                           |                                                                                                                                                      |


## [[Указатели]]

```go
type Vertex struct {
	X int
	Y int
}

func main() {
	v := Vertex{1, 2}
	p := &v
	p.X = 1e9
	fmt.Println(v)
}

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


## [[Generics]]

```go
type List[T any] struct {
	next *List[T]
	val  T
}
```
- Можно так же создавать кастомные [[Новые структуры данных|структуры данных]]