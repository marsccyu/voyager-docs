# Overriding Routes

您可以經由 在`Voyager::routes()` 內撰寫您想要覆蓋的路由覆蓋任何 Voyager 路由，舉例來說如果您想要覆蓋貼文的登入控制器 : 

```php
Route::group(['prefix' => 'admin'], function () {
   Voyager::routes();

   // Your overwrites here
   Route::post('login', ['uses' => 'MyAuthController@postLogin', 'as' => 'postlogin']);
});
```

