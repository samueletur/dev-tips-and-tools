# MAC

[Create fake file size](#create-fake-file-size) 

### **Create fake file size**

```php
// MacOs snippet to fake a 10MB PDF file
mkfile 10m testfile.pdf
```

[🔝 Back to php](#php)

# Laravel

## Auth

[Breeze](#breeze)

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

## Eloquent

[allRelatedIds](#allRelatedIds)

[find](#find)

[insertGetId](#insertGetId)

[isDirty and isClean](#isDirty-and-isClean)

[Push](#push)

[Relationships - Querying existence of relationships](#relationships-querying-existence) `#mysql` `#whereHas` `#has` `#relationship`

[Routing - Parameters regular expression constraint](#routing-parameters-regular-expression-constraint) `#route`

[SelectRaw](#selectraw) `#mysql` `#selectRaw` `#query`

[Sensitive Data](#sensitive-data) `#crypt` `#cast` `#attribute`

[wasChanged](#wasChanged)

[when for conditionally situations](#when-for-conditionally-situations) `#when`

[whereBelongsTo](#whereBelongsTo)

[whereBetween with dates](#wherebetween-with-dates) use whereBetween with a range date. If you need to provide fallback you can do so with the nullish coalescing operator ?? `#whereBetween` `#date`

[with - cheat sheet](#with---cheat-sheet) #with #without

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

### **Push**

Save the product and its relations

```php
$product = Product::find(1);

$product->name = 'New Balance Shoes';
$product->brand->name = 'New Balance';
$product->department->name = 'Men';

// Save the product and its relations
$product->push();
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
```

[🔝 Back to eloquent](#eloquent)


# PHP

[Get class methods](#get-class-methods) 

### **Get class methods**

```php
get_class_methods(mixed $class_name): array
```
[🔝 Back to php](#php)