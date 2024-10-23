## Способы объявления

```go
var a = make(map[string]string)                            // 1
b := make(map[string]int)                                  // 2
var a = map[string]string{"brand": "Ford", "year": "1964"} // 3 
b := map[string]int{"Oslo": 1, "Bergen": 2,}               // 4
```
- **1** - без инициализации
- **2** - shorthand без инициализации
- **3** - с инициализацией
- **4** - shorthand с инициализацией
- **Формат** - `map[тип данных ключа]тип данных значения`
- Хранится в памяти не как при инициализации, а наиболее эффективно

## Заполнение

```go
a["brand"] = "Ford"
```
-  **Дефолтные значения элементов** без инициализации - nil

## Удаление

```go
delete(a,"year")
```
- **Формат** - `delete(map,ключ)`

## Длина
```go
len(s)
```
-  **Длина map** - динамическая
- `len()` - длина map
## Цикл по map в заданном порядке

```go
a := map[string]int{"one": 1, "two": 2, "three": 3, "four": 4} 
var b []string // defining the order 
b = append(b, "one", "two", "three", "four") 
for _, element := range b { // loop with the defined order 
	fmt.Printf("%v : %v, ", element, a[element]) 
}
```
- Чтобы пройти циклом по map в заданном порядке, нужно ввести отдельную структуру данных