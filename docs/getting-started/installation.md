# Installation

Voyager 非常便於安裝，在您建立您的 Laravel 應用後使用 composer 指令 : 

```bash
composer require tcg/voyager
```

接著確認您建立了一個新的資料庫並將資料庫資料加入至 .env 檔案中，以及在 .env 內的 APP_URL 替換為您的應用程式網址

```text
APP_URL=http://localhost
DB_HOST=localhost
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```

{% hint style="info" %}
**使用 Laravel 5.4?**  
如您使用 Laravel 5.4 請參閱 [add the Service Provider manually](installation.md#adding-the-service-provider). Otherwise, if you are on 5.5 this happens automatically thanks to package auto-discovery.
{% endhint %}

最後, 我們準備動手安裝 voyager. 

{% hint style="tip" %}
**使用本地化語言**  
先開啟 `config/app.php` 並設定 `'locale' => 'zh-TW'` , 接著執行 `voyager:install` 便會安裝中文版的 voyager
{% endhint %}

您可以選擇簡單安裝或附有虛擬資料(dummy)的安裝方式，附帶虛擬資料的安裝內容包含 1 個管理者帳號(如果沒有使用者存在於資料表內)、1 個網頁、
4 則文章、2 個分類及 7 個設定

不包含虛擬資料的簡單安裝

```bash
php artisan voyager:install
```

若您想要使用含有虛擬資料的安裝方式請輸入以下指令

```bash
php artisan voyager:install --with-dummy
```

{% hint style="danger" %}
**Specified key was too long error**  
若您看到以上訊息則表示您使用的 MySQL 版本過低, 請參閱以下解決方式: [https://laravel-news.com/laravel-5-4-key-too-long-error](https://laravel-news.com/laravel-5-4-key-too-long-error)
{% endhint %}

輸入 `php artisan serve` 啟動服務並開啟 [http://localhost:8000/admin](http://localhost:8000/admin) 頁面測試看看吧！

如果您在安裝時包含了虛擬數據，則安裝完成後會一併建立以下的管理帳號 : 

>**email:** `admin@admin.com`   
>**password:** `password`

{% hint style="info" %}
**說明**  
只有在資料庫內未含有用戶資料時才會創建虛擬管理員
{% endhint %}

如果您未創建虛擬資料，並希望將管理員權限分配給現有用戶，以下的命令可以讓您輕鬆地完成此工作

```bash
php artisan voyager:admin your@email.com
```

如果您想建立一個新的管理員帳號，透過添加 `--create` 指令來完成，如

```bash
php artisan voyager:admin your@email.com --create
```

接著系統會要求您輸入帳號密碼即可完成創建管理員步驟。

## 進階安裝

本節適用於在現有 Laravel 安裝上安裝 Voyager 或希望執行手動安裝的用戶。若您非上述情形，請回到[installation](installation.md)或跳過本章捷

您應該做的第一件事是發布Voyager附帶的資產。您可以通過運行以下命令來執行此操作：

```bash
php artisan vendor:publish --provider=VoyagerServiceProvider
php artisan vendor:publish --provider=ImageServiceProviderLaravel5
```

## 添加至服務提供者

{% hint style="info" %}
**只針對使用 Laravel 5.4!**  
若您使用 Laravel 5.5+ 請跳過此章節
{% endhint %}

新增 Voyager 至服務提供者，請打開 `config/app.php`，並將 `TCG\Voyager\VoyagerServiceProvider::class,` 添加至 `providers` 陣列內。

如

```php
<?php

'providers' => [
    // Laravel Framework Service Providers...
    //...

    // Package Service Providers
    TCG\Voyager\VoyagerServiceProvider::class,
    // ...

    // Application Service Providers
    // ...
],
```

