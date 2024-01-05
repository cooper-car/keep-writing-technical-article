## **API Response 設計**

### **Success**

```json
{
  "error": "",
  "message": "",
  "data": {
    "icon": "ryan.jpg",
    "name": "ryan is a lion"
  }
}

```

### **Error**

```json
{
  "error": "shop.userNotFound",
  "message": "User not found when attempting to perform shop-related operation."
}

```

```json
{
  "error": "product.userNotFound",
  "message": "User not found when attempting to perform product-related operation."
}

```
<hr>

### **前端處理**

```jsx
// 從 API response 中獲取錯誤相關信息
const errorIdentifier = apiResponse.error;
const [module, code] = errorIdentifier.split('.');

// 顯示對應模組和語言的錯誤訊息
const errorMessage = i18nMessages[userLanguage][module][code];
console.log(errorMessage);

```

### **前端多國語系結構**

### en.json

```json
{
  "product": {
    "userNotFound": "User not found when attempting to perform product-related operation."
  },
  "shop": {
    "userNotFound": "User not found when attempting to perform shop-related operation."
  }
}

```

### zh-tw.json

```json
{
  "product": {
    "userNotFound": "在執行與產品相關操作時找不到用戶。"
  },
  "shop": {
    "userNotFound": "在執行與商店相關操作時找不到用戶。"
  }
}

```

### **設計**

- 統一使用 `error` 字段表示錯誤信息。
- `error` 字段的值是模組和代碼的結合字符串，例如 `"shop.userNotFound"`。
- 在前端，根據 `error` 字串的分割來獲取模組和代碼，進而顯示對應的錯誤訊息。
- 前端多國語系檔案以模組為主，內部包含不同模組和代碼的語言版本。
- 這樣的設計方式簡單而具有可擴展性，同時允許前端根據模組和代碼來動態顯示不同語言的錯誤訊息。

### **Feedback**

- 上述用法是前端工程師之前的經驗
- 一個語系對應一個 json 檔

### 另一種前端檔案結構

- 一個語系對應一個 file
- 每個語系 file 下面對一個 module 的錯誤訊息

  ![img](<CleanShot 2024-01-06.jpg>)