# Additional CSS and JS

在最新的版本您現在可以添加額外的 CSS 及 JS 檔案至 Voyager 主要的視圖中，無須修改或複製視圖本身，CSS 及 JS 檔案可以在任何 Voyager 資源後添加，所以您可以輕易地覆蓋樣式及函式

這些都可以透過 `voyager.php` 設置處理 :

```php
// Here you can specify additional assets you would like to be included in the master.blade
'additional_css' => [
    //'css/custom.css',
],
'additional_js' => [
   //'js/custom.js',
],
```

{% hint style="info" %}
該路徑將會傳遞至 Laravels [asset](https://laravel.com/docs/helpers#method-asset) 功能中。
{% endhint %}

