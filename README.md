# HttpUtil
&emsp;Java 网络请求工具类，支持异步请求，支持传递 header ，支持表单和 json 类型的参数提交。

> 包含两个工具类，一个`HttpUtil`一个`HttpBaseUtil`，一个依赖Spring，一个不依赖任何框架。

## HttpUtil
&emsp;&emsp;依赖于`Spring`框架，如果你的项目基于`Spring`或者`SpringBoot`，推荐使用此工具类。

**使用示例：**
```java
public class Test{
    public void test(){
        // get请求
        String res = HttpUtil.get("https://baidu.com", null);
        System.out.println(res);
        
        // 带参数
        MultiValueMap<String, String> params = new LinkedMultiValueMap<>();
        params.add("name", "hahaha");
        String res = HttpUtil.get("https://baidu.com", params);
        System.out.println(res);
        
        // json参数提交
        User params = new User();
        String res = HttpUtil.request("https://baidu.com", params, null, HttpMethod.POST, MediaType.APPLICATION_JSON);
        System.out.println(res);
        
        // 更多使用方法看源码中的注释
    }
}
```

[查看全部使用方法](https://gitee.com/whvse/HttpUtil/blob/master/HttpUtil.java)

<br>

## HttpBaseUtil
&emsp;&emsp;不依赖于任何框架，使用`HttpURLConnection`实现，支持异步请求方式。

**使用示例：**
```java
public class Test{
    public void test(){
        // get请求
        String res = HttpBaseUtil.get("https://baidu.com", null);
        System.out.println(res);
        
        // 带参数
        Map<String, String> params = new HashMap<>();
        params.add("name", "hahaha");
        String res = HttpUtil.get("https://baidu.com", params);
        System.out.println(res);
        
        // 异步请求
        System.out.println("开始请求...." + System.currentTimeMillis());
        HttpBaseUtil.getAsyn("https://baidu.com", null, new OnHttpResult() {
            @Override
            public void onSuccess(String result) {
                System.out.println("请求结束...." + System.currentTimeMillis());
                System.out.println(result);
            }

            @Override
            public void onError(String message) {
                System.out.println(message);
            }
        });
        System.out.println("---我来证明请求是异步的---");
        
        // json参数提交
        User user = new User();
        String params = JSON.toJSONString(user);
        String res = HttpBaseUtil.request("https://baidu.com", params, null, "POST", "application/json");
        System.out.println(res);
        
        // 更多使用方法看源码中的注释
    }
}
```
 
[查看全部使用方法](https://gitee.com/whvse/HttpUtil/blob/master/HttpBaseUtil.java)
