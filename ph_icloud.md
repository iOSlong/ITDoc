## PhotoKit


### PHAssetResource
#### PHAssetResourceType

##### 获取 PHAssetResource
+ (NSArray<PHAssetResource *> *)assetResourcesForAsset:(PHAsset *)asset;



### Apple Developer - TSI
#### 问题1 ：Title 
asynchronously written specified asset resource to local file failed with Code=257.
#### Description 
For upload photos to server from iOS device one by one, I traverse PHAssetCollections(assetCollectionSubtype == PHAssetCollectionSubtypeSmartAlbumUserLibrary)and get PHAssetResource. then asynchronously written asset resource to unique sandbox directory。
most of assets written success, but always few same especial assets failed with error as follow 2 point。

1. code snippet:
[[PHAssetResourceManager defaultManager] writeDataForAssetResource:photoResource toFile:tmpPath options:nil completionHandler:^(NSError* _Nullable error) {
        if (error) {
                _tmpError = error;
        } else {
            self.localPath = locFilePath;
        }
    }];

2. error log：
Error Domain=NSCocoaErrorDomain Code=257 "未能打开文件“IMG_4391.JPG”，因为您没有查看它的权限。" UserInfo={NSFilePath=/var/mobile/Media/PhotoStreamsData/460484986/124APPLE/IMG_4391.JPG, NSUnderlyingError=0x28340aa60 {Error Domain=NSPOSIXErrorDomain Code=1 "Operation not permitted"}}

3. questions
I wonder why get those error， and how to fix it。 

#### Configuration 
iPhone OS： 13_5_1
model： iPhone12,5
device：iPhone 11 Pro Max

#### Steps to Reproduce 
on my test device，most part of assets can be written success， only same five pictures failed every times，and I try run application on some other device，it's work well。 
It's make me confused。

#### 问题2 ：Title 
How to get PHAsset's original file from iCloud but keep local photo as thumbnail.
#### Description 
I want to upload the iCloud asset resource data to my server, first I download this resource data from iCloud as temporary file in sandbox directory, and upload the temporary file to my server. 

And then the main point:
I find the photo which I request resource from iCloud has been locallyAvailable, it's means my device disk storage space has been take up by the resource。

I wonder how can I get original data as temporary file from iCloud without disk usage creeps up，
Or if have some function to delete local original photo and keep it on the iCloud?

1. The code snippet below show my work:
- (void)test {
    PHAssetResource *aResource;  //resource form PHAsset belong SmartAlbumUserLibrary.
    NSURL           *tmpURL;     //one sandbox tmp directory
    PHAssetResourceRequestOptions *options = [PHAssetResourceRequestOptions new];
    options.networkAccessAllowed = YES;
    [[PHAssetResourceManager defaultManager] writeDataForAssetResource:aResource toFile:tmpURL options:options completionHandler:^(NSError* _Nullable error) {
        if (error) {
            NSLogError(@"[Photo iCloud Fail WriteAssetResource%@",error);
        } else {
            [self uploadFileFromURL:tmpURL complete:^(BOOL success) {
                if (success) {
                    [self removeTmpfileFromURL:tmpURL];
                }else{
                    //upload retry
                }
            }];
        }
    }];
}
- (void)removeTmpfileFromURL:(NSURL *)tmpUrl {
    //clear asset resource data file, make sure device disk storage space。
    //TODO:How to delete local resource(means keep original file on iCloud)???
}
- (void)uploadFileFromURL:(NSURL *)tmpUrl complete:(void(^)(BOOL success))complete {
    //upload asset resource data to one server。
}

2. error log：
None

3. questions
I want get PHAsset's original file from iCloud but keep local photo as thumbnail.
How to delete local resource without synchronization delete to iCloud (means keep original file on iCloud)
Or have some other method to my intention？

Look forward to your reply.

Best Regards,


#### Configuration 
iOS 13.4.1 (17E262)
Model: iPhone XR

#### Steps to Reproduce 
appear inevitably!



