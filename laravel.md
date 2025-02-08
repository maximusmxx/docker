
## Helpers

Create new helper: `app/Helpers/helpers.php` 
```php
if (! function_exists('mySum')) {
    function mySum($a, $b)
    {
        return $a + $b;
    }
}
```

Change `composer.json`
```json
{
  "autoload": {
    "files": [
      "app/Helpers/helpers.php"
    ]
  }
}
```

Run bash command
```bash
composer dump-autoload
```
---





