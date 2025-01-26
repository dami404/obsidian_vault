- Нужен для завершения [горутин](obsidian://open?vault=obsidian_vault&file=Golang%2F%D0%91%D0%B0%D0%B7%D0%B0%2FGoroutines)

## ==Когда использовать?==

1) Завершение операции, выполняющуюся слишком долго
2) Работа с сетью

## Таймаут | Дедлайн

```go
    ctx, cancel := context.WithTimeout(context.Background(), 15*time.Second)
//	ctx,cancel := context.WithDeadline (context.Background(),                
//										time.Now().Add(15*time.Second))
    defer cancel()

    req, err := http.NewRequestWithContext(ctx, http.MethodGet, "https:/...", nil)
    if err != nil {
        return nil, fmt.Errorf("failed to create requset with ctx: %w", err)
    }

    res, err := http.DefaultClient.Do(req)
    if err != nil {
        fmt.Errorf("failed to perform http request: %w", err)
    }
    return res,nil
```
- `context.Background()` - контекст верхнего уровня
- Контекст определяется в начале функции

## Отмена

```go
ctx := context.WithCancel(context.Background())
...
ctx.Done()
```
- `.Done()` завершает контекст