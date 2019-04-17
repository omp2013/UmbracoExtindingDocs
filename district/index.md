# Umbraco Extending District #

### 介绍
UE.District组件是基于Umbraco CMS自定义开发的Data Types三级联动

### 基本要求

* Umbraco 7.14.0

* .NETFramework 4.5.2+

### 使用说明

1. 在VS中，创建项目并使用NuGet安装Umbraco 7.14.0
2. 在VS中，继续使用NuGet安装[UE.District组件](https://www.nuget.org/packages/UmbracoExtending.District)到创建的Umbraco 7.14.0项目中
3. 发布站点并部署到IIS，浏览站点进行安装CMS

4. 站点安装完成，将项目中`App_Data\ueDistrict.sql`导入到本项目的数据库中`[1]`

5. 进入CMS后台创建Data Types`[2]` `[3]`, 如下图所示：

    ![image](https://raw.githubusercontent.com/omp2013/UmbracoExtindingDocs/master/district/images/DataTypes.jpg)

6. 进入Settings -- 创建Document Types调用创建的三级联动Data Types

    ![image](https://raw.githubusercontent.com/omp2013/UmbracoExtindingDocs/master/district/images/doc_type.jpg)

7. 进入Content创建页面，如下图所示：

    ![image](https://raw.githubusercontent.com/omp2013/UmbracoExtindingDocs/master/district/images/Rendering.jpg)

8. Templates模板调用
```C#
var item = Model.Content.GetPropertyValue<string>("selections");
var obj = UmbracoExtending.District.DistrictUtil.ResolveDistrict(item);

省份：@obj.ProvinceName
城市：@obj.CityName
区域：@obj.DistrictName
```


### 备注

`[1]` 库中存在该表`[dbo].[umbracoExtendingDistrict]`，请忽略此步骤

`[2]` `Property editor` 选择Umbraco Extending District

`[3]` 默认是二级联动，选中`Three Tier` 则开启三级联动
