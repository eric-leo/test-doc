> # TalkingData 风险侦测服务接入文档

> ## 关键定义 ##

> TalkingData SDK: TalkingData提供的app统计分析、游戏统计分析、广告统计分析、风险侦测等业务能力的数据采集工具

> TalkingData SDMK: TalkingData智能数据服务商城

> TalkingData风险侦测服务: 基于大数据和AI技术、海量设备数据，TalkingData研发的对贷款申请风险进行实时侦测判别的服务，当前风险侦测接口支持过去三个月的数据回测

### 侦测欺诈请求，并返回风险分
#### Request

Url:                `http://dataapp.tendcloud.com/api/v1/risk/detect`  
Http method： `POST`  
Post Body: 
              
```json 
{
    "appId": "mime-xxxxx",          // Required; appId需要向TalkingData申请开通应用
    "riskServiceVersion": "1.0",    // Required; TalkingData风险侦测服务的版本
    "imei": "86332803****469",      // Required with imei, 待侦测设备的imei（适用于Android平台，双卡取第一个imei）
    "tdid": "xxx",                  // TalkingData设备id, 需要集成TalkingData SDK或者请求TalkingData SDMK的IDMapping服务得到
    "idfa": "xxxxxxxx",             // Required with idfa, 待侦测设备的idfa（适用于iOS平台）
    "ip": "",                       // 设备当前的IP地址
    "mac": "",                      // 设备的mac地址
    "wifiMac": "",                  // 设备的wifi mac地址
    "imsi": "",                     // 设备的imsi地址（双卡取第一个imsi）
    "idCard": "",                   // 设备用户的身份证号
    "personName": "",               // 设备用户的姓名
    "phone": "",                    // 设备用户的手机号
    "bankCard": "",                 // 设备用户的银行卡号
    "email": "",                    // 设备用户的邮箱地址
    "address": "",                  // 设备用户的地址
    "eventTime": 1493611932000,     // 事件时间(单位：毫秒), 如果不传, 则为请求的当前时间
    "eventType": 1,                 // 1="申请",2="激活",3="登录",4="支付",5="注册"
    "platformId": 1,                // 1="Android",2="iOS",3="WindowsPhone",4="HTML5"
    "extraFields": {                // 附加字段
      "k1": "v1"
    }
}
```

#### Response

```json
{
    "status": 2000,   // 2000="Success.";4000="Invalid Argument.";4001="Unauthorized.";5000="Service Internal Error."
    "message": "",
    "data": {
        "requestId": "0711030e-2c2d-4794-a2e3-0724103cf399", // 本次侦测请求的序列号
        "riskScore": 0,   // 设备的欺诈风险分，0～100，分数越高风险越高
        "riskResultCode": "PASS",   // 风险处置建议en. "PASS"="通过";"REJECT"="拒绝";"PEND"="待评估"
        "riskResultName": "通过",   // 风险处置建议cn. 通过, 拒绝, 待评估
        "detectTime": 1505281051041 // 侦测时间 
    },
    "ok": true
}
```

#### 侦测欺诈请求，并返回详情
Url:                `http://dataapp.tendcloud.com/api/v1/risk/detect/detail`  
Http Method: `POST `   
Post Body:   
            
```json
{
    "appId": "mime-xxxxx",          // Required; appId需要向TalkingData申请开通应用
    "riskServiceVersion": "1.0",    // Required; TalkingData风险侦测服务的版本
    "imei": "86332803****469",      // Required with imei, 待侦测设备的imei（适用于Android平台，双卡取第一个imei）
    "tdid": "xxx",                  // TalkingData设备id, 需要集成TalkingData SDK或者请求TalkingData SDMK的IDMapping服务得到
    "idfa": "xxxxxxxx",             // Required with idfa, 待侦测设备的idfa（适用于iOS平台）
    "ip": "",                       // 设备当前的IP地址
    "mac": "",                      // 设备的mac地址
    "wifiMac": "",                  // 设备的wifi mac地址
    "imsi": "",                     // 设备的imsi地址（双卡取第一个imsi）
    "idCard": "",                   // 设备用户的身份证号
    "personName": "",               // 设备用户的姓名
    "phone": "",                    // 设备用户的手机号
    "bankCard": "",                 // 设备用户的银行卡号
    "email": "",                    // 设备用户的邮箱地址
    "address": "",                  // 设备用户的地址
    "eventTime": 1493611932000,     // 事件时间(单位：毫秒), 如果不传, 则为请求的当前时间
    "eventType": 1,                 // 1="申请",2="激活",3="登录",4="支付",5="注册"
    "platformId": 1,                // 1="Android",2="iOS",3="WindowsPhone",4="HTML5"
    "extraFields": {                // 附加字段
      "k1": "v1"
    }
}
```

#### Response

