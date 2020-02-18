# Java-WebService-
Java 调用 WebService接口
# Java 调用 WebService接口

[调用天气例子](https://blog.csdn.net/weixin_30437847/article/details/99450909)

## 1、在浏览器中输入接口URL+?wsdl

接口URL：**http://www.webxml.com.cn/WebServices/WeatherWebService.asmx

浏览器中输入：**http://www.webxml.com.cn/WebServices/WeatherWebService.asmx?wsdl** 

## 2、F12 复制网页源代码

![复制这里](..\images\copyCode.png)

## 3、在IDEA项目中src自定义目录下新建文件**.wsdl文件

<img src="..\images\newFile.png" alt="新建wsdl文件" style="zoom:150%;" />

## 4、将复制的内容粘贴到文件内，并更改其中代码

将 所有的  <s:element ref="s:schema" />  改成   <s:any minOccurs="2" maxOccurs="2" />  并删掉  <s:any />

![](..\images\replace.png)

## 5、自动生成接口类

![生成](..\images\generate.png)

![](..\images\sel.png)

![](..\images\success.png)

## 6、实例化接口类，调用接口方法

```java
@Controller
@RequestMapping(path = "/weather")
public class TestWebServiceController {
    @RequestMapping(path = "/test")
    public void test() throws Exception {
        //实例化接口类
        WeatherWebService weatherWebService = new WeatherWebServiceLocator();  
        
        //查看接口URL
        String weatherWebServiceSoapAddress = weatherWebService.getWeatherWebServiceSoapAddress();
        System.out.println(weatherWebServiceSoapAddress);
        //先获得Soap类 getWeatherWebServiceSoap()
        WeatherWebServiceSoap_PortType weatherWebServiceSoap = weatherWebService.getWeatherWebServiceSoap();
        //调用其中接口方法
        String[] s = weatherWebServiceSoap.getWeatherbyCityName("西安");
        //处理返回值
        for (int i= 0; i<s.length;i++){
            System.out.println(s[i]);
        }
    }
}
```

