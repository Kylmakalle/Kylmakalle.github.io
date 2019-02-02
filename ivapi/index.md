# IV API

Create IV image galleries and audio playlists using this API.

## SERVER SOURCE URL
- `https://github.com/Kylmakalle/ivapi`

## Headers
- `content-type: application/json`

## Method
- `POST`

## JSON params


| Field        | Type           | Required | Description |
| ------------- |:-------------:| :-----:| ------------- |
| title     | String | Yes | IV post title|
| comment | String     |   No |   IV post comment, will be seen as description in IV preview and as normal text in post|
| photos | Array of Photos  | Yes if no audios | Photos for gallery view |
| audios | Array of Audios  | Yes if no photos | Audio for playlist view  |

## Types
### Photo
Array of Photo urls and captions

| Field        | Type           | Required | Description |
| ------------- |:-------------:| :-----:| ------------- |
| url     | String | Yes | Photo url|
| caption | String     |   No | Caption that will be seen under photo in fullscreen  |

### Audio
Array of Audio urls

| Field        | Type           | Required | Description |
| ------------- |:-------------:| :-----:| ------------- |
| url     | String | Yes | Audio url|


## Result
```
{ 
  "ok": true, 
  "iv_url": "https://t.me/iv?url=https%3A%2F%2Fasergey.me%2Fiv%2Fe7414ec6abcd4a8e8b5b44e85633633a.html&rhash=610fa9e72e9e1a", 
  "url": "https://asergey.me/iv/35a6310140c04df2b59ca1d6efa1c850.html"
}
```

## Status codes

| Code | Description |
|:-----:| ---------- |
| `429` | You are making more than `1` request per `0.05` seconds| 
| `400` | Missing some required params|
| `403` | Wrong headers|


## Example Python code

```python
import requests
url = 'https://api.asergey.me/ivapi/'
header = {'content-type': 'application/json'}
data = {'title': 'SOME TITLE', 'comment': 'Some comment',
         'photos': [{'url': 'http://useless.altervista.org/iv/img_pulpit.jpg', 'caption': 'PIC A'},
                    {'url': 'http://useless.altervista.org/iv/img_pulpit.jpg', 'caption': 'PIC A1'},
                    {'url': 'http://useless.altervista.org/iv/img_pulpit2.jpg', 'caption': 'PIC B'}],
         'audios': [{'url': 'http://useless.altervista.org/iv/GreenIsLike.mp3'}, {
             'url': 'http://cdn.mos.musicradar.com/audio/samples/techno-demo-loops/TechBassR120E-01.mp3'}]}
iv = requests.post(url, json=data, headers=header)
print(iv.text)
```

