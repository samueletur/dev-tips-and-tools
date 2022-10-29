## Prevent LazyLoading
```php
class AppServiceProvider extends ServiceProvider
{
  public function boot()
  {
    Model::shouldBeStrict(App::isLocal());
    Model::preventAccessingMissingAttributes(App::isLocal());
  }
}
```
## Long database queries  
```php
use Illuminate\Support\Facades\DB;

public function boot()
{
    // Log a warning if we spend more than a total of 2000ms querying.
    DB::whenQueryingForLongerThan(2000, function (Connection $connection) {
        Log::warning("Database queries exceeded 2 seconds on {$connection->getName()}");
    });
}

// If you want to run a callback when a single query takes a long time, you can do that with a DB::listen callback.

use Illuminate\Support\Facades\DB;

public function boot()
{
    // Log a warning if we spend more than 1000ms on a single query.
    DB::listen(function ($query) {
        if ($query->time > 1000) {
            Log::warning("An individual database query exceeded 1 second.", [
                'sql' => $query->sql
            ]);
        }
    });
}

// Request and command lifecycle

use Illuminate\Contracts\Http\Kernel as HttpKernel;
use Illuminate\Contracts\Console\Kernel as ConsoleKernel;

public function boot()
{
    if ($this->app->runningInConsole()) {
        // Log slow commands.
        $this->app[ConsoleKernel::class]->whenCommandLifecycleIsLongerThan(
            5000,
            function ($startedAt, $input, $status) {
                Log::warning("A command took longer than 5 seconds.");
            }
        );
    } else {
        // Log slow requests.
        $this->app[HttpKernel::class]->whenRequestLifecycleIsLongerThan(
            5000,
            function ($startedAt, $request, $response) {
                Log::warning("A request took longer than 5 seconds.");
            }
        );
    }
}
```

