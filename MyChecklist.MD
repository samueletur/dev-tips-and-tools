## Prevent LazyLoading
```php
class AppServiceProvider extends ServiceProvider
{
  public function boot()
  {
    Model::preventLazyLoading(App::isLocal());
    Model::shouldBeStrict(App::isLocal());
  }
}
```

