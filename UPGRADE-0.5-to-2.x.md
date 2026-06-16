# Upgrading from 0.5.x to 2.x

Version `2.0.0` replaces the legacy `0.5.x` line for Laravel 9 and newer.

## Composer constraints

```json
// Laravel 6–8 (no change):
"curbngo/jwt-auth": "0.5.22"

// Laravel 9+:
"curbngo/jwt-auth": "^2.0"
```

## Breaking changes

| Legacy (0.5.x) | Modern (2.x) |
|---|---|
| `JWTAuthServiceProvider` manual registration | Auto-discovery via `extra.laravel` |
| `jwt:generate` | `jwt:secret` |
| `NamshiAdapter` | Lcobucci provider |
| Middleware: `GetUserFromToken`, `RefreshToken` | `jwt.auth`, `jwt.refresh` aliases |
| `App\User` default in config | `App\Models\User` |
| Custom middleware auth | `'driver' => 'jwt'` guard in `config/auth.php` |
| `namshi/jose` | `lcobucci/jwt` (requires `ext-sodium` for lcobucci 5.x) |

## Installation (Laravel 9+)

```bash
composer require curbngo/jwt-auth:^2.0
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
php artisan jwt:secret
```

Configure the API guard in `config/auth.php`:

```php
'guards' => [
    'api' => [
        'driver' => 'jwt',
        'provider' => 'users',
    ],
],
```

## Middleware (Laravel 11+)

Register in `bootstrap/app.php`:

```php
->withMiddleware(function (Middleware $middleware) {
    $middleware->alias([
        'jwt.auth' => \Tymon\JWTAuth\Http\Middleware\Authenticate::class,
        'jwt.refresh' => \Tymon\JWTAuth\Http\Middleware\RefreshToken::class,
    ]);
})
```

## Requirements

- PHP `^8.0` (Laravel 11+ requires PHP 8.2+, Laravel 13 requires PHP 8.3+)
- `ext-json`
- `ext-sodium` when using `lcobucci/jwt` 5.x
