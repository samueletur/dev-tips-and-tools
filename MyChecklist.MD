## Prevent LazyLoading
```php
class AppServiceProvider extends ServiceProvider
{
  public function boot()
  {
    Model::shouldBeStrict(App::isLocal());
  }
}
```

