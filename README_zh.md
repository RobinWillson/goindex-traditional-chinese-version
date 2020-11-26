# GoIndex-theme-acrou

結合 [Cloudflare Workers](https://workers.cloudflare.com/) 和 [Google Drive](https://www.google.com/drive/) 的力量，你可以在Cloudflare Workers的瀏覽器上建立你的文件索引。

[go2index/index.js](https://github.com/Aicirou/goindex-theme-acrou/go2index) 是Workers腳本的內容。

這個主題的goindex目前是基於 [Achrou/goindex-theme-acrou](https://github.com/Achrou/goindex-theme-acrou)

[README](README.md) | [中文文檔](README_zh.md)

## 預覽  

Acrou: [https://oss.achirou.workers.dev/](https://oss.achirou.workers.dev/) 

## 特色

- [x] 👑 頁面級緩存，瀏覽器前進後退不刷新秒加載（mac用戶使用觸控板體驗更佳）
- [x] 🗂 多盤切換
- [x] 🔐 Http Basic Auth
- [x] 🎨 網格視圖模式（文件預覽）
- [x] 🎯 分頁加載
- [x] 🌐 I18n（多國語言）
- [x] 🛠 Markdown/Html渲染（也許它可以成為你的博客）
- [x] 🖥 視頻在線播放（支持外掛字幕vtt）
- [x] 🕹 支持自定義視頻播放器（API）
- [x] 🎧 音頻在線播放
- [x] 🚀 擁有更快的速度

## TODO

- [ ] 更多文件格式預覽
- [ ] 讓Goindex不只是一個目錄索引

## 快速部署

1. 打開以下任意網址

   - https://goindex-auth.glitch.me

2. 授權並獲取授權碼

3. 將代碼部署到 [Cloudflare Workers](https://www.cloudflare.com/)

## 部署

1. 開啟[Google Drive API](https://console.developers.google.com/apis/api/drive.googleapis.com/overview)
2. 創建一個 [OAuth client ID](https://console.developers.google.com/apis/credentials/oauthclient)
3. 本地安裝[rclone](https://rclone.org/downloads/)
4. 使用`rclone`獲取`refresh_token`
5. 下載`index.js` (https://github.com/Eggsmemory/goindex-theme-acrou/blob/master/go2index/index.js) 然後替換`client_id`,`client_secret`,`refresh_token` 為你剛剛獲取到的
6. 把代碼部署到[Cloudflare Workers](https://www.cloudflare.com/)

> 如果你寫了一篇不錯的文章，想分享給大家，請提交Issues，我會把鏈接貼在這里。

## 選項

### Video

| Option     | Type                       | Default                                                      | Description                                                  |
| ---------- | -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `api`      | String                     | `''`                                                         | 外部視頻播放器api。當這個值不為空時，以下所有選項都不起作用。 |
| `autoplay` | Boolean                    | `true`                                                       | 當設置為`true`時，視頻會自動播放，不過這取決於瀏覽器是否支持。 |
| `controls` | Array, Function or Element | `['play-large', 'restart', 'play', 'progress', 'current-time', 'duration', 'mute', 'volume', 'captions', 'settings', 'pip', 'airplay', 'download', 'fullscreen']` | 控制欄中顯示哪些按鈕。詳細查看[CONTROLS.md](https://github.com/sampotts/plyr/blob/master/CONTROLS.md#using-default-controls) |
| `settings` | Array                      | `['quality', 'speed', 'loop']`                               | 菜單中顯示哪些設置                                           |

更多選項查看 plyr [options](https://github.com/sampotts/plyr#options)

### Audio

| Option      | Type    | Default    | Description                                                  |
| ----------- | ------- | ---------- | ------------------------------------------------------------ |
| `container` | String  | `.aplayer` | 不支持修改                                                   |
| `fixed`     | Boolean | `true`     | 不支持修改                                                   |
| `autoplay`  | Boolean | `false`    | 當設置為`true`時，音頻會自動播放，不過這取決於瀏覽器是否支持。 |
| `loop`      | String  | `'all'`    | 音頻循環播放, 可選值: 'all', 'one', 'none'                   |
| `order`     | String  | `'list'`   | 音頻循環順序, 可選值: 'list', 'random'                       |
| `preload`   | String  | `'auto'`   | 預加載，可選值: 'none', 'metadata', 'auto'                   |
| `volume`    | Number  | `0.7`      | 默認音量，請注意播放器會記憶用戶設置，用戶手動設置音量後默認音量即失效 |
| `audios`    | Array   | `[]`       | 預設播放列表。詳情查看 [FAQ](#FAQ)                           |

更多選項查看 APlayer [options](https://aplayer.js.org/#/home?id=options)

## 常見問題

> 怎麽修改列表的排序方式？

修改第636行或者在代碼中搜索`params.orderBy`

```javascript
－ params.orderBy = "folder,name,modifiedTime desc";
＋ params.orderBy = "modifiedTime desc";
```

> 怎麽預設音頻播放列表？

音頻選項中添加 `audios`

```
audio: {
  audios: [
    {
      name: "Mojito",
      artist: "周杰倫",
      url: "https://xx.mp3",
      lrc: "https://xx.lrc",
      cover: "https://xx.jpg"
    }
  ]
}
```

## 更新日志

### v2.0.8

- 修覆圖片文件操作列不可用問題 [#100](https://github.com/Aicirou/goindex-theme-acrou/issues/100)
- 修覆錯誤判斷圖片問題 [#88](https://github.com/Aicirou/goindex-theme-acrou/issues/88)
- 修覆無法設置10個以上的drive [#59](https://github.com/Aicirou/goindex-theme-acrou/issues/59) [#85](https://github.com/Aicirou/goindex-theme-acrou/issues/85)
- 修覆搜索結果中的某些操作無法使用
- 修覆修改內容後緩存不刷新
- 添加默認視頻播放器 ([plyr](https://github.com/sampotts/plyr)) [#22](https://github.com/Aicirou/goindex-theme-acrou/issues/22) [#38](https://github.com/Aicirou/goindex-theme-acrou/issues/38)
- 添加音頻播放器 ([APlayer](https://github.com/MoePlayer/APlayer)) [#77](https://github.com/Aicirou/goindex-theme-acrou/issues/77)
- 視頻頁面添加覆制按鈕
- 添加 [NProgress](https://github.com/rstacruz/nprogress)
- 添加語言緩存清理
- 添加快捷方式無法下載提示 [#76](https://github.com/Aicirou/goindex-theme-acrou/issues/76)
- Markdown默認顯示渲染的html
- CLI刪除懶加載模塊的預加載
- 刪除fontawesome5

### v2.0.5

- 添加清理文件緩存
- 支持自定義視頻播放器（API）
- 美化：網格模式文件無預覽圖時顯示圖標
- 美化：調整HEAD.md渲染位置
- 解決搜索不能預覽的文件點擊無法直接下載 [#30](https://github.com/Aicirou/goindex-theme-acrou/issues/30)
- 解決文件名中有#無法打開的問題 [#20](https://github.com/Aicirou/goindex-theme-acrou/issues/20)
- 解決當前頁面加載中切換頁面會回退的問題 [#37](https://github.com/Aicirou/goindex-theme-acrou/issues/37) (感謝[@PedroZhang](https://github.com/PedroZhang)幫忙找出的問題原因)

### v2.0.0

- 程序改為單頁應用

- 添加頁面級緩存（瀏覽器前進後退不刷新秒加載，mac用戶使用觸控板體驗更佳）
- 添加 http basic auth（每個盤符可單獨配置用戶名和密碼，可以保護該盤下所有子文件和子文件夾）
- 添加網格視圖模式（文件預覽）
- 添加分頁加載
- 添加 i18n多國語言
- 添加 html渲染
- 添加 渲染文件夾/文件的描述 （用途自行挖掘）
- 添加可選配置
- 支持快速部署（幫助小白的利器）
- 支持PDF在線預覽
- 更換文本編輯器
- 解決url編碼問題 [#20](https://github.com/Aicirou/goindex-theme-acrou/issues/20) [#23](https://github.com/Aicirou/goindex-theme-acrou/issues/23) [#25](https://github.com/Aicirou/goindex-theme-acrou/issues/25)
- 解決其他已知問題

### v1.x

- 支持多盤切換
- 添加版本檢測
- 優化搜索結果
- 優化頁面顯示

## Lisense

[MIT](LICENSE)
