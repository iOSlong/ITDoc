[Create your own CocoaPods library](https://medium.com/flawless-app-stories/create-your-own-cocoapods-library-da589d5cd270)

### Here is a quick overview of all the steps to create a pod:

#### 1. Set up Xcode project and necessary targets
* 注意pod 名不能重复，譬如 LCAsync

* Create a Cocoa Touch Framework Xcode project
> 选择Cocoa Touch Framework， 输入名字 LCAsync
> select the checkbox Include Unit Tests
> 不要勾选 Create Git repository on my Mac

* Prepare the targets
> now have a project called SwiftyLib and it has two targets:
    1. LCAsync: Our pod implementation will happen in here
    2. LCAsyncTests: Unit tests our pod and collects code coverage

* Add a new target called LCAsyncExamples .
> Select SwiftyLib project from the project navigator, then choose File > New > Target…, select Single View App as the template and click on Next .


#### 2.  Link to Github
* Create a new repository
* Link existing project

```
git init
> git remote add origin git@github.com:iOSlong/LCAsync.git
> git add .
> git commit -m "Initial project setup"
> git push -u origin master
```
* README and MIT License

> 关于LICENSE的创建，[Adding a license to a repository](https://help.github.com/en/articles/adding-a-license-to-a-repository)
Choose a license template 这个按钮可能需要创建完LICENSE后刷新，再点击编辑LICENSE才会显示。

* 完了更新本地仓库

```
 git pull
...
2 files changed, 24 insertions(+)
create mode 100644 LICENSE
create mode 100644 README.md
```


#### 3.  Implement the pod
* 实现具体的库文件，

#### 4.  Write unit tests
> 保证库质量的测试

#### 5.  Configure Travis CI and Codecov
> 辅助监测pod库的两个第三方工具。
1. [Travis CI](https://travis-ci.org/)
2. [Codecov](https://codecov.io/)
补充一个 [Slather](https://github.com/SlatherOrg/slather) 

#### 6.  Publish the pod
* Then create a podspec file that defines our pod, e.g., where to find the source.

```
pod spec create LCAsync
...
Specification created at LCAsync.podspec
```

* Edit the LCAsync.podspec file:

```
bogon:LCAsync lxw$ cat LCAsync.podspec 
#
#  Be sure to run `pod spec lint LCAsync.podspec' to ensure this is a
#  valid spec and to remove all comments including this before submitting the spec.
#
#  To learn more about Podspec attributes see http://docs.cocoapods.org/specification.html
#  To see working Podspecs in the CocoaPods repo see https://github.com/CocoaPods/Specs/
#

Pod::Spec.new do |s|

  # ―――  Spec Metadata  ―――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  These will help people to find your library, and whilst it
  #  can feel like a chore to fill in it's definitely to your advantage. The
  #  summary should be tweet-length, and the description more in depth.
  #

  s.name         = "LCAsync"
  s.version      = "0.0.1"
  s.summary      = "A CocoaPods library written in Swift. you can do some aysnc missons with LCAsync."

  # This description is used to generate tags and improve search results.
  #   * Think: What does it do? Why did you write it? What is the focus?
  #   * Try to keep it short, snappy and to the point.
  #   * Write the description between the DESC delimiters below.
  #   * Finally, don't worry about the indent, CocoaPods strips it!
  s.description  = <<-DESC
A CocoaPods library written in Swift,
This CocoaPods library helps you perform calculation and some async missons。
                   DESC

  s.homepage     = "https://github.com/iOSlong/LCAsync"
  # s.screenshots  = "www.example.com/screenshots_1.gif", "www.example.com/screenshots_2.gif"


  # ―――  Spec License  ――――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  Licensing your code is important. See http://choosealicense.com for more info.
  #  CocoaPods will detect a license file if there is a named LICENSE*
  #  Popular ones are 'MIT', 'BSD' and 'Apache License, Version 2.0'.
  #

  s.license      = {:type => "GPL-3.0", :file => "LICENSE"}
  # s.license      = { :type => "MIT", :file => "FILE_LICENSE" }


  # ――― Author Metadata  ――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  Specify the authors of the library, with email addresses. Email addresses
  #  of the authors are extracted from the SCM log. E.g. $ git log. CocoaPods also
  #  accepts just a name if you'd rather not provide an email address.
  #
  #  Specify a social_media_url where others can refer to, for example a twitter
  #  profile URL.
  #

  s.author             = { "xw.long" => "xuewu1011@163.com" }
  # Or just: s.author    = "xw.long"
  # s.authors            = { "龙学武" => "xuewu1011@163.com" }
  # s.social_media_url   = "http://twitter.com/龙学武"

  # ――― Platform Specifics ――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  If this Pod runs only on iOS or OS X, then specify the platform and
  #  the deployment target. You can optionally include the target after the platform.
  #

  # s.platform     = :ios
  # s.platform     = :ios, "5.0"

  #  When using multiple platforms
  # s.ios.deployment_target = "5.0"
  # s.osx.deployment_target = "10.7"
  # s.watchos.deployment_target = "2.0"
  # s.tvos.deployment_target = "9.0"


  # ――― Source Location ―――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  Specify the location from where the source should be retrieved.
  #  Supports git, hg, bzr, svn and HTTP.
  #

  s.source       = { :git => "https://github.com/iOSlong/LCAsync.git", :tag => "#{s.version}" }


  # ――― Source Code ―――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  CocoaPods is smart about how it includes source code. For source files
  #  giving a folder will include any swift, h, m, mm, c & cpp files.
  #  For header files it will include any header in the folder.
  #  Not including the public_header_files will make all headers public.
  #

  s.source_files  = "LCAsync/**/*.{h,m}"
  s.exclude_files = "LCAsync/Exclude"

  # s.public_header_files = "Classes/**/*.h"


  # ――― Resources ―――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  A list of resources included with the Pod. These are copied into the
  #  target bundle with a build phase script. Anything else will be cleaned.
  #  You can preserve files from being cleaned, please don't preserve
  #  non-essential files like tests, examples and documentation.
  #

  # s.resource  = "icon.png"
  # s.resources = "Resources/*.png"

  # s.preserve_paths = "FilesToSave", "MoreFilesToSave"


  # ――― Project Linking ―――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  Link your library with frameworks, or libraries. Libraries do not include
  #  the lib prefix of their name.
  #

  # s.framework  = "SomeFramework"
  # s.frameworks = "SomeFramework", "AnotherFramework"

  # s.library   = "iconv"
  # s.libraries = "iconv", "xml2"


  # ――― Project Settings ――――――――――――――――――――――――――――――――――――――――――――――――――――――――― #
  #
  #  If your library depends on compiler flags you can set them in the xcconfig hash
  #  where they will only apply to your library. If you depend on other Podspecs
  #  you can include multiple dependencies to ensure it works.

  # s.requires_arc = true

  # s.xcconfig = { "HEADER_SEARCH_PATHS" => "$(SDKROOT)/usr/include/libxml2" }
  # s.dependency "JSONKit", "~> 1.4"

end
```

* Check if SwiftyLib.podspec is correct, fix issues if there is any
> 可能出现界面如下:

```
bogon:LCAsync lxw$ pod lib lint

 -> LCAsync (0.0.1)
    - ERROR | source: The Git source still contains the example URL.
    - WARN  | summary: The summary is not meaningful.
    - ERROR | description: The description is empty.
    - ERROR | [OSX] unknown: Encountered an unknown error (The `LCAsync` pod failed to validate due to 2 errors:
    - ERROR | source: The Git source still contains the example URL.
    - WARN  | summary: The summary is not meaningful.
    - ERROR | description: The description is empty.
    - ERROR | [OSX] xcodebuild: Returned an unsuccessful exit code. You can use `--verbose` for more information.


) during validation.

```

```
ERROR | source: 重新编辑source地址
WARN  | summary: 重新编写有说服力的简介
ERROR | description:描述不能为空，且最好内容多余summary描述，否则有警告

//出现下面这个，将pod就好。'sudo gem install cocoapods'
ERROR | [iOS] unknown: Encountered an unknown error (Could not find a `ios` simulator (valid values: com.apple.coresimulator.simruntime.ios-12-2, com.apple.coresimulator.simruntime.tvos-12-2, com.apple.coresimulator.simruntime.watchos-5-2). Ensure that Xcode -> Window -> Devices has at least one `ios` simulator listed or otherwise add one.) during validation.

ERROR | [OSX] xcodebuild: Returned an unsuccessful exit code. You can use `--verbose` for more information.   这个一般是功能不能通过编译导致，
通过：pod lib lint --verbose 查看详情
    - ERROR | [OSX] xcodebuild: Returned an unsuccessful exit code.
    - NOTE  | xcodebuild:  note: Using new build system
    - NOTE  | [OSX] xcodebuild:  note: Planning build
    - NOTE  | [OSX] xcodebuild:  note: Constructing build description
    - NOTE  | [OSX] xcodebuild:  Headers/Public/LCAsync/LCAsync.h:9:9: fatal error: 'UIKit/UIKit.h' file not found
可以通过NOTE 定位到 LCAsync.h文件中 9行，UIKit/UIKit.h'代码有问题，解决了就好。


警告也会导致链接验证不通过如下：
bogon:LCAsync lxw$ pod lib lint
 -> LCAsync (0.0.1)
    - WARN  | description: The description is shorter than the summary.
    - NOTE  | xcodebuild:  note: Using new build system
    - NOTE  | xcodebuild:  note: Planning build
    - NOTE  | xcodebuild:  note: Constructing build description

[!] LCAsync did not pass validation, due to 1 warning (but you can use `--allow-warnings` to ignore it).
解决：编辑description，使得内容多余summary即可。


 -> LCAsync (0.0.1)
    - NOTE  | xcodebuild:  note: Using new build system
    - NOTE  | xcodebuild:  note: Planning build
    - NOTE  | xcodebuild:  note: Constructing build description

LCAsync passed validation.


》Great! Let’s save our changes to Github!
    git add .
    git commit -m "Added LCAsync.podspec"
    git push
```

* Start to distribute our library
> Tag the correct version

    ```
        > git tag 0.0.1
        > git push origin 0.0.1
    ```
> Then push it!

    ```
    bogon:LCAsync lxw$ pod trunk push

    [!] Found podspec `LCAsync.podspec`
    [!] You need to register a session first.
    
    》 出现如上错误，需要填写邮箱注册并受到邮件之后点击验证一下：
    bogon:LCAsync lxw$ pod trunk register xuewu1011@163.com 'xw.long' --description='macbook pro'
    [!] Please verify the session by clicking the link in the verification email that has been sent to xuewu1011@163.com
    》 邮件验证之后可继续执行命令。
    
    bogon:LCAsync lxw$ pod trunk push
    [!] Found podspec `LCAsync.podspec`
Updating spec repo `master`
    [!] CocoaPods was not able to update the `master` repo. If this is an unexpected issue and persists you can inspect it running `pod repo update --verbose`
    》 这个错误一致困扰着，一个小时过去了， ~ 多次尝试pod repo update --verbose也执行了， 依然没有好。   
    ```
    > 再出幺蛾子如下:
    
    ```
    bogon:LCAsync lxw$ pod trunk push

    [!] Found podspec `LCAsync.podspec`
    Updating spec repo `master`
    Validating podspec
     -> LCAsync (0.0.1)
         - NOTE  | xcodebuild:  note: Using new build system
         - NOTE  | xcodebuild:  note: Planning build
         - NOTE  | xcodebuild:  note: Constructing build description

    [!] Unable to accept duplicate entry for: LCAsync (0.0.1)
    ```
##### 6.1 于是只好同时跟新podspec中的version号和git tag为：0.0.2 然后分别执行命令 pod spec lint 验证并提交到CocoPods（提交命令： pod trunk push LCAsync.podspec）

```
bogon:LCAsync lxw$ vim LCAsync.podspec  //更改版本号。
bogon:LCAsync lxw$ git add .
bogon:LCAsync lxw$ git commit -m"add podversion to 0.0.2 for trunck"
[master 10feac1] add podversion to 0.0.2 for trunck
 2 files changed, 1 insertion(+), 1 deletion(-)
bogon:LCAsync lxw$ git push

bogon:LCAsync lxw$ git tag 0.0.2
bogon:LCAsync lxw$ git push --tags
Total 0 (delta 0), reused 0 (delta 0)
To github.com:iOSlong/LCAsync.git
 * [new tag]         0.0.2 -> 0.0.2
bogon:LCAsync lxw$ git push origin master
Everything up-to-date
bogon:LCAsync lxw$ pod spec lint

 -> LCAsync (0.0.2)
    - NOTE  | xcodebuild:  note: Using new build system
    - NOTE  | xcodebuild:  note: Planning build
    - NOTE  | xcodebuild:  note: Constructing build description

Analyzed 1 podspec.

LCAsync.podspec passed validation.

bogon:LCAsync lxw$ pod trunk push LCAsync.podspec
Updating spec repo `master`
Validating podspec
 -> LCAsync (0.0.2)
    - NOTE  | xcodebuild:  note: Using new build system
    - NOTE  | xcodebuild:  note: Planning build
    - NOTE  | xcodebuild:  note: Constructing build description

Updating spec repo `master`

--------------------------------------------------------------------------------
 🎉  Congrats

 🚀  LCAsync (0.0.2) successfully published
 📅  July 12th, 02:11
 🌎  https://cocoapods.org/pods/LCAsync
 👍  Tell your friends!
--------------------------------------------------------------------------------
》 终于得见光明。
```

>  6.1 中的方式，也适合用于cocoapods 库的更新。


### Pod search LCAsync 

```
bogon:LCAsync lxw$ pod search LCAsync
[!] Unable to find a pod with name, author, summary, or description matching `LCAsync`

// 解决，将电脑上的原有搜索缩影json文件移除掉，再重新搜索。
bogon:LCAsync lxw$ rm ~/Library/Caches/CocoaPods/search_index.json
bogon:LCAsync lxw$ pod search LCAsync
Creating search index for spec repo 'master'.. Done!

-> LCAsync (0.0.2)
   A CocoaPods library written in Swift. you can do some aysnc missons with LCAsync.
   pod 'LCAsync', '~> 0.0.2'
   - Homepage: https://github.com/iOSlong/LCAsync
   - Source:   https://github.com/iOSlong/LCAsync.git
   - Versions: 0.0.2, 0.0.1 [master repo]

end
```

### update version of LCAsync
> 这是第一次提交成功之后，更新库的操作记录：


#### 1.update pod version in LCAsync.podspec
lxw$ vim LCAsync.podspec 
编辑更新pod 版本。

#### 2.update the changes with commit massage
lxw$ git add .
lxw$ git commit -m"update podversion 0.0.2 - 0.0.3"
lxw$ git push

#### 3.pod lib lint 验证LCAsync.podspec 库链接
OK：
```
bogon:LCAsync lxw$ pod lib lint

 -> LCAsync (0.0.3)
    - NOTE  | xcodebuild:  note: Using new build system
    - NOTE  | xcodebuild:  note: Planning build
    - NOTE  | xcodebuild:  note: Constructing build description

LCAsync passed validation.
```
#### 4.push new tag 0.0.3
OK：
```
bogon:LCAsync lxw$ git tag 0.0.3
bogon:LCAsync lxw$ git push origin 0.0.3
Total 0 (delta 0), reused 0 (delta 0)
To github.com:iOSlong/LCAsync.git
 * [new tag]         0.0.3 -> 0.0.3

```

#### 5. pod trunk push 提交cocoapods托管库

> 第一次执行命令，长久没有反映， 于是取消执行（control+C）:

```
bogon:LCAsync lxw$ pod trunk push

[!] Found podspec `LCAsync.podspec`
Updating spec repo `master`
^C[!] Cancelled
```

> 切换为shadowsocks 代理网络状态，验证了一下可以链接Google。再次执行命令， 成功：

```
bogon:LCAsync lxw$ pod trunk push

[!] Found podspec `LCAsync.podspec`
Updating spec repo `master`

CocoaPods 1.8.0.beta.1 is available.
To update use: `sudo gem install cocoapods --pre`
[!] This is a test version we'd love you to try.

For more information, see https://blog.cocoapods.org and the CHANGELOG for this version at https://github.com/CocoaPods/CocoaPods/releases/tag/1.8.0.beta.1

Validating podspec
 -> LCAsync (0.0.3)
    - NOTE  | xcodebuild:  note: Using new build system
    - NOTE  | xcodebuild:  note: Planning build
    - NOTE  | xcodebuild:  note: Constructing build description

Updating spec repo `master`

CocoaPods 1.8.0.beta.1 is available.
To update use: `sudo gem install cocoapods --pre`
[!] This is a test version we'd love you to try.

For more information, see https://blog.cocoapods.org and the CHANGELOG for this version at https://github.com/CocoaPods/CocoaPods/releases/tag/1.8.0.beta.1


--------------------------------------------------------------------------------
 🎉  Congrats

 🚀  LCAsync (0.0.3) successfully published
 📅  August 10th, 03:10
 🌎  https://cocoapods.org/pods/LCAsync
 👍  Tell your friends!
--------------------------------------------------------------------------------
```


