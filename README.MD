# GIT

[Git commands and their explanations](#git-commands)

[Git clone specific branch](#git-clone-specific-branch)

# Images

[Using Picture](#using-picture)

[Using Srcset](#using-srcset)

# LIVEWIRE

[Livewire Redirect](#livewire-redirect)

# MAC

[Create fake file size](#create-fake-file-size) 

# MYSQL

[Delete billions of rows](#delete-billions-of-rows)

[Set Timezone](#set-timezone)

# NGROK
[Ngrok Getting Started](#ngrok-getting-started)
# PHP

[isset](#isset)

[Helpers checks bugs](#helpers-checks-bugs)
# Laravel

## Auth

[Breeze](#breeze)

[Login - Event](#login-event)

## Collection

[Arr::dot](#arr-dot)

[Arr::join](#arr-join)

[Collection tips](#collection-tips)
## Eloquent

[after](#after)

[allRelatedIds](#allRelatedIds)

[Custom Casts](#custom-casts)

[Composite Indexes](#composite-indexes)

[find](#find)

[GroupBy](#groupby)

[insertGetId](#insertGetId)

[Invisible Database Columns](#invisible-database-columns)

[isDirty and isClean](#isDirty-and-isClean)

[Lazy Loading](#lazi-loading)

[Model Keys](#model-keys)

[Push](#push)

[Query Casting](#query-casting)

[Random Order](#random-order)

[Relationships - Default](#relationship-default)

[Relationships - Querying existence of relationships](#relationships-querying-existence) `#mysql` `#whereHas` `#has` `#relationship`

[Relationships - Query filter](#relationships---query-filter)

[Relationships - Eager loading](#relationships---eager-loading)

[Routing - Parameters regular expression constraint](#routing-parameters-regular-expression-constraint) `#route`

[Routing - Global route pattern](#routing-global-route-pattern) `#route`

[SelectRaw](#selectraw) `#mysql` `#selectRaw` `#query`

[Sensitive Data](#sensitive-data) `#crypt` `#cast` `#attribute`

[Value](#value)

[wasChanged](#wasChanged)

[when for conditionally situations](#when-for-conditionally-situations) `#when`

[whereBelongsTo](#whereBelongsTo)

[whereBetween with dates](#wherebetween-with-dates) use whereBetween with a range date. If you need to provide fallback you can do so with the nullish coalescing operator ?? `#whereBetween` `#date`

[whereColumn](#wherecolumn)

[whereDate](#wheredate)

[whereIn](#whereIn)

[with - cheatsheet](#with---cheat-sheet) #with #without

[withCount](#withcount) #with #withCount

## Form Request

[Add Values to the form after validation](#add-values-to-the-form-after-validation)

## General

[Namespaces](#namespaces)

## Logs
[Query Log](#query-log)

## Migrate

[Migrate After](#migrate-after)
## Misc

[Laravel Pint](#laravel-pint)

[Str Plural](#str-plural)

[Config values on the fly](#config-values-on-the-fly)

## Route

[Generate csv from route list](#generate-csv-from-route-list)

[URI fragment](#uri-fragment)

[Redirect](#redirect)

[Resources Group](#resources-group)


## Storage

[Cheatsheet](#storage-cheatsheet)

## URL

[Url Facade](#url-facade)

### **Git commands**  

```php
git init // It is used for initializing a Git repository 
git clone <url> // Used to clone the repository from remote
git add <file-name> // Add a file in to the staging
git add . // Add all files in the staging 
git add -A  // Add new files to the staging
git commit -m "message" // Commit the changes
git rm -r file.html // Removes a file
git branch // lists are the branches
git status // Checking the status
git branch -a // List all the local and remote branches
git config --global --list // Get global config 
git revert commit_id // Revert the changes for a commit using id
git log // View the changes
git pull // Pull the changes from remote to local
git push // Push the changes from local to remote
git branch branch_name // Create a new branch
git branch -d branch_name // Delete a branch
git checkout branch_name // Switch to a branch
git checkout -b branch_name // Create a new branch with the given name and immediately switch to it
git checkout -- file.html // Discard changes from a file
git stash // Stash the changes
git stash clear // Discard all the stashes
git remote add origin URL // Add a remote repository
git branch -m old_branch_name new_branch_name
git checkout -  // Switch to the branch last checked out
git log --summary // View changes with details
```

[🔝 Back to git](#git)

### **Git clone specific branch**  

```php
 git clone -b <branch> git@github.com:BolajiAyodeji/nextjs-blog.git <directory>
```

[🔝 Back to git](#git)

### **Using picture**

```php
// Reference: https://sendy.daily-dev-tips.com/w/PxB892JyyvFQAG3r0BENjd7g/u1EYAy4ATBwEDYLJQ8o84g/t8N763Qt5c2zcUziLCeqWpaQ
<picture>
  <source
    media="(max-width: 767px)"
    width="96"
    height="96"
    srcset="img-mobile.jpg, img-mobile@2x.jpg 2x"
  />
  <source
    media="(min-width: 768px)"
    width="368"
    height="193"
    srcset="img-desktop.jpg, img-desktop@2x 2x, img-desktop@3x 3x"
  />
  <img src="img-desktop.jpg" width="368" height="193" />
</picture>
```

[🔝 Back to img](#images)

### **Using srcset**

```php
// Reference: https://sendy.daily-dev-tips.com/w/PxB892JyyvFQAG3r0BENjd7g/u1EYAy4ATBwEDYLJQ8o84g/t8N763Qt5c2zcUziLCeqWpaQ
<img
  srcset="img-small.jpg 480w, img-large.jpg 1080w"
  sizes="(max-width: 480px) 100vw, (max-width: 1024px) 50vw, 800px"
/>
```

[🔝 Back to img](#images)

### **Create fake file size**

```php
// MacOs snippet to fake a 10MB PDF file
mkfile 10m testfile.pdf
```

[🔝 Back to mac](#mac)

### **Livewire Redirect**

Tip: All (non-initial) Livewire requests store the original route in the Referer header.

So even though Livewire doesn't support redirect()->back(), you can do this and it works perfectly.

```php
return redirect(request()->header('Referer'));
```

[🔝 Back to livewire](#livewire)
```

[🔝 Back to mac](#mac)

### **Delete billions of rows**

```php
// instead of
DELETE FROM user_activities WHERE year = 2020;

// you can use
ALTER TABLE user_activities DROP PARTITION user_activities_2019_q01, ..., user_activities_2019_q04; 
```

[🔝 Back to Mysql](#mysql)
### **Set timezone**

[Support timezones](https://www.php.net/manual/en/timezones.php) 
 
```php
SET time_zone = "America/Sao_Paulo";

```

[🔝 Back to Mysql](#mysql)

### **isset**

```php
// instead of
if(isset($value) && isset($value2) && isset($value3))

// you can use
if(isset($value,$value2,$value3))
```

[🔝 Back to php](#php)

### **ngrok getting started**

Share development environment with others  
[Site](https://ngrok.com)
```php
// Install, configure and run ngrok
// Download package and extract it
// Mac users: mv ~/Downloads/ngrok /usr/local/bin
// ngrok config add-authtoken <token>
// Authtoken saved to configuration file: /Users/samueletur/Library/Application Support/ngrok/ngrok.yml
// Publish your local web server to the internet
// php artisan serve && ngrok http http://127.0.0.1:8000
```

[🔝 Back to ngrok](#ngrok)

### **helpers-checks-bugs**

[PHP CS Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)
// This tool will help you by keeping the style of your code consistent for you and your team. You can easily configure it to fit yours and your team's rules. Also, run this as part of your continous integration workflow.

[PHPStan](https://github.com/phpstan/phpstan)
// This tool will analyze your code and find potential issues in your code based on the rules you set for you and your team. You can create custom rules and test them as well. Also, run this as part of your continous integration workflow.

[Arkitect](https://github.com/phparkitect/arkitect)
// This tool will help you keep your folder and namespace architecture constistent for you and your team. You can customize it based on your project structure. Also, run this as part of your continous integration workflow.

[Infection](https://github.com/infection/infection)
// This tool will add an additional layer of scenarios for your automated tests to see if your code is written properly.    Also, run this as part of your continous integration workflow.

[Deptrac](https://github.com/qossmic/deptrac)
// Deptrac is a static code analysis tool for PHP that helps you communicate, visualize and enforce architectural decisions in your projects. Also, run this as part of your continous integration workflow.

[Rector](https://github.com/rectorphp/rector)
// This tool will help you refactor your code as well as upgrade your codebase from time to time to keep up with the latest PHP, tools, packages and framework updates.

[🔝 Back to php](#php)

### **breeze**

An alternative to pluck('id'') to get all of the IDs for the related models.

```php
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
php artisan migrate

// Breeze Vue
php artisan breeze:install vue
npm install && npm dev
php artisan migrate
```

[🔝 Back to eloquent](#eloquent)

### **Login Event**

Closure-based login event listener

```php
namespace App\Providers;

use Illuminate\Support\Facades\Event;
use Illuminate\Foundation\Support\Providers\EventServiceProvider as ServiceProvider;

class EventServiceProvider extends ServiceProvider
{
    protected $listen = [];

    public function boot()
    {
        parent::boot();

        Event::listen('Illuminate\Auth\Events\Login', function() {
            logger('login ...');
        });

    }
}
```

[🔝 Back to collection](#collection)

### **Arr Dot**

```php
use illuminate\SupportArr;

$arr  = [
    'rede_sociais' => [
        'youtube' => 'youtube.com'
    ]
];

Arr::dot($arr);

// rede_sociais.youtube: youtube.com
```

[🔝 Back to collection](#collection)

### **Arr Join**

Similar to `Collection::join`, you can `Arr::join` to return the new string by concatenating all of the elements in an array

```php
use illuminate\SupportArr;

$arr  = ['Batman', 'Superman', 'Spider', 'Aquaman'];

Arr::join($arr, ', ', ' and ');

// Batman, Spuperman, Spider and Aquaman
```

[🔝 Back to collection](#collection)

### **Collection Tips**

Tip: Instead of manipulating data with lots of procedural PHP methods, consider refactoring to  collections. They allow for beautiful code chains that are so much easier to understand

```php
/**
 * Much of the time, our code is responsible for walking through data 
 * and filtering / formatting it. Instead of writing lots of procedural 
 * steps using plain PHP, consider refactoring to collections. It's a 
 * greate way to clean things up and write less code overall.
 */

$data = [
    'name' => 'orange', 'citrus' => true,
    'name' => 'lemon', 'citrus' => true,
    'name' => 'apple', 'citrus' => false,
];

// Before
$data = array_filter($data, function($item) {
    return $item['citrus'];
});

array_walk($data, function(&$item) {
    $item = ucfirst($item['name']);
});

$sort($data);

return array_values($data); // ['Lemon', 'Orange']

// After

return collect($data)
    ->filter(fn($item) => $item['citrus'])
    ->map(fn($item) => ucfirst($item['name']))
    ->sort()   
    ->values()
    ->toArray();
```

[🔝 Back to collection](#collection)

### **allRelatedIds**

An alternative to pluck('id'') to get all of the IDs for the related models.

```php
// instead of
$article->tags()->pluck('id')->toArray();

// you can use
$article->tags()->allRelatedIds()->toArray();
```

[🔝 Back to eloquent](#eloquent)

### **Custom Casts**

Tip: You can create custom casts to have Laravel automatically format your Eloquent model data. Here's an example that capitalises a user's name when it is retrieved or changed.

```php
namespace App\Casts;

use Illuminate\Contracts\Database\Eloquent\CastsAttributes;

class CapitalizeWordsCast implements CastsAttributes
{
    public function get($model, $key, $value, $attributes)
    {
        return ucwords($value);
    }

    public function set($model, $key, $value, $attributes)
    {
        return ucwords($value);
    }
}

class User extends Model 
{
    protected $casts = [
        'name' => CapitalizeWordsCast::class,
        'email' => 'string',
    ];
}
```

[🔝 Back to eloquent](#eloquent)

### **Composite Indexes**

Tip: Database indexes can really help to speed up queries, but applying them arbitrarily to many columns can make things worse. Instead, if you’re querying across multiple columns, use a composite index. Here’s how

```php

class CreateInvitationsTable extends Migration {
    Schema::create('invitations', function (Blueprint $table) {
        $table->increments('id');
        // Before
        $table->string('organization_id')->index();
        $table->string('vacancy_id')->index();
        $table->string('user_id')->index();

        // After
        $table->string('organization_id');
        $table->string('vacancy_id');
        $table->string('user_id');

        $table->index(['organization_id','vacancy_id','user_id']);
    });
}
```

[🔝 Back to eloquent](#eloquent)

### **find**

AThe `find` method accepts an array of ids to retrieve many records based on IDs.

```php
// instead of this
$users = $user->whereIn('id',$ids)->get();

// you can use
$users = $user->find($ids);

// Or you can use findMany
$users = $user->findMany($ids,['name','email']);
```

[🔝 Back to eloquent](#eloquent)

### **GroupBy**

```php
// instead of this
$years = Post::query()
    ->with('user')
    ->latest('created_at')
    ->get()
    ->groupBy(fn($post)=>$post->created_at->year);

return view('posts', ['years'=>$years]);

// in your view
@foreach($years as $year => $posts)
<h3>{{ $year }}</h3>
    @foreach($posts as $post)
        <p>{{ $post->title }}</p>
    @endforeach
@endforeach

```

[🔝 Back to eloquent](#eloquent)

### **Invisible database columns**

The invisible column is a new concept in MySQL 8. What it does: when you run a select * query it won't retrieve any invisible column. If you need an invisible column's value you have to specify it explicitly in the select statement.

It's a very useful concept for sensitive information such as:

Password
Tokens
API keys
Payment-related information

And now, Laravel supports these columns:

```php
Schema::table('users', function (Blueprint $table) {
  $table->string('password')->invisible();
});

$user = User::first();
$user->secret === null;

// This query will return null despite the fact that it's a select * query.
// It's because password is invisible.
// If you need the password you need to run this query:

$user = User::select('password')->first();
$user->password !== null;
```

[🔝 Back to eloquent](#eloquent)

### **insertGetId**

If you want to return the record ID, instead of a boolean value, when you use `insert` query builder method. You can use `insertGetId` instead.

```php
// return boolean
DB::table('users')->insert($data);

// return a integer record ID
DB::table('users')->insertGetId($data);
```

[🔝 Back to eloquent](#eloquent)

### **isDirty-and-isClean**

```php
use App\Models\User;
 
$user = User::create([
    'first_name' => 'Taylor',
    'last_name' => 'Otwell',
    'title' => 'Developer',
]);
 
$user->title = 'Painter';
 
$user->isDirty(); // true
$user->isDirty('title'); // true
$user->isDirty('first_name'); // false
$user->isDirty(['first_name', 'title']); // true
 
$user->isClean(); // false
$user->isClean('title'); // false
$user->isClean('first_name'); // true
$user->isClean(['first_name', 'title']); // false
 
$user->save();
 
$user->isDirty(); // false
$user->isClean(); // true
```

[🔝 Back to eloquent](#eloquent)

### **Model-Keys**

If you need to get an array of ID's from eloquent collection, you would probabally use combination of pluck() and toArray(). You can simplify it by using modelKeys() method

```php
// instead of
Vendor::all()->pluck('id')->toArray();
// you can use
Vendor::all()->modelKeys();
```

[🔝 Back to eloquent](#eloquent)
```

[🔝 Back to eloquent](#eloquent)

### **Lazy-Loading**

Dealing with N+1 queries is probably one of the most common sources of performance issues. Since Laravel 8, you can entirely turn off lazy loading. This means if a relationship is not eager loaded, and you try to access it, Laravel will throw an exception in your face!

```php
class AppServiceProvider extends ServiceProvider
{
  public function boot()
  {
    Model::preventLazyLoading(!app()->isProduction());
  }
}
```

[🔝 Back to eloquent](#eloquent)

### **Push**

Save the product and its relations

```php
$product = Product::find(1);

$product->name = 'New Balance Shoes';
$product->brand->name = 'New Balance'; $product->department->name = 'Men';

// Save the product and its relations
$product->push();
```

[🔝 Back to eloquent](#eloquent)

### **Query Casting**

Add casts to a specific query

```php
$users = User::select([
    'users.*',
    'last_posted_at' => Post::selectRaw('MAX(created_at)')->whereColumn('user_id', 'users.id')
])->withCasts([
    'last_posted_at' => 'datetime',
])->get();
```

[🔝 Back to eloquent](#eloquent)

### **Random Order**

Eloquent has an ‘inRandomOrder()’ method, which is useful for mixing up content or for showing related but different content e.g. blog posts. However, it is VERY SLOW on large tables. Fortunately, we can easily fix it by replacing it with a ‘whereRaw’ filter.

```php

$related = Article::where('tag','PHP')
    ->whereRaw('`articles`.`id` >= FLOOR(1 + RAND() * (SELECT MAX(`id`) FROM `articles`))')
    ->limit(3)
    ->get();

// Instead of this
$related = Article::where('tag','PHP')->inRandomOrder()->limit(5)->get();
```


[🔝 Back to eloquent](#eloquent)

### **Relationship - Default**

Define default models

```php
class Comment extends Model
{
    public function author()
    {
        return $this->belongsTo(User::class)->withDefault([
            'name' => 'Guest'
        ]);
    }
}

// Now in the view, instead of doing this
{{ $comment->author ? $comment->author->name : 'Guest' }}

// Can do this
{{ $comment->author->name }}

```

[🔝 Back to eloquent](#eloquent)

### **Relationships Querying Existence**

Querying existence of relationships when retrieving models in Laravel: 

```php
// Retrieve all posts that have at the least on comment ...
$posts = Post::has('comments')->get();

// Retrieve all posts that have three or more comments ...
$posts = Post::has('comments','>=',3)->get();

// Retrieve all posts that have at least one comment with images ...
$posts = Post::has('comments.images')->get();

// Retrieve posts with at least one comment containing words like code% ...
$posts = Post::whereHas('comments',function(Builder $qry){
    $qry->where('content','like','code%');
})->get();

// Retrieve posts with at least ten comments containing words like code% ...
$posts = Post::whereHas('comments',function(Builder $qry){
    $qry->where('content','like','code%');
}, '>=', '10')->get();

// Alternatively, query with a single, simple where condition attached to the relationship query
$posts = Post::whereRelation('comments', 'is_approved', false)->get();
$posts = Post::whereRelation(
    'comments', 'created_at', '>=', now()->subHour()
)->get();

// Instead of a join
$apple = Holding::select('holdings.*')->leftJoin('stocks', 'stocks.id', 'holdings.stock_id')->where('stocks.ticker', 'AAPL')->get();

// You can do this
$apple = Holding::whereRelation('stock', 'ticker', 'AAPL')->get();

// Querying a relationship absense
$posts = Post::doesntHave('comments')->get();
$posts = Post::whereDoesntHave('comments', function (Builder $qry) {
    $qry->where('content','like','code%');
})->get();

```

[🔝 Back to eloquent](#eloquent)

### **Relationships - Query filter**

If you need to filter a model by a nested relationship and are also eager load 
both of the relationships you can create a closure that takes care of 
the logic and pass it to both `with` and `whereHas`

```php
$filter = function ($query){
    $query->where('year', now()->format('Y'));
};

// Get book from authors that have won awards this year
// and eager load the authors and awards won this year 
$authors = Book::with(['authors.awards' => $filter])
    ->whereHas('authors.awards', $filter)
    ->get();
```

[🔝 Back to eloquent](#eloquent)

### **Relationships - Eager Loading**

Eager loading model relationships is way more efficient, however if used blindly, 
it can result in the fetching of data that you don’t actually need. 
To help avoid this problem, consider adding a constraint to the query

```php
class ListingController {
    public function index() {
        return view('listings.index',[
            'listings' => Listing::with('images')->paginate(20)
        ]);
    }
}

Listing::with([
    'images'=> fn($query) => $query->where('type', 'primary'),
]);
```

[🔝 Back to eloquent](#eloquent)

### **Routing Parameters Regular Expression Constraint**

```php
Route::get('posts/{post}', function() {
    // ...
})->where('post','[A-Za-z]+');

// only letters
->whereAlpha();

//only numbers
->whereNumber();
// Letters e numbers
->onlyAlphaNumeric();

// regular expression with more parameters
Route::get('posts/{id}/{post}', function() {
    // ...
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);    

Route::get('/user/{id}/{name}', function ($id, $name) {
    //
})->whereNumber('id')->whereAlpha('name');    
```

[🔝 Back to eloquent](#eloquent)

### **Routing Global route pattern**

```php
// instead of
Route::get('customers/{id}', [CustommerController::class, 'show'])->where('id', '[0-9]+');
Route::get('vendors/{slug}', [VendorController::class, 'show'])->where('slug', '[a-z0-9-]+');

// you can do
// You can define these patterns in boot method of RouteServiceProvider

public function boot()
{
    Route::pattern('id', '[0-9]+');
    Route::slug('id', '[0-9]+');
}
```

[🔝 Back to eloquent](#eloquent)

### **SelectRaw**

Count and show reviews table using the db server to process

```php
Product::query()
    ->where('product_id',1)
    ->reviews()
    ->selectRaw('
        count(case when rating = 1 then 1 end) as one_star,
        count(case when rating = 2 then 1 end) as two_star,
        count(case when rating = 3 then 1 end) as three_star,
        count(case when rating = 4 then 1 end) as four_star,
        count(case when rating = 5 then 1 end) as five_star,
    ')
    ->first();
```

[🔝 Back to eloquent](#eloquent)

### **Sensitive Data**

If we want to put "sensitive" data in our DB then we can use Crypt Facade and handle these using accessors and mutators.

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Cast\Attribute;
use Illuminate\Support\Facades\Crypt;

class Client extends Model
{
    protected function document(): Attribute
    {
        return Attribute::make(
            set: fn ($value) => Crypt::encryptString($value),
            get: fn ($value) => Crypt::decryptString($value),
        );
    }
}
```

[🔝 Back to eloquent](#eloquent)

### **Value**

There is a 'value' method on the Query Builder which can make your code a lot shorter.

```php
User::where('type',UserTypeEnum::ADMIN)
    ->select('name')
    ->first()
    ->name;

User::where('type',UserTypeEnum::ADMIN)
    ->value('name');
```

[🔝 Back to eloquent](#eloquent)

### **wasChanged**

```php
$user = User::create([
    'first_name' => 'Taylor',
    'last_name' => 'Otwell',
    'title' => 'Developer',
]);
 
$user->title = 'Painter';
 
$user->save();
 
$user->wasChanged(); // true
$user->wasChanged('title'); // true
$user->wasChanged(['title', 'slug']); // true
$user->wasChanged('first_name'); // false
$user->wasChanged(['first_name', 'title']); // true
```

[🔝 Back to eloquent](#eloquent)

### **When for conditionally situations**

For situations where you need to conditionally build up a database query e.g. if published = true, then add a WHERE statement… make use of the ‘when’ method directly on the query builder. It’s great for keeping things neat and chained.

```php

// instead of
$query = Article::query();

if($published)
    $query = $query->where('published',true);

return $query->get();

// you can use
    return Article::query()
        ->when($published, fn($query) => $query->where('published',true))
        ->get();
```

[🔝 Back to eloquent](#eloquent)

### **whereBelongsTo**

Get relationship without use where on query

```php
// instead of
Order::where('user_id',$user->id)->sum('total_amount');

// you can use
Order::whereBelongsTo($user)->sum('total_amount');

// instead of
Post::where('user_id',$author->id)->where('category_id',$category->id)->first();
// you can use
Post::whereBelongsTo($author)->whereBelongsTo($category)->first();
```

[🔝 Back to eloquent](#eloquent)

### **wherebetween with dates**

How to retrieve records between two timestamps in Laravel 🗓  Use whereBetween with a from and to date. If you need to provide fallback you can do so with the nullish coalescing operator

```php
Post::whereBetween('publish_at', [
    $request->from ?? '1970-01-01',
    $request->to ?? today()->toDateTimeString()
])->get();
```

[🔝 Back to eloquent](#eloquent)

### **whereColumn**

Eloquent tip for comparing database columns to each other within a query

```php
Post::whereColumn('created_at','updated_at');

Post::whereColumn('created_at','updated_at')
    ->whereColumn('author_id','<','editor_id')

Post::whereColumn('created_at','updated_at')
    ->whereColumn('author_id','<','editor_id', 'or')
```

[🔝 Back to eloquent](#eloquent)
### **whereDate**

Tip: Eloquent’s ‘whereDate’ function is useful, but it prevents the database from using an index, which can effect performance on large tables. Fortunately, it is easy to replace it with ‘whereBetween’:

```php
/**
 * Eloquent includes a whereDate method, as well as variations for moth, day, etc...
 * It is useful for finding all records on a particular date
 */
User::whereDate('created_at', now()->toDateString())->get();

/**
 * The problem, is that under the hood, Eloquent warps the where condition
 * within a DATE() function. In MySQL (and probably other databases), this
 * prevents an index from beign used, which can effect performance on large tables.
 * For large tables, this can hurt performance. You can easily fix it by replacing
 * it witb a whereBetween condition:
 */
$start = now()->startOfDay();
$end = now()->endOfDay();

User::whereBetween('created_at', [$start, $end])->get();
```

[🔝 Back to eloquent](#eloquent)    

```

[🔝 Back to eloquent](#eloquent)

### **whereIn**

Use a query builder in where-in clause

```php
Post::whereIn('user_id', User::select('id')->where('promoted',true))->get();
```

[🔝 Back to eloquent](#eloquent)
```

[🔝 Back to eloquent](#eloquent)

### **withCount**

```php
// Get post with comments count
$post = Post::withCount('comments');

// Get an article with approved comments count
$post = Post::withCount([
    'comments' => fn($query) => $query->where('approved',true)
]);

// You can access the comment using
$post->comment_counts;
```

[🔝 Back to eloquent](#eloquent)

### **with - cheat sheet**

```php
// Eager loads the 'author' relationship in the Book model
$books = Book::with('author')->get();

// Eager loads the 'author' and 'publisher' relationships in the Book model
$books = Book::with(['author','publisher'])->get();

// Eager loads the 'author' relationship in the Book model 
// and the 'contacts' relationship in the Author model
$books = Book::with('author.contacts')->get();

// Eager loads the 'author' relationship in the Book model 
// with only the columns 'id' and 'name'
$books = Book::with('author:id,name')->get();

// Eager loads by default the 'author' relationship 
class Book extends Model 
{
    protected $with = ['author'];
}

// You can disable default relationships with "without"
$books = Book::without('author')->get();

// Overwrite the $with property for a single query
$books = Book::withOnly('genre')->get();

// Eager loads with constraints.
// Only eager loads only the author that have the name begining with "Samuel"
$books = Book::with(['author' => function($query) {
    $query->where('name','like','Samuel%');
}])->get();

// You can eager load nested relations using clean array syntax
$books = Book::with([
    'author' => [
        'contacts',
        'publisher'
    ],
])->get();
```

[🔝 Back to eloquent](#eloquent)

### **Add Values to the form after validation**

Add Values to the Form Request After Validation

```php
class UpdateBookRequest extends FormRequest
{
    public function validated()
    {
        return array_merge(parent::validated(), [
            'user_id' => Auth::user()->id,
        ]);
    }
}
```

[🔝 Back to Form Request](#form-request)

### **Namespaces**

```php

// instead of
use App\Resources\UserResource;
use App\Resources\StudentResource;
use App\Resources\AdministratorResource;

// you can use
use App\Resources
```

[🔝 Back to eloquent](#eloquent)

### **Query Log**

Inside the 𝗔𝗽𝗽𝗦𝗲𝗿𝘃𝗶𝗰𝗲𝗣𝗿𝗼𝘃𝗶𝗱𝗲𝗿, locate the 𝗯𝗼𝗼𝘁() function and add the following statement

```php

// \app\Providers\AppServiceProvider.php

use DB;
use Log;

public function boot()
{

    // Add in the boot method of the AppServiceProvider
    DB::listen(function ($query) {
        Log::info($query->sql, $query->bindings, $query->time);
    });
}
```

[🔝 Back to logs](#logs)

composer require laravel/pint --dev

// running
./vendor/bin/pint -v

[🔝 Back to misc](#misc)

### **Migrate After**

If you want to add columns after another column then in that case you can use the `after` method.

```php
Schema::table('users', function (Blueprint $table) {
    $table->after('email', function ($table) {
        $table->integer('status');
        $table->string('address');
        $table->string('city');
        $table->string('state');
    });
});
```

[🔝 Back to migrate](#migrate)

### **Laravel Pint**

```php

// https://github.com/laravel/pint
// Laravel Pint requires PHP 8.0+.

composer require laravel/pint --dev

// running
./vendor/bin/pint -v
```

[🔝 Back to misc](#misc)

### **Config Values on the fly**

```php
use Illuminate\Support\Facades\Config;

Config::set('app.allowed_mail_domains', ['example.com']);
```

[🔝 Back to Misc](#misc)

### **Str Plural**

```php
{{ $itens->count() }}

{{ str('item')->plural($itens->count) }} in your cart

// 1 item in your cart
// 3 itens in your cart

// Macro
// In AppServiceProvider boot method
Str::macro(
    'pluralize', 
    fn($value, $count) => $count .' '. Str::plural($value,$count)
);

// Later
{{ Str::pluralize('item',$items->count()) }} in your cart

```

[🔝 Back to Misc](#misc)

### **Generate csv from route list**

```php
Route::get('r', function()
{
    header('Content-Type: application/excel');
    header('Content-Disposition: attachment; filename="routes.csv"');

    $routes = Route::getRoutes();
    $fp = fopen('php://output', 'w');
    fputcsv($fp, ['METHOD', 'URI', 'NAME', 'ACTION']);
    foreach ($routes as $route) {
        fputcsv($fp, [head($route->methods()) , $route->uri(), $route->getName(), $route->getActionName()]);
    }
    fclose($fp);
});
```

[🔝 Back to Route](#route)

### **Uri fragment**

```php
return redirect()
    ->back()
    ->withFragment('contactForm');
// domain.test/url#contactForm

return redirect()
    ->route('product.show')
    ->withFragment('reviews')
// domain.test/product/23#reviews

$products = Product::paginate(15)
    ->fragment('produts');
// domain.test/products?page=2#products
```

[🔝 Back to eloquent](#eloquent)

### **Redirect**

```php
Redirect::to();

Redirect::route();

redirect();

redirect()->to();

redirect()->route();

to_route();
```

[🔝 Back to eloquent](#eloquent)


### **Resources Group**

```php
// instead of
route::resource('users', UserController::class);
route::resource('clients', ClientController::class);
route::resource('providers', ProviderController::class);
route::resource('partners', PartnerController::class);

// You can use
Route::resources([
    'users' => UserController::class,
    'clients' => ClientController::class,
    'partners' => PartnerController::class,
    'providers' => ProviderController::class,
]);
```

[🔝 Back to route](#route)

### **Storage Cheatsheet**

```php
// Get the contents of a file
Storage::get($path);

// Create a streamed download response for a given file
Storage::download($path, $name = null, array $headers = []);

// Write the contents of a file
Storage::put($path, $contents, $options = []);

// Store the uploaded file on the disk
Storage::putFile($path, $file, $options = []);

// Store the uploaded file on the disk with a given name
Storage::putFileAs($path, $file, $name, $options = []);

// Get the visibility for the given path
Storage::getVisibility($path);

// Set the visibility for the given path
Storage::setVisibility($path, $visibility);

// Prepend to a file
Storage::prepend($path, $data, $separator = PHP_EOL);

// Append to a file
Storage::append($path, $data, $separator = PHP_EOL);

// Delete the file at a given path
Storage::delete($paths);

// Copy a file to a new location
Storage::copy($from, $to);

// Move a file to a new location
Storage::move($from, $to);

// Get the file size of a given file
Storage::size($path);

// Get the mime-type of a given file
Storage::mimeType($path);

// get the file's last modification time
Storage::lastModified($path);

// Get an array of all files in a directory
Storage::files($directory = null, $recursive = false);
```

[🔝 Back to storage](#storage)

### **Url Facade**

```php
Use Illuminate\Support\Facades\URL;

// example.com
'https://dominioprincipal.com.br/user/admin?foo=bar'

URL::current(); => 'https://dominioprincipal.com.br/user/admin'

URL::full(); => 'https://dominioprincipal.com.br/user/admin?foo=bar'

URL::previous(); => 'https://dominioprincipal.com.br'
```

[🔝 Back to storage](#url)

# PHP

[Get class methods](#get-class-methods) 

### **Get class methods**

```php
get_class_methods(mixed $class_name): array
```
[🔝 Back to php](#php)