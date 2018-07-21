---
layout:     post
title:      "WeChat Mini Program Login"
date:       2016-10-28 13:00:00
author:     "Shi"
---

# Login, UserInfo and CheckSession Process:

https://github.com/IvinWu/weRequest

1. wx.checkSession 

   success: 

2. wx.login

3. wx.getUserInfo

4. Send `code, encryptedData, iv ` to server

# Login 

Weixin app api can return user's nickname and avatar, but not its openid

## **wx.login**()

https://developers.weixin.qq.com/miniprogram/dev/api/api-login.html

### Returns:

```
{
      "openid": "OPENID",
      "session_key": "SESSIONKEY",
}
```



#### **session_key**

1. session_key is the key to decode user's data
2. Everytime wx.login() called, session_key will be updated
3. wx.checkSession() to check if session is valid

## Steps:

1. Client: `wx.login()` to get `temporaryCode` (is called `code` in weixin's api return value, and it can be used onece only)

2. Client: Send  `temporaryCode`  to server

3. Server: Send appid+appsecret+temporaryCode to Weixin's server, Weixin's server returns **session_key** (salt of `temporaryCode`) and **openid** (openid is the unique Weixin user id)

   ```
   https://api.weixin.qq.com/sns/jscode2session?appid=APPID&secret=SECRET&js_code=temporaryCode&grant_type=authorization_code
   ```

4. Server: return `3rd_session (token; selfDefinedLoginStatus)` (maybe can be the same as `openid` ) that generated according to `session_key` and `openid` to client. 

   ```
   {
       openid,
       session_key,
       expires_in,
   }
   ```

5. Client: Store  `3rd_session (token)` in persistence 

6. Client: Do request with   `3rd_session(token)` 

7. Server: Check if user can do request with  `3rd_session(token)` 



Note:  Weixin nickName code format is ISO-8859-1, you can convert it with:

```
String nickNameDecode = new String(nickName.getBytes("ISO-8859-1"),"utf-8");
```


## Java Backend

Good version： https://my.oschina.net/magicalSam/blog/832895

juejin version: https://juejin.im/post/5ac9b72cf265da23906c486a

Simple version：https://my.oschina.net/ZhenyuanLiu/blog/1838069

https://blog.csdn.net/weixin_40099554/article/details/80003058



# UserInfo


## **wx.getUserInfo()**

https://developers.weixin.qq.com/miniprogram/dev/api/open.html#wxgetuserinfoobject

**注意：此接口有调整，使用该接口将不再出现授权弹窗，请使用 **`<button open-type="getUserInfo"></button> `**引导用户主动进行授权操作**

###  getUserInfo return :

```
{
    userInfo,
    rawData,
    signature,
    encryptedData,
    iv
}
```

userInfo contains:

```
{
  "nickName": "Band",
  "encryptedData": 1,
  "language": "zh_CN",
  "city": "Guangzhou",
  "province": "Guangdong",
  "country": "CN",
  "avatarUrl": "http://wx.qlogo.cn/mmopen/vi_32/1vZvI39NWFQ9XM4LtQpFrQJ1xlgZxx3w7bQxKARol6503Iuswjjn6nIGBiaycAjAtpujxyzYsrztuuICqIM5ibXQ/0"
}
```



We should use  `session_key` , `iv` to decrypt `encryptedData`

```
{
    "openId": "OPENID",
    "nickName": "NICKNAME",
    "gender": GENDER,
    "city": "CITY",
    "province": "PROVINCE",
    "country": "COUNTRY",
    "avatarUrl": "AVATARURL",
    "unionId": "UNIONID",
    "watermark": {
      "appid":"APPID",
      "timestamp":TIMESTAMP
    }
}
```

 

## access_token

access_token 是全局唯一接口调用凭据，开发者调用各接口时都需使用 access_token

https://developers.weixin.qq.com/miniprogram/dev/api/token.html#%E8%8E%B7%E5%8F%96-access_token

https://developers.weixin.qq.com/miniprogram/dev/api/signature.html#wxchecksessionobject

## Example

https://www.cnblogs.com/nosqlcoco/p/6105749.html

https://blog.csdn.net/qq_37848203/article/details/72763837

### App decode request

```
//httpclient.req(url, data, method, success, fail)
httpclient.req(
'http://localhost:8090/wxappservice/api/v1/wx/decodeUserInfo',
  {
    apiName: 'WX_DECODE_USERINFO',
    encryptedData: this.data.encryptedData,
    iv: this.data.iv,
    sessionId: wx.getStorageSync('thirdSessionId')
  },
  'GET',
  function(result){
  //解密后的数据
    console.log(result.data)
  },
  function(result){
    console.log(result)
  }
);
```

### Server side

```
/**
 * 解密用户敏感数据
 * @param encryptedData 明文
 * @param iv            加密算法的初始向量
 * @param sessionId     会话ID
 * @return
 */
@Api(name = ApiConstant.WX_DECODE_USERINFO)
@RequestMapping(value = "/api/v1/wx/decodeUserInfo", method = RequestMethod.GET, produces = "application/json")
public Map<String,Object> decodeUserInfo(@RequestParam(required = true,value = "encryptedData")String encryptedData,
        @RequestParam(required = true,value = "iv")String iv,
        @RequestParam(required = true,value = "sessionId")String sessionId){

    //从缓存中获取session_key
    Object wxSessionObj = redisUtil.get(sessionId);
    if(null == wxSessionObj){
        return rtnParam(40008, null);
    }
    String wxSessionStr = (String)wxSessionObj;
    String sessionKey = wxSessionStr.split("#")[0];

    try {
        AES aes = new AES();
        byte[] resultByte = aes.decrypt(Base64.decodeBase64(encryptedData), Base64.decodeBase64(sessionKey), Base64.decodeBase64(iv));
        if(null != resultByte && resultByte.length > 0){
            String userInfo = new String(resultByte, "UTF-8");
            return rtnParam(0, userInfo);
        }
    } catch (InvalidAlgorithmParameterException e) {
        e.printStackTrace();
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
    }
    return rtnParam(50021, null);
}
```

https://developers.weixin.qq.com/miniprogram/dev/demo/aes-sample.zip