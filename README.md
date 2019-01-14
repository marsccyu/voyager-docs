# **V**oyager
Made by [The Control Group](https://www.thecontrolgroup.com)

Website & Documentation: https://laravelvoyager.com

Video Tutorial Here: https://laravelvoyager.com/academy/

View the Voyager Cheat Sheet: https://voyager-cheatsheet.ulties.com/

<hr>

Laravel Admin & BREAD System (Browse, Read, Edit, Add, & Delete), supporting Laravel 5.4, 5.5, 5.6 and 5.7!

## 安裝

### 1. Require the Package

After creating your new Laravel application you can include the Voyager package with the following command: 

```bash
composer require tcg/voyager
```

### 2. 加入資料庫及網站連結

先創立一個新的資料庫並將帳號密碼填入 .env 文件內

```
DB_HOST=localhost
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```

以及在 .env 文件內更新您的網站連結

```
APP_URL=http://localhost:8000
```

> 如果您使用 Laravel 5.4 版本請參閱 [Add the Service Provider.](https://voyager.readme.io/docs/adding-the-service-provider)

### 3. Run The Installer

最後我們可以開始安裝 voyager， 您可以在安裝時選擇是否一併填入虛擬數據。

虛擬數據內會含有 1 個 admin 管理帳號(如果 user 表不存在)、 1 個範例頁面、 4 則貼文 、2 個分類表及 7 個設定

簡單安裝 (不包含虛擬數據) :

```bash
php artisan voyager:install
```

安裝時包含虛擬數據 : 

```bash
php artisan voyager:install --with-dummy
```

> 障礙排除 : 安裝過程若遇到資料庫提示**Specified key was too long error**. 則表示您的 MySQL 版本過低, 請參閱網頁 : https://laravel-news.com/laravel-5-4-key-too-long-error

一切安裝完成之後，開始 voyager 吧 !

輸入 `php artisan serve` 開始您的本機開發服務然後開啟 [http://localhost:8000/admin](http://localhost:8000/admin).

## 建立管理員帳號

如果您在安裝時包含了虛擬數據，則安裝完成後會一併建立以下的管理帳號 : 

>**email:** `admin@admin.com`   
>**password:** `password`

注意 : 只有在資料庫內未含有用戶資料時才會創建虛擬管理員

如果您沒有使用虛擬用戶，則可能希望為現有用戶分配管理員權限。這可以通過運行此命令輕鬆完成

```bash
php artisan voyager:admin your@email.com
```

如果您未創建虛擬資料，以下的命令可以使您創造一個管理員帳號

```bash
php artisan voyager:admin your@email.com --create
```

接著系統會要求您輸入帳號密碼即可完成創建管理員步驟。
