# 配置

當您安裝 Voyager 完成後，您會找到一個新的配置檔案位於 `config/voyager.php`

在這個文件中，您可以找到各種選項來更改 Voyager 安裝的配置。

{% hint style="info" %}
若您對於配置檔案進行了快取，請確保在您更改配置設定後執行 `php artisan config:clear` 指令
{% endhint %}

下面我們將深入探討配置文件，並提供每個配置設定的詳細說明

## Users

```php
<?php

'user' => [
    'add_default_role_on_register' => true,
    'default_role'                 => 'user',
    'admin_permission'             => 'browse_admin',
    'namespace'                    => App\User::class,
    'redirect'                     => '/admin'
],
```

**add\_default\_role\_on\_register:** 指定是否要將默認角色添加到創建的任何新用戶。
**default\_role:** 您還可以指定用戶是何種默認腳色  
**admin\_permission:** 可以瀏覽後台管理頁面的腳色權限  
**namespace:** 您的 User Class 使用的命名空間  
**redirect:** 用戶登入後重新導向的路徑。

## Controller

```php
<?php

'controllers' => [
    'namespace' => 'TCG\\Voyager\\Http\\Controllers',
],
```

您可以指定 Voyager 默認的 `controller` 命名空間，如果您希望覆寫 Voyager 的任何核心功能，可以透過複製 Voyager 控制器並指定自定義控制器的位置來實現。

{% hint style="info" %}
**複寫單個控制器**  
如果您只想覆蓋單個控制器, 您可以考慮將以下代碼添加到您的 `AppServiceProvider` class 的 `register` 方法內.  
`$this->app->bind(VoyagerBreadController::class, MyBreadController::class);`
{% endhint %}

## Model

```php
<?php

'models' => [
    //'namespace' => 'App\\',
],
```

您可以指定資料庫模型的命名空間或位置，從 Voyager 的數據庫部分創建模型時使用此方法。如果未定義此方法，將使用默認應用程序命名空間。

## Assets

```php
<?php

'assets_path' => '/vendor/tcg/voyager/assets',
```

您可能希望指定不同的 `assets` 路徑，如果您的站點位於子資料夾中，則可能需要將該目錄包含在路徑的開頭。

如果您希望複製已發布的資源並自定義您自己的資源，也可以使用此方法。

{% hint style="info" %}
當您升級 Voyager 的新版本時，可能需要覆蓋在 `/vendor/tcg/voyager/assets` 內的檔案，所以如果您需要自訂任何樣式表則需要復該製目錄並指定 asset_path 的新位置。
{% endhint %}

## Storage

```php
<?php

'storage' => [
    'disk' => 'public',
],
```

Voyager 預設使用本地端的 public 目錄，您還可以使用在 `config/filesystems.php` 中的其他驅動程序，這表示您可以使用如 S3 、 Google Cloud Storage 或是任何您想使用的儲存方式

## Database

```php
<?php

'database' => [
    'tables' => [
        'hidden' => ['migrations', 'data_rows', 'data_types', 'menu_items', 'password_resets', 'permission_role', 'settings'],
    ],
],
```

您可能希望隱藏部分 Voyager 中的資料表，在資料庫配置中，您可以選擇要隱藏的資料表。

## Multilingual

```php
<?php

'multilingual' => [
    'enabled' => false,
    'default' => 'en',
    'locales' => [
        'en',
        //'pt',
    ],
],
```

您可以指定是否要啟動(**enable**)多語言，您可以指定默認語言和所有支持語言（區域設置）。

了解更多關於多語言設定 [multilanguage](../core-concepts/multilanguage.md).

## Dashboard

```php
<?php

'dashboard' => [
    'navbar_items' => [
        'Profile' => [
            'route'         => 'voyager.profile',
            'classes'       => 'class-full-of-rum',
            'icon_class'    => 'voyager-person',
        ],
        'Home' => [
            'route'         => '/',
            'icon_class'    => 'voyager-home',
            'target_blank'  => true,
        ],
        'Logout' => [
            'route'      => 'voyager.logout',
            'icon_class' => 'voyager-power',
        ],
    ],
    'widgets' => [
        'TCG\\Voyager\\Widgets\\UserDimmer',
        'TCG\\Voyager\\Widgets\\PostDimmer',
        'TCG\\Voyager\\Widgets\\PageDimmer',
    ],
],
```

在控制台配置中，您可以添加 navbar_items 使 data_tables 為響應式，進而管理儀表板小部件。

**navbar\_items** 透過 'route', 'icon\_class', and 'target\_blank' 設定包含在主用戶導航選單下的新路由

**data\_tables** 如果將 'responsive' 設置為 true ，則資料表將是響應式的。 

**widgets** 在此處可以管理在控制台內的小工具元件，您可以查看 `tcg/voyager/src/Widgets` 中的當前窗口小元件來查看示例窗口小元件類。

## Primary color

```php
<?php

'primary_color' => '#22A7F0',
```

Voyager 的預設主色為亮藍色，您可以在此配置中更換主色

## Show developer tips

```php
<?php

'show_dev_tips' => true,
```


在 Voyager 中，有開發者提示或通知，將向您展示如何從Voyager中引用某些值。您可以通過將此配置值設置為 false 來選擇隱藏這些通知。

## Additional stylesheets

```php
<?php

'additional_css' => [
    //'css/custom.css',
],
```

您可以添加自定義樣式表，這些樣式表將包含在 Voyager 管理中。這意味著您可以通過添加自己的自定義樣式表在技術上為 Voyager 創建一個全新的主題。

[了解更多](../customization/additional-css-js.md).

{% hint style="info" %}
該路徑將傳遞至 Laravel 的 [asset](https://laravel.com/docs/helpers#method-asset) 功能
{% endhint %}

## Additional Javascript

```php
<?php

'additional_js' => [
    //'js/custom.js',
],
```

這個配置與 CSS 樣式表相同，您可以添加自定義的 javascript 並在 Voyager 管理中執行。

[了解更多](../customization/additional-css-js.md).

## Google Maps

```php
<?php

'googlemaps' => [
    'key'    => env('GOOGLE_MAPS_KEY', ''),
    'center' => [
        'lat' => env('GOOGLE_MAPS_DEFAULT_CENTER_LAT', '32.715738'),
        'lng' => env('GOOGLE_MAPS_DEFAULT_CENTER_LNG', '-117.161084'),
    ],
    'zoom' => env('GOOGLE_MAPS_DEFAULT_ZOOM', 11),
],
```

有一種稱為 **coordinates** 的新數據類型，允許您將谷歌地圖添加為數據類型。然後，用戶可以在 Google 地圖中拖放圖釘以在數據庫中保存經度和緯度值。

在此配置中，您可以設置默認的 Google 地圖密鑰和中心位置。這也可以添加到 .env 文件中。

