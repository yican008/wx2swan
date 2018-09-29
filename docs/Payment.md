# 简介

为了方便开发者一站式快速接入多种支付渠道（如支付宝、微信、百度钱包等），我们提供了聚合收银台。聚合收银台调起后效果如下图，您也可以使用百度App扫描右侧二维码亲自体验。

![图片](https://ws4.sinaimg.cn/large/006tNbRwly1fvlujljc25j30dw0bymy6.jpg)

# 接入流程
## 申请入驻
[点此前往入驻](http://u.nuomi.com/)

![图片](https://ws2.sinaimg.cn/large/006tNbRwly1fvlul91vbsj31kw0twawx.jpg)

## 资质认证
认证资料提交后，进入人工审核，审核周期约 3 个工作日。

![图片](https://ws4.sinaimg.cn/large/006tNbRwly1fvlulnweo3j31kw0uk0x2.jpg)

## 开发者信息设置
设置开发者公钥和收银台参数。

![图片](https://ws1.sinaimg.cn/large/006tNbRwly1fvlumd8cw9j31kw0voq9a.jpg)

**Tip:** 变更参数，需要重新提交审核。

## 创建服务
![图片](https://ws4.sinaimg.cn/large/006tNbRwly1fvlumxqi9mj31kw0xggve.jpg)

填写服务信息后，提交平台进行服务审核，审核周期约 1 个工作日，审核通过后服务即可上线。

# 支付流程

1、小程序中调用 `swan.request`请求业务方后台。
2、业务方后台创建自己的订单后，返回 `orderInfo`。
3、小程序调用 `swan.requestPolymerPayment`调起聚合收银台发起支付。
4、百度通知业务方后台订单支付结果。

以上流程（1、2、3）前端示例代码如下：
```
swan.request({
    url: 'https://mbd.baidu.com/ma/nuomi/createorder', // 业务方订单创建接口
    success: res => {
        let data = res.data;
        swan.requestPolymerPayment({
            orderInfo: data.data,
            success(res) {
                // 支付成功
            },
            fail(err) {
                // 支付失败
            }
        });
    }
});
```

# 常见问题

### swan.requestPolymerPayment 是否可用于判断最终支付结果
success 回调只在用户支付成功后返回，可用于判断最终支付结果。

### 常见的错误码有哪些
请参考 [常见的错误码整理](https://dianshang.baidu.com/platform/doclist/index.html#!/doc/nuomiplus_3_business/mini_program_cashier/error_code.md)
