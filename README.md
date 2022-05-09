# react proxy-setting

### Proxy


### React setting
+ 第三方proxy
  ```
  
  ```
+ webpack.config.js
  ```
  ```
+ setupProxy.js
  + 安裝 http-proxy-middleware
    ```
    yarn add http-proxy-middleware
    ```
  + 在專案下 src 建立 setupProxy.js 檔案 
    ```
    const { createProxyMiddleware } = require('http-proxy-middleware');

    module.exports = function (app) {
      app.use(
        '/test/annie/react-api',
        createProxyMiddleware({
          target: 'http://localhost:5000', // 要設置的網域
          changeOrigin: true,
        })
      );
    };
    ```
  + 重新 build 專案
    ```
    yarn run build
    ```
  + api 使用
    ```
    axios.get('/test/annie/react-api/itemlist')
      .then(response =>{
          return {
              itemList: response?.itemList,
          };
      })
      .catch(error=>{
          console.log(error)
      })
    ```
### Source
> [Proxying API Requests in Development](https://create-react-app.dev/docs/proxying-api-requests-in-development/)
> 
> [DAY06 - API串接常見問題 - CORS - 解決CORS問題篇](https://ithelp.ithome.com.tw/m/articles/10268821)
> 
