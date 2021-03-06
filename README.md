# [MobPush API for Java](https://www.mob.com/wiki/detailed/?wiki=MobPushRestAPIfenlei1333&id=136)

![image](https://github.com/MOBX/MOB-SMS-WEBAPI/blob/master/doc/images/logo.png)

**[MobPush API for Java](https://www.mob.com/wiki/detailed/?wiki=MobPushRestAPIfenlei1333&id=136)** 
为了帮助开发者更方便接入MobPush免费推送SDK，提供完整的API接口的java实现，包含设备操作相关接口、推送操作相关接口以及公共接口。

了解更多 [MobPush 免费推送SDK.](https://www.mob.com/mobService/mobpush)


## 优势

**免费使用**、**自定义UI**、**稳定服务**、**流程体验**、**数据同步**、**专业技术团队服务**

# 接口
* 推送接口:
	* 广播推送 pushAll
    * 别名推送 pushByAlias
    * 用户标签推送 pushByTags
    * Registration ID推送 pushByRids
    * 复杂地理位置推送 pushByAreas
    * 用户自定义配置推送 pushTaskV3
    * 别名和rid批量推送 pushMulti         
* 推送任务详情查询接口
	* 查询推送任务详情(根据batchId) getPushByBatchId
	* 查询推送任务详情(根据workno) getPushByWorkno
* 推送任务的处理接口
    * 取消推送任务(根据workId) cancelPushTask
    * 替换推送任务(根据workId) replacePushTask
    * 撤回推送任务(根据workId) recallPushTask
* 查询推送统计接口
    * 根据推送任务id查询统计 getStatsByWorkId
    * 根据推送任务id批量查询统计 getStatsByWorkIds
    * 根据用户id查询统计 getStatsByWorkno
    * 按小时查询统计 getStatsByHour
    * 按日期查询统计 getStatsByDay
    * 根据id查询任务下发给设备的详情统计 getStatsByDevice
* 设备操作接口
    * 根据rid查询设备信息接口 getByRid
    * 查询设备分布情况 getDeviceDistribution
    * 根据别名查询设备信息 queryByAlias
    * 更新设备别名 updateAlias (updateByAlias已经废弃)
    * 更新设备标签 updateTags (upateByTags已经废弃)
    * 根据标签查询设备信息 queryByTags   




# 使用方式

* ## maven集成方式
    pom依赖:
```Java
<dependency>
  <groupId>com.mob.push.sdk</groupId>
  <artifactId>mobpush-websdkv3-java</artifactId>
  <version>2.0.0</version>
</dependency>
```
* ## 源码编译

    主要需要依赖httpclient.jar 、fastjson.jar,日志相关包
 
# 使用注意事项
* 初始化appkey、appSecret
```Java
   MobPushConfig.appkey = "";
   MobPushConfig.appSecret = "";
```
以上是使用时设置的方式，还可以直接引用源码在mob.push.api.MobPushConfig设置

* 错误码请参考 
  [MobPush Api 错误码](http://wiki.mob.com/mobpush-rest-api-接口文档/#map-6)



# 使用示例 

发送推送示例片段代码

```Java
MobPushConfig.appkey = "appkey";
MobPushConfig.appSecret = "appSecret";
try {
    //Registration ID推送
    Result<PushV3Res> resResult=PushV3Client.pushByRids("workNo","title","content","rid");
 catch (ApiException e) {
    e.getStatus();	   	   //错误请求状态码
    e.getErrorCode();	       //错误状态码
    e.getErrorMessage();        //错误信息 
    }
}
```

统计查询示例片段代码

```Java
MobPushConfig.appkey = "appkey";
MobPushConfig.appSecret = "appSecret";
try {
    //根据workId查询统计结果
    Result<StatsV3Res> resResult=StatsV3Client.getStatsByWorkId("workId");
 catch (ApiException e) {
    e.getStatus();	   	   //错误请求状态码
    e.getErrorCode();	       //错误状态码
    e.getErrorMessage();        //错误信息 
    }
}
```
*1.0.4版本相对于1.0.3版本新增了定速推送配置(PushNotify.speed)
*2.0.0版本相对于1.0.4版本去掉了updateByAlias,upateByTags无效方法
