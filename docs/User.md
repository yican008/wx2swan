# 背景
由于百度App不会强制用户登录百度账号，因此使用小程序的人很可能处于未登录状态。
那么便存在以下问题：

1、如何标识一个未登录的用户。
2、开发者如何将百度用户和自己帐户体系关联起来。

为便于开发者解决以上问题，我们设计了 `swanid` 及 `openid`，预计10月中旬上线。

# 名词解释
## swanid
`swanid` 是根据用户设备生成的标识。`swanid` 具有以下特征：

1、用户在同一台设备上使用同一个开发者所开发的不同智能小程序，得到的是相同的 `swanid`。
2、用户在同一台设备上使用不同开发者所开发的不同智能小程序，得到的`swanid`是不同的。
## openid
`openid`是根据用户的百度帐号生成的标识，openid只与用户的百度帐号有关，可以唯一标识一个百度用户。

# 获取方法
## swanid
```javasscript
swan.getSwanId({
    success(res) {
        console.log(res.data.swanid);
    }
});
```

## openid
获取到openid的前提是当前用户已登录百度帐号，具体步骤如下：

1、调用 `swan.login` 获取 临时登录凭证code ，并回传到开发者服务器；
2、开发者服务器以 `code` 换取 `session_key`；
3、调用 `swan.getUserInfo` 获取用户信息。
4、将获取到的加密数据`data`通过 `swan.request`回传至开发者服务器进行对称解密，便可以获取到`openid`了。

以上步骤的前端示例代码如下：

```
Page({
    data: {
        openid: ''
    },

    login() {
        let self = this;
        swan.checkSession({
            success(res) {
                self.getOpenId();
            },
            fail(err) {
                swan.login({
                    success(res) {
                        swan.request({
                            url: 'https://xxx/xxx', // 开发者服务器地址，用 code 换取 session_key
                            data: {
                                code: res.code
                            },
                            method: 'POST',
                            success: res => {
                                self.getOpenId();
                            }
                        });
                    }
                });
            }
        });
    },

    getOpenId(data) {
        let self = this;
        swan.getUserInfo({
            success(res) {
                swan.request({
                    url: 'https://xxx/xxx', // // 开发者服务器地址，对 data 进行解密
                    data: res.data,
                    success(res) {
                        // 开发者服务器解密后返回 openid
                        self.setData({
                            openid: res.data.data.openid
                        });
                    }
                });
            }
        });
    }
});
```