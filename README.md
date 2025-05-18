# vibe

This project is a simple trial for me to test if Cursor can help build a quick UI/UX demonstration page. With it, a system analyst like me can communicate with front-end web developer more efficiently.

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

## How it is created

The first version(2025-05-18) was created by Cursor with my scripts in Chinese. In the following version, I ckecked the code and modified it based on knowledge.

### Script for First Version

```
1. vibe: 

寫一些能夠DEMO心理諮商所診前問卷的網頁，流程如下：

第一頁：讓使用者輸入ID與生日並可按確認，假設輸入A123進入第二A頁，輸入B123進入第二B頁

第二A頁：顯示問卷組件A跟問卷組件B，可填寫並按確認送出

第二B頁：顯示問卷組件B，可填寫並按確認送出

第三頁：顯示問卷已成功送出

2. 限制：只用 Vue；純前端，不要接 API；問卷組件A跟問卷組件B實際是同一個組件，用參數控制標題及內容

3. UI風格：簡潔、可愛

4. 時限：20 分鐘應可完成，component 控制在 100 行內
```
Here is the English translation of the script only for readers and not for Cursor:

```
1. vibe: 

Build a simple front-end demo for a psychological counseling clinic's pre-consultation questionnaire.

2. Flow:

Page 1: Let the user input an ID and birthday, then click "Confirm".

- If the input is "A123", go to Page 2A.
- If the input is "B123", go to Page 2B.

Page 2A: Show Questionnaire Component A and Questionnaire Component B; user can fill in and submit.
Page 2B: Show only Questionnaire Component B; user can fill in and submit.

Page 3: Show a "Submission Successful" confirmation page.

3. Constraints: 

- Use Vue only
- Front-end only; do not connect to any backend or API
- Questionnaire A and B are actually the same component, with props controlling the title and content

4. UI Style: 

- Clean and cute

5. Time Limit:

- Should be completable within 20 minutes
- Each component should stay under 100 lines
```

The result met my expectation for 80%.

- Page 1:

![Page_1](/public/img/screenshot_1.jpg "Page 1")

- page 2A:

![Page_2A](/public/img/screenshot_2.jpg "Page 2A")

- page 2B

![Page_2B](/public/img/screenshot_4.jpg "Page 2B")

- page 3

![Page_3](/public/img/screenshot_3.jpg "Page 3")

It seemed good, but there is a few mistakes due to my imprecise script. The submit button in page 2A and 2B should be independent from the forms. In addition, adding a 'return to page 1' button in page 3 can provide a more efficient way to test the whole flow.

As a result, I wrote a supplemental script in Chinese as follows:

```
進行以下修正：

1. 問卷組件不包含確認按鈕
2. 在二A頁跟二B頁的確認按鈕，獨立於組件之外
3. 第三頁應有返回首頁按鈕，讓使用者可回到第一頁
```

Its translation for readers is:

```
Make the following changes:

1. The questionnaire components do not include a confirmation button.

2. The confirmation buttons on pages 2A and 2B are separate from the components.

3. Page 3 should have a “Back to Home” button that allows the user to return to page 1.
```

The result is shown as follows:

![Page_2A_1](/public/img/screenshot_5.jpg "Page 2A modified")

![Page_3_1](/public/img/screenshot_6.jpg "Page 3 modified")

Now the basic flow is exactly what I want. To demonstrate the situation that a patient can't fill in questionnaire due to a uncompleted registration, I added extra scripts in Chinese. 

```
1. 做一個navigator，包含2個tab：掛號、診前問卷

2. 點按掛號tab時，顯示掛號組件，可維持空白

3. 點按診前tab時，將上述第一到三頁包裝成組件顯示

4. 當診前問卷第一頁輸入C123並確認時，顯示提示訊息：請先掛號，並跳回掛號tab
```

Here is its English translation for readers.

```
1. Create a navigator with 2 tabs: "Registration" and "Pre-Consultation Questionnaire"

2. When the "Registration" tab is clicked, show the Registration component, which can remain empty

3. When the "Pre-Consultation Questionnaire" tab is clicked, display the previously described pages 1 to 3 wrapped as a component

4. When the user inputs "C123" on the first page of the questionnaire and confirms, show an alert message: "Please register first", then switch back to the "Registration" tab

```

Here is the result:

![Page_1_1](/public/img/screenshot_8.jpg "Page 1 modified")

![Page_1_2](/public/img/screenshot_7.jpg "Page 1 new tab")