#### [Live Photos](https://developer.apple.com/design/human-interface-guidelines/live-photos/overview/)
> [Live Photo 实况图(包含拍摄前后共3s以内的音视频内容)](https://support.apple.com/zh-cn/HT207310)

* 数据组成：一个图片文件(HEIC/jpg) + 一个视频文件(mov)， iOS使用是内置组件api组合数据，并通过LivePhotoView组件展示效果。

* 测试微信qq等转发效果：转发为一张jpg格式的图片(不会转发源文件)。
* 苹果设备隔空投送：源文件格式

##### 1. 在Android端
* Android本身不支持Live Photo，但是可以进行模拟。 譬如：先从服务端拉取要展示的图片+视频，展示时，直接将图片覆盖到视频上，当进行按压时，隐藏图片，播放视频即可。
* 另可尝试使用web控件展示

##### 2. 在Web端支持LivePhoto
* Tip: 使用JS库 [LivePhotosKit JS](https://developer.apple.com/documentation/livephotoskitjs?language=objc)

##### 3. [一个不错的LivePhoto研发随笔](https://www.cnblogs.com/zhanggui/p/9283428.html)

