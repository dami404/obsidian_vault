## If-else
### Пример 1:

```go
if name == "" {
	return name, errors.New("empty name") 
} else if name =="Bob"{ 
	return "Goofy", nil 
}else{ 
	return name, nil 
} 
```
- `} else{` - обязательный **формат**
- Условие может быть в скобках

### Пример 2:

```go
if bool1, b1err := strconv.ParseBool(val1); b1err == nil{ 
	fmt.Println("Parsed value:", bool1) 
} else { 
	fmt.Println("Cannot parse", val1) 
}
```
-  **Формат**: `if оператор инициализации ; выражение`

## Switch-case

```go
day := 4 
switch day { 
	case 1: 
		fmt.Println("Monday") 
		fallthrough // перейти к некст кейсу 
	case 2: 
		fmt.Println("Tuesday") 
	case 3,4,5,6,7: 
		fmt.Println("Others") 
	default: 
		fmt.Println("Not a weekday") 
}
```
- `fallthrough` - перейти к следующему кейсу
- `default` - если ни один из кейсов не сработал
- Если у `switch` не указывать аргумент, это будет лаконичным аналогом `if-else``