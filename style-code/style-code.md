---
name: style-code
description: Defines code style conventions for the project. Always apply these rules when writing any PHP code. Trigger on any code generation task.
---

# Code Style

## Context
Functional style and Laravel helpers keep code expressive, readable and consistent — fewer intermediate variables, clearer intent.

## Conventions

- `declare(strict_types=1)` mandatory in all files
- Strict typing everywhere
- Functional style — chain calls, no unnecessary intermediate variables
- `Arr::` instead of `array_*`
- `Str::` instead of `str_*`
- `collect()` instead of manipulating arrays manually
- Laravel facades instead of global PHP functions

## Do ✅ / Don't ❌

```php
// ✅ chained
return User::active()
    ->get()
    ->filter(fn($u) => $u->verified)
    ->map(fn($u) => $u->name);

// ❌ intermediate variables
$users = User::active()->get();
$filtered = $users->filter(fn($u) => $u->verified);
$mapped = $filtered->map(fn($u) => $u->name);
return $mapped;

// ✅ Laravel helpers
Arr::map($items, fn($i) => $i->name);
Str::slug($title);
collect($items)->pluck('name');

// ❌ native PHP functions
array_map(fn($i) => $i->name, $items);
str_replace(' ', '-', strtolower($title));
```
