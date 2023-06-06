# WeChat H5 Auth
WeChat H5 Auth helps you to easily create WeChat H5 authentication available for your user. 

# Features
- Official USER LOGIN REQUEST integration
- Using strapi default user-permission collection
- JWT Authentication
- Sanitized response
- Highly secure

# How to use
### STEP 1
Install the strapi plugin
> npm i strapi-wechat-h5-auth

### STEP 2
Add the folling lines of code in the file: config/plugins.js
```
module.exports = {
    // ...
    'strapi-wechat-h5-auth': {
        enabled: true
    },
    // ...
}
```
After done this, you can start the application with command:
> npm run develop

### STEP 3
- Config the WeChat AppID，AppSecret and redirct_url.

Go to the Strapi Dashboard, and change to the PLUGINS -> WeChat H5 Authenticator, input the AppID,AppSecret,redirect_url and save it.

- Add fileds to User Collection

Go to the Strapi Dashboard, and change to the User Collection(PLUGINS -> Content-Type Builder -> COLLECTION TYPES -> User).
Add two fields to this collection, and save.
|  NAME   | TYPE  |
|  ----  | ----  |
| openid  | Text |
| wechatUserInfo  | JSON |

### STEP 4

Use the getUserInfo button in your WeChat H5 to get the current userinfo

#### HTML

```html
<!-- use a tag go wx login -->
<a href="<STRAPI_BACKEND>/strapi-wechat-h5-auth/code">    
    <span>登录</span>
</a>
```

#### Javascript
Initialisation a request to STRAPI_BACKEND to get JWT token and Sanitized userinfo.

```javascript
// code from <FRONTEND>?code=xxxx
const urlParams = getUrlParams();
if(urlParams.code){
    $.ajax({
        type: 'POST',
        url: '<STRAPI_BACKEND>/strapi-wechat-h5-auth/login',
        data: {
            code: urlParams.code
        },
        success(response){
          // when get userinfo success
        }
    })
}
```

The STRAPI_BACKEND request response look like this:
```JSON
    {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjY3NTM3MzU5LCJleHAiOjE2NzAxMjkzNTl9.giRP146cEV0wyIh98D3KJigHShsEGofedtW5YYckzsQ",
      "user": {
        "id": 1,
        "username": null,
        "email": null,
        "provider": "local",
        "confirmationToken": null,
        "confirmed": true,
        "blocked": false,
        "createdAt": "2022-11-04T02:41:27.149Z",
        "updatedAt": "2022-11-04T02:41:27.149Z",
        "openid": "oFHxc5TV5VKscIudqlmfx9JpK4d4",
        "wechatUserInfo": {
          "nickName": "wfz",
          "gender": 0,
          "language": "zh_CN",
          "city": "",
          "province": "",
          "country": "",
          "avatarUrl": "https://A-WECHAT-AVATAR-LINK"
        }
      }
    }
```
You can using the JWT token in your application.

# Report Bugs/Issues
Any bugs/issues you may face can be submitted as issues in the Github repo.

Inspired by [/wfzong/strapi-wechat-miniprogram](https://github.com/wfzong/strapi-wechat-miniprogram-auth)
