---
name: pipe
description: 'Generates a Laravel Pipe following project conventions. Trigger on: "create a pipe", "new pipe", "pipe for {Entity}", "add a step", "add a pipeline step". Always use this skill for any Pipe creation or modification.'
---

# Pipe

## Context
The Pipe is an atomic step in the Pipeline — it has a single responsibility, enriches the DTO, can save to DB or cache, and passes control to the next step. All business logic lives here.

## Conventions

- `__invoke` — always returns `mixed`
- Single responsibility — one concern per Pipe
- Always call `$next($dto)` to pass to the next step
- Enriches the DTO via its mutable properties
- Can save to DB or cache
- Naming centered on data:
  - `Store{Entity}Pipe` → save to DB
  - `Create{Entity}Pipe` → external creation/third-party API
  - `Retrieve{Entity}Pipe` → data retrieval
- Location → `app/Pipes/{Resource}/`
- Unit test mandatory — 100% coverage → `tests/Unit/Pipes/{Resource}/`

## Do ✅ / Don't ❌

```php
// ✅ single responsibility — store
public function __invoke(StoreItemDto $dto, Closure $next): mixed
{
    $dto->item = Item::create([
        'name' => $dto->name,
    ]);
    return $next($dto);
}

// ✅ retrieve
public function __invoke(StoreItemDto $dto, Closure $next): mixed
{
    $dto->item = Item::whereItemId($dto->item_id)->firstOrFail();
    return $next($dto);
}

// ✅ external API
public function __invoke(StoreItemDto $dto, Closure $next): mixed
{
    $dto->payment = Stripe::create($dto->amount);
    return $next($dto);
}

// ❌ multiple responsibilities in one Pipe
public function __invoke(StoreItemDto $dto, Closure $next): mixed
{
    $dto->item = Item::create(['name' => $dto->name]);
    Mail::to($dto->email)->send(new WelcomeMail());
    Cache::put('item', $dto->item);
    return $next($dto);
}

// ❌ missing $next
public function __invoke(StoreItemDto $dto, Closure $next): mixed
{
    $dto->item = Item::create(['name' => $dto->name]);
    // missing return $next($dto);
}

// ❌ wrong return type
public function __invoke(StoreItemDto $dto, Closure $next): StoreItemDto
{
    return $next($dto);
}
```
