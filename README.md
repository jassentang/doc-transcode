## 文档转码 `COS公共桶` 转存到 `CAM存储桶` 方法
说明：文件转存后，转码结果也需要对应的修改，主要修改 `ResultUrl` 和 `ThumbnailUrl` 两个字段    
比如：没有转存前：ResultUrl: https://transcode-result-1259648581.file.myqcloud.com/ + taskid    
转存后变为：ResultUrl: https://你们的域名/ + taskid

#### 第一步：配置好 [CAM存储桶](https://cloud.tencent.com/document/product/1137/45256)
#### 第二步：确认需要转存的 时间间隔（最大支持3个月内（从当前日期算起））、文档转码的 sdkappid、文档转码类型（静态/动态）
#### 第三步：根据用户是否 配置了回调，分为两种
##### 1. 配置了转码回调：
接收新的文档转码回调事件，根据回调中的 taskid，修改用户数据库中的 转码结果（只会有 TranscodeFinished 事件）
> 说明：
> 腾讯这边，会根据用户提供的 时间段 和 转码类型，将转码文件 --> 转存到 用户新的 CAM存储桶中 --> 然后触发新的回调
##### 2. 没有配置转码回调：
等待 腾讯这边提供转存完成的 taskid 列表，用户根据 cos桶的url规则，组装新的转码结果更新数据库（主要修改 `ResultUrl` 和 `ThumbnailUrl` 两个字段）
> 说明：
> 腾讯这边，会根据用户提供的 时间段 和 转码类型，将转码文件 --> 转存到 用户新的 CAM存储桶中 --> 用户根据 taskid，自己修改数据库里的转码结果（主要是修改 `ResultUrl` 和 `ThumbnailUrl` 两个字段）

