# MAC

[Create fake file size](#create-fake-file-size) 

### **Create fake file size**

```php
// MacOs snippet to fake a 10MB PDF file
mkfile 10m testfile.pdf
```

[🔝 Back to php](#php)

# Laravel

## Eloquent

[allRelatedIds](#allRelatedIds)

[Push](#push)

[Sensitive Data](#sensitive-data) `#crypt` `#cast` `#attribute`

[whereBelongsTo](#whereBelongsTo)

[whereBetween with dates](#wherebetween-with-dates) use whereBetween with a range date. If you need to provide fallback you can do so with the nullish coalescing operator ??

### **allRelatedIds**

An alternative to pluck('id'') to get all of the IDs for the related models.

```php
// instead of
$article->tags()->pluck('id')->toArray();

// you can use
$article->tags()->allRelatedIds()->toArray();
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

### **whereBelongsTo**

Get relationship without use where on query

```php
// instead of
Order::where('user_id',$user->id)->sum('total_amount');

// you can use
Order::whereBelongsTo($user)->sum('total_amount');
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


# PHP

[Get class methods](#get-class-methods) 

### **Get class methods**

```php
get_class_methods(mixed $class_name): array
```
[🔝 Back to php](#php)