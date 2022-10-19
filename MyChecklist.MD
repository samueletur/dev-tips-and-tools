## Prevent LazyLoading
AppServiceProvider::boot()
```php
Model::preventLazyLoading(! app()->isProduction());
```

