## TalkingData 风险侦测服务接入示例代码
              
```java 
import com.alibaba.fastjson.JSONObject;
import com.talkingdata.client.TDClient;
import com.talkingdata.client.config.TDSetting;
import com.talkingdata.client.constant.HttpConstants;
import com.talkingdata.client.entity.Request;

import java.io.IOException;
import java.net.URISyntaxException;
import java.util.HashMap;

/**
 * 调用欺诈侦测服务，并返回欺诈分以及风险画像
 */
public class RiskDetectDetail {

    public static void main(String... args) throws IOException, URISyntaxException {
        //填入你的apikey 以及 apiToken
        String apiKey = "";
        String apiToken = "";

        TDSetting.setting(apiKey, apiToken, "https://api.talkingdata.com/tdmkaccount/authen/app/v2");

        //更换需要访问的apiUrl
        String apiUrl = "https://api.talkingdata.com/data/api/v1/risk/detect/detail";
        String appId = ""; // 需要先向Talkingdata申请

        JSONObject jsonObject = new JSONObject();
        jsonObject.put("appId", appId);
        jsonObject.put("riskServiceVersion", "1.0");
        jsonObject.put("imei", "");
        jsonObject.put("tdid", "xxx");                  // Talkingdata设备id,需要集成Talkingdata SDK或者请求SDMK的IDMapping服务拿到
        jsonObject.put("idfa", "xxxxxxxx");             // Required with imei, 待侦测设备的IDFA（iOS）
        jsonObject.put("ip", "");                       // 设备当前的IP
        jsonObject.put("mac", "");                      // 设备的MAC地址
        jsonObject.put("wifiMac", "");                  // 设备的Wifi Mac地址
        jsonObject.put("imsi", "");                     // 设备的IMSI地址
        jsonObject.put("idCard", "");                   // 设备用户的身份证号
        jsonObject.put("personName", "");               // 设备用户的姓名
        jsonObject.put("phone", "");                    // 设备用户的手机号
        jsonObject.put("bankCard", "");                 // 设备用户的银行卡
        jsonObject.put("email", "");                    // 设备用户的邮箱地址
        jsonObject.put("address", "");                  // 设备用户的地址
        jsonObject.put("eventTime", 1493611932000L);     // 事件时间. 如果不传，则为请求的当前时间
        jsonObject.put("eventType", 1);                 // 1="申请",2="激活",3="登录",4="支付"
        jsonObject.put("platformId", 1);                // 1="Android",2="iOS",3="WindowsPhone",4="HTML5"
        jsonObject.put("eventTime", 1493698332000L);
        Request request = new Request(apiUrl, null, jsonObject.toJSONString(), HttpConstants.POST);
        HashMap resp = TDClient.request(request, HashMap.class);

        if (Integer.valueOf(resp.get("code").toString()) == 2000) {
            JSONObject data = (JSONObject) resp.get("data");
            System.out.println(data);
        } else {
            System.out.println("error: " + resp);
        }
    }
}
```