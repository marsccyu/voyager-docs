# Multilanguage

Voyager 支援在模型中使用多語系，在開始之前，您必須先做一些設置 

## Setup

首先，您需要在 `config/voyager.php` 定義 `locales`，並且啟用 \(`enable`\) 多語系 :

```php
'multilingual' => [
        'enabled' => true,
        'rtl' => false,
        'default' => 'en',
        'locales' => [
            'en',
            'da',
        ],
    ],
```

之後您需要在您的模型內包含 `Translatable` 特徵，然後定義可翻譯屬性 : 

```php
use TCG\Voyager\Traits\Translatable;
class Post extends Model
{
    use Translatable;
    protected $translatable = ['title', 'body'];
}
```

現在，您將可以看在 BREAD 中看到語系選擇的選項。

## Usage

### Eager-load translations

```php
// Loads all translations
$posts = Post::with('translations')->get();

// Loads all translations
$posts = Post::all();
$posts->load('translations');

// Loads all translations
$posts = Post::withTranslations()->get();

// Loads specific locales translations
$posts = Post::withTranslations(['en', 'da'])->get();

// Loads specific locale translations
$posts = Post::withTranslation('da')->get();

// Loads current locale translations
$posts = Post::withTranslation('da')->get();
```

### Get default language value

```php
echo $post->title;
```

### Get translated value

```php
echo $post->getTranslatedAttribute('title', 'locale', 'fallbackLocale');
```

如果您未定義 `locale`，那麼當前應用程序的語言環境 \(`locale`\) 將會被調用，您可以將您的 `locale` 作為字串傳遞。

如果您未定義 `fallbackLocale`，那麼當前應用程序 `fallbackLocale` ，如果您想要關閉 `fallbacklocale`，只要傳遞 `false` 即可。
如果在模型內指定的屬性值未被找到，像是 `locale` 或 `fallback`，它會將該屬性設置為null。

### Translate the whole model

```php
$post = $post->translate('locale', 'fallbackLocale');
echo $post->title;
echo $post->body;

// You can also run the `translate` method on the Eloquent collection
// to translate all models in the collection.
$posts = $posts->translate('locale', 'fallbackLocale');
echo $posts[0]->title;
```


### Check if model is translatable

```php
// with string
if (Voyager::translatable(Post::class)) {
    // it's translatable
}

// with object of Model or Collection
if (Voyager::translatable($post)) {
    // it's translatable
}
```

### Set attribute translations

```php
$post = $post->translate('da');
$post->title = 'foobar';
$post->save();
```

這將會更新或創建具有 da 的標題翻譯，請注意，如果修改後的屬性不可翻譯，則會直接對模型本身進行更改。這意味著它將覆蓋默認語言集中的屬性。