```json
{
    "status": 2000,  // 2000="Success.";4000="Invalid Argument.";4001="Unauthorized.";5000="Service Internal Error."
    "message": "",
    "data": {
        "requestId": "98f9adf9-ca77-4941-86ca-c5675bd6149e",    // 本次侦测请求的序列号
        "riskScore": 0,                                         // 设备的欺诈风险分，0～100，分数越高风险越高
        "riskResultCode": "PASS",                               // 风险处置建议en. "PASS"="通过";"REJECT"="拒绝";"PEND"="待评估"
        "riskResultName": "通过",                               // 风险处置建议cn. 通过,拒绝,待评估
        "detectTime": 1505900739803,                            // 侦测时间 
        "portrait": {
            "loanapply": {
                "code": "loanapply",
                "name": "贷款申请核验",
                "featureValues": {
                    "cZI": {
                        "code": "cZI",
                        "name": "近1天，同一设备贷款申请的机构数量",
                        "value": 1,
                        "abnomralState": "0"
                    },
                    "cZK": {
                        "code": "cZK",
                        "name": "近1天，同一设备贷款申请的次数",
                        "value": 1,
                        "abnomralState": "0"
                    },
                    "bZU": {
                        "code": "bZU",
                        "name": "近1天，同一设备贷款申请的用户数量",
                        "value": 1,
                        "abnomralState": "0"
                    }
                }
            },
            "app": {
                "code": "app",
                "name": "APP使用核验",
                "featureValues": {
                    "bGs": {
                        "code": "bGs",
                        "name": "近1月，支付类app安装数",
                        "value": 2,
                        "abnomralState": "0"
                    }
                }
            },
            "registerlogin": {
                "code": "registerlogin",
                "name": "注册登录核验",
                "featureValues": {
                    "cZM": {
                        "code": "cZM",
                        "name": "近1天，同一设备注册的次数",
                        "value": 0,
                        "abnomralState": "0"
                    },
                    "cZO": {
                        "code": "cZO",
                        "name": "近1天，同一设备注册的机构数量",
                        "value": 0,
                        "abnomralState": "0"
                    },
                    "bZ0": {
                        "code": "bZ0",
                        "name": "近1天，同一设备的注册用户数量",
                        "value": 0,
                        "abnomralState": "0"
                    },
                    "bZ3": {
                        "code": "bZ3",
                        "name": "近1天，同一设备登录的用户数量",
                        "value": 0,
                        "abnomralState": "0"
                    },
                    "cZQ": {
                        "code": "cZQ",
                        "name": "近1天，同一设备登录的次数",
                        "value": 0,
                        "abnomralState": "0"
                    },
                    "cZS": {
                        "code": "cZS",
                        "name": "近1天，同一设备登录的机构数量",
                        "value": 0,
                        "abnomralState": "0"
                    }
                }
            },
            "device": {
                "code": "device",
                "name": "设备核验",
                "featureValues": {
                    "bZx": {
                        "code": "bZx",
                        "name": "近1月，出现的省份数",
                        "value": 1,
                        "abnomralState": "0"
                    },
                    "bZo": {
                        "code": "bZo",
                        "name": "近1月，设备报活的天数",
                        "value": 11,
                        "abnomralState": "0"
                    },
                    "bZn": {
                        "code": "bZn",
                        "name": "近1周，设备报活的天数",
                        "value": 0,
                        "abnomralState": "1"
                    },
                    "aAI": {
                        "code": "aAI",
                        "name": "近1月，设备关联的IP地址数量",
                        "value": 19,
                        "abnomralState": "0"
                    },
                    "aAH": {
                        "code": "aAH",
                        "name": "近3周，设备关联的IP地址数量",
                        "value": 7,
                        "abnomralState": "0"
                    },
                    "bZC": {
                        "code": "bZC",
                        "name": "近1月，出现的城市数",
                        "value": 3,
                        "abnomralState": "0"
                    },
                    "bZB": {
                        "code": "bZB",
                        "name": "近3周，出现的城市数",
                        "value": 3,
                        "abnomralState": "0"
                    },
                    "bZw": {
                        "code": "bZw",
                        "name": "近3周，出现的省份数",
                        "value": 1,
                        "abnomralState": "0"
                    }
                }
            },
            "overload": {
                "code": "overload",
                "name": "多头核验",
                "featureValues": {
                    "bQt": {
                        "code": "bQt",
                        "name": "近1月，贷款类app安装数",
                        "value": 4,
                        "abnomralState": "0"
                    },
                    "bYK": {
                        "code": "bYK",
                        "name": "近1月，微小贷款额度app安装数",
                        "value": 4,
                        "abnomralState": "0"
                    },
                    "bEz": {
                        "code": "bEz",
                        "name": "近1月，银行类app安装数",
                        "value": 5,
                        "abnomralState": "0"
                    },
                    "bY2": {
                        "code": "bY2",
                        "name": "近1月，中等贷款额度app安装数",
                        "value": 2,
                        "abnomralState": "0"
                    },
                    "bYB": {
                        "code": "bYB",
                        "name": "近1月，小贷款额度app安装数",
                        "value": 1,
                        "abnomralState": "0"
                    },
                    "bX1": {
                        "code": "bX1",
                        "name": "近1月，短贷款期限app安装数",
                        "value": 1,
                        "abnomralState": "0"
                    },
                    "bYa": {
                        "code": "bYa",
                        "name": "近1月，超短贷款期限app安装数",
                        "value": 3,
                        "abnomralState": "0"
                    },
                    "bVQ": {
                        "code": "bVQ",
                        "name": "近1月，金融理财app安装数",
                        "value": 17,
                        "abnomralState": "1"
                    },
                    "bXS": {
                        "code": "bXS",
                        "name": "近1月，中等贷款期限app安装数",
                        "value": 2,
                        "abnomralState": "1"
                    }
                }
            }
        }
        
    },
    "ok": true
}
```

