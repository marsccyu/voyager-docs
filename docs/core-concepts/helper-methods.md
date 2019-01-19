# Helper methods

Voyager 有幾個可以使用的輔助函數，您可以在這邊找到這些清單並加速您的開發

## Thumbnails URL

當您指定 [additional field options](bread-builder.md#additional-field-options) 時，Voyager 將為圖片欄位類型生成縮略圖。 

在創建縮圖後，您或許希望縮圖顯示在您的視圖中或取得縮圖連結，為此，您需要添加 `Resizable` 在您的模型中。

```php
use TCG\Voyager\Traits\Resizable;

class Post extends Model
{
    use Resizable;
}
```

#### Display a single image

```php
@foreach($posts as $post)
    <img src="{{Voyager::image($post->thumbnail('small'))}}" />
@endforeach
```

或者您可以指定可選的圖片欄位名稱（屬性），默認為圖像
Or you can specify the optional image field name \(attribute\), default to `image`

```php
@foreach($posts as $post)
    <img src="{{Voyager::image($post->thumbnail('small', 'photo'))}}" />
@endforeach
```

#### Display multiple images

```php
@foreach($posts as $post)
    $images = json_decode($post->images);
    @foreach($images as $image)
        <img src="{{ Voyager::image($post->getThumbnail($image, 'small')) }}" />
    @endforeach
@endforeach
```

