# Laravel

## Eloquent

[Push](#push)

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

[🔝 Back to contents](#eloquent)







