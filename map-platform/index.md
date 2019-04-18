# 地图平台工具包

### 介绍
包含简单的百度云地图、QQ地图、高德地图解析对象。

### 封装方法
1. 地址解析
2. 批量距离计算
3. IP定位

### 安装教程

在VS中，使用NuGet给对应项目安装组件[[NuGet组件](https://www.nuget.org/packages/Maplatform/)]

### 使用说明

1. 地址解析

使用SafelyMapManager类提供的GetPlatform方法, 再通过IMaplatform接口调用Geocoder方法实现地址解析


```C#
IMaplatform baidu = SafelyMapManager.GetPlatform(Model.Platform.BAIDU, "获取相应平台秘钥KEY");
var result = baidu.Geocoder("详细地址", "城市名称");
```

参数说明

GetPlatform方法

| 参数 | 是否必传 | 说明 |
| ---- | :----: | ---- |
| 参数一 | 是 | 根据提供的Model.Platform枚举类，调用BAIDU、QQ、GAODE |
| 参数二 | 是 | 地图平台秘钥KEY |

Geocoder方法

| 参数 | 是否必传 | 说明 |
| ---- | :----: | ---- |
| 参数一 | 是 | 详细地址 |
| 参数二 | 否 | 城市名称 (传空字符串) |
| 其它参数 | 否 | 根据地图平台地址解析查看 |

正确时返回的JSON数据包如下

```json
{
    "Status": 0,
    "AddressComponents": {
	    "Province": "上海市",
	    "City": "上海市",
	    "District": "黄浦区"
    },
    "Location": {
	    "Lat": 31.2272940412404,
	    "Lng": 121.484735788434
    }
}
```


2. 批量距离计算

使用SafelyMapManager类提供的GetPlatform方法, 再通过IMaplatform接口调用BatchCalculation方法实现地址解析

```C#
IMaplatform baidu = SafelyMapManager.GetPlatform(Model.Platform.BAIDU, "获取相应平台秘钥KEY");
var result = baidu.BatchCalculation(Model.Calculation.DRIVING, "起点坐标", "终点坐标");
```


参数说明

GetPlatform方法的使用（同上地址解析）

BatchCalculation方法

| 参数 | 是否必传 | 说明 |
| ---- | :----: | ---- |
| 参数一 | 是 | 根据提供的Model.Calculation枚举类，调用DRIVING (驾车)、WALKING (步行) |
| 参数二 | 是 | 起点坐标：包装经纬度属性类传参 (只支持一个坐标点) |
| 参数三 | 是 | 终点坐标：包装经纬度属性列表类传参 (支持多个坐标点) |
| 其它参数 | 否 | 根据地图平台距离测量查看 |

正确时返回的JSON数据包如下

```json
{
    "Status": 0,
    "Result": [{
	    "Distance": {
	        "Text": "52.6公里",
	        "Value": 52647
	    },
	    "Duration": {
	        "Text": "33分钟",
	        "Value": 1974
	    }
    }, {
	    "Distance": {
	        "Text": "54.4公里",
	        "Value": 54435
	    },
	    "Duration": {
	        "Text": "34分钟",
	        "Value": 2041
	    }
    }]
}
```
3. IP定位

使用SafelyMapManager类提供的GetPlatform方法, 再通过IMaplatform接口调用IP方法实现IP定位

```C#
IMaplatform baidu = SafelyMapManager.GetPlatform(Model.Platform.BAIDU, "获取相应平台秘钥KEY");
var result = baidu.IP("114.247.50.2");
```


参数说明

GetPlatform方法的使用（同上地址解析）

IP方法

| 参数 | 是否必传 | 说明 |
| ---- | :----: | ---- |
| 参数一 | 是 | IP地址 |
| 其它参数 | 否 | 根据地图平台IP定位查看 |

正确时返回的JSON数据包如下

```json
{
    "Status": 0,
    "Province": "北京市",
    "City": "北京市",
    "Location": {
        "Lat": 39.91488908,
        "Lng": 116.40387397
    }
}
```
