# vibe

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

1. vibe: 寫一些能夠DEMO心理諮商所診前問卷的網頁，流程如下：

第一頁：讓使用者輸入ID與生日並可按確認，假設輸入A123進入第二A頁，輸入B123進入第二B頁

第二A頁：顯示問卷組件A跟問卷組件B，可填寫並按確認送出

第二B頁：顯示問卷組件B，可填寫並按確認送出

第三頁：顯示問卷已成功送出

2. 限制：只用 Vue；純前端，不要接 API；問卷組件A跟問卷組件B實際是同一個組件，用參數控制標題及內容
3. UI風格：簡潔、可愛
4. 時限：20 分鐘應可完成，component 控制在 100 行內

===

進行以下修正：

1. 問卷組件不包含確認按鈕
2. 在二A頁跟二B頁的確認按鈕，獨立於組件之外
3. 第三頁應有返回首頁按鈕，讓使用者可回到第一頁

===

1. 做一個navigator，包含2個tab：掛號、診前問卷

2. 點按掛號tab時，顯示掛號組件，可維持空白

3. 點按診前tab時，將上述第一到三頁包裝成組件顯示

4. 當診前問卷第一頁輸入C123並確認時，顯示提示訊息：請先掛號，並跳回掛號tab