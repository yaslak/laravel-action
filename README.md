# yaslak/laravel-action

A collection of AI agent skills for Laravel developers following the **DTO → Pipe → Action → Resource → Controller** architecture pattern.

## Skills

| Skill | Description |
|-------|-------------|
| `action` | Orchestrates business flow via a Pipeline of Pipes |
| `cast` | Eloquent custom cast classes |
| `controller` | Single-action and resource controllers |
| `dto` | Data Transfer Objects with typed properties |
| `enum` | PHP 8.1+ backed enums |
| `event` | Laravel events and listeners |
| `exception` | Custom exception classes |
| `factory` | Eloquent model factories |
| `form-request` | Validation via Form Requests |
| `listener` | Event listeners |
| `logs` | Logging conventions |
| `migration` | Database migrations |
| `model` | Eloquent models |
| `pipe` | Pipeline pipes for business logic |
| `policy` | Authorization policies |
| `resource` | API resources |
| `response` | HTTP response conventions |
| `routes` | Route definitions |
| `service-provider` | Service providers |
| `style-code` | Code style conventions |
| `support` | Support classes and helpers |
| `test` | Testing conventions with Pest |

## Installation
```bash
php artisan boost:add-skill yaslak/laravel-action --all
```

## Usage

Skills are activated on-demand by your AI agent (Claude Code, Cursor, etc.) when working on related tasks. No manual invocation needed.