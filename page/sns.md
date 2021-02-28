# SNS

## Instagram
2020年6月29日までは、[instafeed](https://instafeedjs.com/)を使ってJavaScriptで表示していましたが、  
2020年6月30日以降は新しいAPI(Instagram Basic Display APIおよびInstagram Graph API）では、PHPを使用して表示します。  
  
サーバーによってやり方が異なりますので、  
表示できる方を使用してください。


### file_get_contents
```php
<ul class="js-loopslider__content">
	<?php
		$count = '6'; //画像取得数
		$id    = ''; //InstagramビジネスアカウントID
		$token = ''; // アクセストークン3

		///////////////////////////////////////////////////////////////
		// file_get_contents
		///////////////////////////////////////////////////////////////
		$json = file_get_contents("https://graph.facebook.com/v6.0/{$id}?fields=name%2Cmedia.limit({$count})%7Bcaption%2Cmedia_url%2Cthumbnail_url%2Cpermalink%7D&access_token={$token}");

		$json = mb_convert_encoding($json, 'UTF8', 'ASCII,JIS,UTF-8,EUC-JP,SJIS-WIN');
		$obj = json_decode($json, true);


		///////////////////////////////////////////////////////////////
		// output
		///////////////////////////////////////////////////////////////
		$insta = [];

		foreach ($obj['media']['data'] as $k => $v) {
			if ( isset( $v['thumbnail_url'] ) ) {
				$data = [
					'img'  => $v['thumbnail_url'], // 投稿が動画だったらサムネURLを取得
					'link' => $v['permalink'],    // パーマリンク
				];
			} else {
				$data = [
					'img'  => $v['media_url'],
					'link' => $v['permalink'],
				];
			}
			$insta[] = $data;
		}

		foreach ($insta as $k => $v){
			echo '<li><a href="'.$v['link'].'" target="_blank"><img src="'.$v['img'].'" class="c-objectfit -cover"></a></li>';
		}

	?>
</ul>
```

### cURL
```php
<ul class="js-loopslider__content">
	<?php
		$count = '6'; //画像取得数
		$id    = ''; //InstagramビジネスアカウントID
		$token = ''; // アクセストークン3


		///////////////////////////////////////////////////////////////
		// cURL
		///////////////////////////////////////////////////////////////
		$url = 'https://graph.facebook.com/v6.0/'.$id.'?fields=name%2Cmedia.limit('.$count.')%7Bcaption%2Cmedia_url%2Cthumbnail_url%2Cpermalink%7D&access_token='.$token;

		$ch = curl_init();
		curl_setopt($ch, CURLOPT_URL, $url);
		curl_setopt($ch, CURLOPT_HEADER, false);
		curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
		curl_setopt($ch, CURLOPT_TIMEOUT, 60);
		$json = curl_exec($ch);
		curl_close($ch);
		$obj = json_decode($json, true);


		///////////////////////////////////////////////////////////////
		// output
		///////////////////////////////////////////////////////////////
		$insta = [];

		foreach ($obj['media']['data'] as $k => $v) {
			if ( isset( $v['thumbnail_url'] ) ) {
				$data = [
					'img'  => $v['thumbnail_url'], // 投稿が動画だったらサムネURLを取得
					'link' => $v['permalink'],    // パーマリンク
				];
			} else {
				$data = [
					'img'  => $v['media_url'],
					'link' => $v['permalink'],
				];
			}
			$insta[] = $data;
		}

		foreach ($insta as $k => $v){
			echo '<li><a href="'.$v['link'].'" target="_blank"><img src="'.$v['img'].'" class="c-objectfit -cover"></a></li>';
		}

	?>
</ul>
```

