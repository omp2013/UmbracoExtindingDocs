# Umbraco Extending Dealer #

### 介绍

UE.Dealer组件是基于Umbraco CMS所开发的经销商模块。支持与百度地图、腾讯地图等第三方平台整合的经销商管理功能。

### 基本要求

* Umbraco 7.14.0
* .NETFramework 4.5.2+

### 使用说明

1. 在VS中，创建项目并使用NuGet安装Umbraco 7.14.0
2. 在VS中，继续使用NuGet安装[UE.Dealer组件](https://www.nuget.org/packages/UmbracoExtending.Dealer)到创建的Umbraco 7.14.0项目中
3. 发布站点并部署到IIS，浏览站点进行安装CMS
4. 站点安装完成，检查本项目数据库中是否存在该表`[dbo].[umbracoExtendingDistrict]`，如果不存在，请将`App_Data\ueDistrict.sql`导入到库中，否则请忽略当前操作。同时，将`App_Data\ueDealer.sql`导入到库中。
5. 请用超级管理员用户，点击（Users）用户模块 -- 找到右上角Groups -- 点击权限组 -- （区域）Sections添加（Umbraco Extending Dealer）经销商模块权限
6. 打开IIS回收应用程序池，清理浏览器图片和文件缓存，进入CMS后台，重新强制刷新后台，左侧菜单会友好的显示经销商模块，如下图所示：

    ![image](https://raw.githubusercontent.com/omp2013/UmbracoExtindingDocs/master/dealer/images/menu.jpg)

7. 点击左侧Umbraco Extending Dealer菜单模块。
    ## 配置Configuration项

    > 1. 在Dealer List上右击鼠标，选择Configuration项
    > 2. 配置Platform，选择相应平台，
    > 3. 根据Platform选择的平台，填写对应平台的秘钥KEY


    ## 创建经销商 
    > 1. 在Dealer List上右击鼠标，选择Create Dealer创建经销商
    > 2. 填写地址(address), 门店名称（Store Name）保存即可

8. Templates模板调用
```C#
// 调用省份列表
var provinces = DealerUtil.GetProvinces();

<select class="form-control" id="province">
    <option>=请选择=</option>
    @foreach (var province in provinces)
    {
        <option value="@province.Code">@province.Name</option>
    }
</select>

// 根据省份触发城市列表接口地址
/umbraco/UmbracoDealer/FrontendDistrict/GetCitys

// 经销商接口地址
/umbraco/UmbracoDealer/FrontendDealer/GetDealers
```