### reference
1. [iOS 获取图像的方式与坑点](https://blog.csdn.net/jeffasd/article/details/50465244)
2. [iOS开发之iCloud开发数据与文档的读写删除](http://blog.hudongdong.com/ios/385.html)
3. [CGImageSource](https://www.jianshu.com/p/d804fc4162a8)

    PHImageResultIsDegradedKey = 0;
    PHImageResultRequestIDKey = 20;


/var/mobile/Containers/Data/Application/7677AC06-49CA-46EA-A26D-06F14A42B2D0/Library/Caches/sync.tmp/所有照片/3FF2209B-5770-439C-A9B0-B81150A4BF87.PNG


iOS设备的相册备份 问题说明：
原有逻辑是会把所有能识别到的相册(非智能相册)都放入备份相册目录中，并且做实体源文件上传。
包括：
1. 相机胶卷(所有照片）
2. 用户自建(手机上自建的索引相册,第三方应用创建)
3. 外部设备导入的相册文件夹(其中图片不在相机胶卷中，开启iCloud同步则无此项)
4. 其他种类相册(最近的照片流，iCloud共享)
5. 其他部分Apple智能分类相册(已屏蔽)

当前发现问题：
1. 索引相册做实体文件备份，会导致iOS设备大量照片重复
> 待解决：iOS中的索引相册不做实体文件备份，如需要可另设交互开关开启创建索引相册【待产品确认具体设计方案，索引相册范围为用户在设备上自建的，其他的存在不可控情况】。
2. iOS开发者接口中部分相册照片实体源文件无权取得而导致备份失败(包括最近的照片流、iCloud共享等)
> 解决：备份扫描时候屏蔽无法取得读写权限的相册及照片。



https://lanhuapp.com/web/#/item/project/board?pid=c0846fc6-c4ac-4e01-938c-cf7a53d21b57
相册_备份设置页面优化，
https://lanhuapp.com/web/#/item/project/board?pid=2bcec1a9-c819-44df-b8bd-d64fb3b3dc2f



[系统设置_文件与共享服务UI已提交](https://lanhuapp.com/web/#/item/project/board?pid=65588f0c-96a7-48a3-a033-c1ec7e26b1ef)


// 文件服务接口 请先用192.168.1.6调接口
// 文件服务接口
1、AFP服务开启/关闭
   /settings?afp=true/false

2、smb服务开启/关闭
   /settings?smb=true/false

3、ftp服务开启/关闭及配置：
   /settings?ftp=true&port=xxxx

4、ntfs服务开启/关闭及配置：
   /settings?ntfs=true&port=xxxx

5、webdav服务开启/关闭及配置
   /settings?webdav=true&http_port=xxx&https_port=xxx

6、限速开启/关闭及配置
   /settings?limit=true&upload=xxx&download=xxx

http://192.168.1.6:8038/settings?ftp=true&port=1234
7、获取配置及服务状态
   http://127.0.0.1:8038/settings?config=1
   返回值：son
   示例：
    {
        "hostname" : "",
        "share_dir" : "",
 "afp" : false,
 "dlna" : 
 {
  "dir" : [ "/data/123" ],
  "is_share" : true,
  "turnoff" : false
 },
 "ftp" : 
 {
  "port" : 222,
  "turnoff" : false
 },
 "limit" : 
 {
  "download" : 222,
  "turnoff" : false,
  "upload" : 111
 },
 "ntfs" : 
 {
  "port" : 888,
  "turnoff" : false
 },
 "smb" : true,
 "webdav" : 
 {
  "http_port" : 1111,
  "https_port" : 2222,
  "turnoff" : false
 }

8、dlna文件服务接口及配置
  说明：post方式发送 json
   示例：
    "dlna" : 
  {
   "dir" : [ "/tmp/zfuse/share/", "/data/downloader", "/data1/download/dlna" ],  
   "is_share" : false,                                                                
   "turnoff" : true                                                                 
  }

"dlna" : 
  {
   "is_share" : true,                                                                
   "turnoff" : true                                                                 
  }



#### 时间线问题-天天整理： https://shimo.im/docs/kgy6THRh3WgTCQJG

提测功能点：
1. 增加自动备份和手动备份控制开关
2. 增加相册备份任务中心入口
3. 单张照片分享，不要链接，直接分享内容。
4. 上传照片时获取exif的地点\时间信息。
5. 授权调整(首次使用授权说明文案调整、其他情况为在需要使用授权功能时弹出授权申请弹框)


