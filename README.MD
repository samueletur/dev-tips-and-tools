# GIT

[Git commands and their explanations](#git-commands)

# Images

[Using Picture](#using-picture)

[Using Srcset](#using-srcset)

# MAC

[Create fake file size](#create-fake-file-size) 

# MYSQL

[Delete billions of rows](#delete-billions-of-rows)

# PHP

[isset](#isset)

# Laravel

## Auth

[Breeze](#breeze)

[Login - Event](#login-event)

## Collection

[Arr::join](#arr-join)

## Eloquent

[allRelatedIds](#allRelatedIds)

[find](#find)

[GroupBy](#groupby)

[insertGetId](#insertGetId)

[Invisible Database Columns](#invisible-database-columns)

[isDirty and isClean](#isDirty-and-isClean)

[Lazy Loading](#lazi-loading)

[Push](#push)

[Relationships - Default](#relationships-default)

[Relationships - Querying existence of relationships](#relationships-querying-existence) `#mysql` `#whereHas` `#has` `#relationship`

[Routing - Parameters regular expression constraint](#routing-parameters-regular-expression-constraint) `#route`

[SelectRaw](#selectraw) `#mysql` `#selectRaw` `#query`

[Sensitive Data](#sensitive-data) `#crypt` `#cast` `#attribute`

[wasChanged](#wasChanged)

[when for conditionally situations](#when-for-conditionally-situations) `#when`

[whereBelongsTo](#whereBelongsTo)

[whereBetween with dates](#wherebetween-with-dates) use whereBetween with a range date. If you need to provide fallback you can do so with the nullish coalescing operator ?? `#whereBetween` `#date`

[whereColumn](#wherecolumn)

[with - cheatsheet](#with---cheat-sheet) #with #without

[withCount](#withcount) #with #withCount

## General

[Namespaces](#namespaces)

## Misc

[Laravel Pint](#laravel-pint)

[Str Plural](#str-plural)

[Config values on the fly](#config-values-on-the-fly)

## Route

[Generate csv from route list](#generate-csv-from-route-list)

[URI fragment](#uri-fragment)

[Redirect](#redirect)

## Storage

[Cheatsheet](#storage-cheatsheet)

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

### **Using picture**

```php
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

### **Delete billions of rows**

```php
// instead of
DELETE FROM user_activities WHERE year = 2020;

// you can use
ALTER TABLE user_activities DROP PARTITION user_activities_2019_q01, ..., user_activities_2019_q04; 
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

[🔝 Back to eloquent](#eloquent)

### **Arr Join**

Similar to `Collection::join`, you can `Arr::join` to return the new string by concatenating all of the elements in an array

```php
use illuminate\SupportArr;

$arr  = ['Batman', 'Superman', 'Spider', 'Aquaman'];

Arr::join($arr, ', ', ' and ');

// Batman, Spuperman, Spider and Aquaman
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

### **Lazi-Loading**

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

// Querying a relationship absense
$posts = Post::doesntHave('comments')->get();
$posts = Post::whereDoesntHave('comments', function (Builder $qry) {
    $qry->where('content','like','code%');
})->get();

```

[🔝 Back to eloquent](#eloquent)

routing-parameters-regular-expression-constraint
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

# PHP

[Get class methods](#get-class-methods) 

### **Get class methods**

```php
get_class_methods(mixed $class_name): array
```
[🔝 Back to php](#php)