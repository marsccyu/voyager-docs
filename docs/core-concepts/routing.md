# Routing

在您執行安裝 Voyager 後，您會發現有一些新的路由添加至 `routes/web.php` 檔案中 : 

```php
Route::group(['prefix' => 'admin'], function () {
    Voyager::routes();
});
```

這是渲染 Voyager 路徑的地方，您可以依照需求修改 `admin` 前綴或設置其他關於 `middleware`、 `domain` 的路由配置。  

當建立新 BREAD 類型及指定 slug 名稱後, 您可以使用以下的連結訪問路由 :  

```text
URL/admin/slug-name
```

舉例來說, 如果我們有一個名為 `products` 的資料表而且我們指定 slug 為 `products`, 您現在將可以使用以下的連結訪問 : 

```text
URL/admin/products
```

{% hint style="info" %}
**Notice**
您可能無法在管理員選單中看到指向新創建的路線或 BREAD 的連結。要在管理員選單中創建新連結，請訪問選單部分的[文檔](menus-and-menu-builder.md).
{% endhint %}

