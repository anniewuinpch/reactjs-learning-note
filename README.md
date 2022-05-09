# react CORS 問題排除筆記

## JSONP
### 方法1: jsonp
+ 安裝套件
  ```
  yarn add jsonp
  ```
+ 使用
  ```
  import jsonP from 'jsonp';
  
  const URL = 'http://localhost:5000';  // 要設置的網域

  jsonP(
    `${URL}/test/annie/react-api/itemlist`,
    {
      param: 'callback',
    },
    function (err, response) {
      if (response) {
        resolve(response);
      } else {
        reject(response.message);
      }
    })
  ```

### axios-jsonp 
+ 方法2: 安裝套件
  ```
  yarn add axios-jsonp url
  ```
+ 使用
  ```
  import jsonpAdapter from 'axios-jsonp';
  
  const URL = 'http://localhost:5000';  // 要設置的網域
  
  return axios.get(`${URL}/test/annie/react-api/itemlist`,{ adapter: jsonpAdapter }
        .then(response =>{
            return {
                itemList: response?.itemList,
            };
        })
        .catch(error=>{
            console.log(error)
        })
  ```

## Proxy 代理伺服器
### React setting
+ 方法1: setupProxy.js (目前選用)
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
  + 若無抓到: 重新 build 專案
    ```
    yarn run build
    ```
+ 方法2: webpack.config.js
  + 安裝 dev server
    ```
    yarn add webpack webpack-cli webpack-dev-server
    ```
  + 設定proxy
    ```
    devServer: {
      proxy: [
        {
          context: ['/api'],
          target: 'http://localhost:5000',
          changeOrigin: true,
        },
      ],
    },
    ```
+ 方法3: 第三方 CORS Proxy
  ```
  const CORS_URL = 'https://cors-anywhere.herokuapp.com/'; // cors-anywhere
  const URL = 'http://localhost:5000';  // 要設置的網域
  
  axios.get(`${CORS_URL}${URL}`, {
      referrerPolicy: 'strict-origin-when-cross-origin',
      body: null,
      method: 'GET',
      mode: 'cors',
      credentials: 'omit',
      ...options.headers,
    })
    .then((response => {
      return {
                itemList: response?.itemList,
            };
    })
    .catch((error) => {
      console.log(error);
    });
  ```
### Source
> [Cross Domain Ajax 跨網域抓取資料(JSONP)](https://ithelp.ithome.com.tw/articles/10094915)
>  
> [DAY06 - API串接常見問題 - CORS - 解決CORS問題篇](https://ithelp.ithome.com.tw/m/articles/10268821)
> 
> [Proxying API Requests in Development](https://create-react-app.dev/docs/proxying-api-requests-in-development/)
