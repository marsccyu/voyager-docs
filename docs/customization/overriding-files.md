# Overriding files

### Overriding BREAD Views

您可以經由在 `resources/views/vendor/voyager/slug-name` 內創建新目錄來覆蓋**單個BREAD**的任何 BREAD 視圖， 其中的 _slug-name_ 是您分配給資料表的 _slug_ 名稱。 

這裡有四個檔案可以覆蓋 : 

* browse.blade.php
* edit-add.blade.php
* read.blade.php
* order.blade.php

透過在 `resources/views/vendor/voyager/bread` 內建立上述的檔案來覆蓋所有 **BREADs** 的視圖

### Using custom Controllers

您可以透過繼承 Voyagers 控制器的新控制器來覆蓋單個 BREAD 的控制器，舉例來說 :  

```php
<?php

namespace App\Http\Controllers;

class VoyagerCategoriesController extends \TCG\Voyager\Http\Controllers\VoyagerBaseController
{
    //...
}
```
之後轉到 BREAD 設置並使用符合限制的類名填寫控制器名稱 :

![](../.gitbook/assets/bread_controller.png)

您現在可以覆蓋所有在 [VoyagerBaseController](https://github.com/the-control-group/voyager/blob/1.1/src/Http/Controllers/VoyagerBaseController.php) 內的方法 

### Overriding Voyagers Controllers

如果您想要覆蓋任何 Voyagers 的核心控制器，您首先需要修改 `config/voyager.php` 內的設定 : 

```php
/*
|--------------------------------------------------------------------------
| Controllers config
|--------------------------------------------------------------------------
|
| Here you can specify voyager controller settings
|
*/
​
'controllers' => [
    'namespace' => 'App\\Http\\Controllers\\Voyager',
],
```

接著執行 `php artisan voyager:controllers` ，Voyager 現在將會使用被創建在 `App/Http/Controllers/Voyager` 內的子控制器。

### Overriding Voyager-Models

如果您需要的話，您也可以覆蓋 Voyagers 模型。為此，您需要在您的 `AppServiceProviders` 註冊方法內添加以下內容 :

```php
Voyager::useModel($name, $object);
```

這邊的 **name** 是模型的類名稱而 **object** 則是自訂模型內完全符合限制的名稱，舉例來說 :

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Events\Dispatcher;
use TCG\Voyager\Facades\Voyager;

class AppServiceProvider extends ServiceProvider
{
    public function register()
    {
        Voyager::useModel('DataRow', \App\DataRow::class);
    }
    // ...
}
```

下個步驟是建立一個您的模型，這個模型必須繼承原始模型，以 `DataRow` 舉例來說 :

```php
<?php

namespace App;

class DataRow extends \TCG\Voyager\Models\DataRow
{
    // ...
}
```
