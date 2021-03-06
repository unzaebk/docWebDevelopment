# Выполнить сортировку(упорядочивание) по связующему полю Eloquent

Вы могли бы сделать сортировку в [ `whereHas` ](https://laravel.com/docs/5.5/eloquent-relationships#querying-relationship-existence) 

```php
// Retrieve all products with at least one variant ordered by price

$query = Product::whereHas('variants', function ($query) use ($request) {
    if ($request->input('sort') == 'price') {
        $query->orderBy('variants.price', 'ASC');
    }
})
->with('reviews')
```

По сути, ваш подзапрос будет: `select * from variants where product_id in (....) order by price` , и это не то, что вы хотите, верно?

```php
<?php 
// ...

$order = $request->sort;

$products = Product::whereHas('variants')->with(['reviews',  'variants' => function($query) use ($order) {
  if ($order == 'price') {
    $query->orderBy('price');
  }
}])->paginate(20);

```

Если вы хотите отсортировать товар + / или вариант, вам нужно использовать join.

```php
$query = Product::select([
          'products.*',
          'variants.price',
          'variants.product_id'
        ])->join('variants', 'products.id', '=', 'variants.product_id');

if ($order === 'new') {
    $query->orderBy('products.created_at', 'DESC');
}

if ($order === 'price') {
    $query->orderBy('variants.price');
}

return $query->paginate(20);
```

**********
[PHP](/tags/PHP.md)
[Eloquent](/tags/Eloquent.md)
[сортировка (sort)](/tags/%D1%81%D0%BE%D1%80%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%BA%D0%B0%20%28sort%29.md)
[упорядочивание (order) ](/tags/%D1%83%D0%BF%D0%BE%D1%80%D1%8F%D0%B4%D0%BE%D1%87%D0%B8%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%28order%29%20.md)
