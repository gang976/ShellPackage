
# ReleaseDir
Shell脚本-ipa打包专用
```objc
 脚本说明：
 1、实现功能：
     1）、指定打包项目的Build号，Version版本号（Version号可选择自增或自定义）
     2）、导出xcarchive文件
     3）、打包生成ipa文件
 2、使用方式：
     1）、将ReleaseDir文件夹，放到跟所要打包的项目的根目录（shellPackageDemo）同级别的目录下
     2）、cd至ReleaseDir，运行脚本./Release.sh shellPackageDemo，并选择输入相关参数，开始打包
     3）、完成打包后，生成的目标文件在如下目录：
          /ReleaseDir/ArchivePath/shellPackageDemo/1.0.0/2017_08_29_16:15:20
          (/ReleaseDir/ArchivePath/打包项目名称/打包版本号/打包时间)
--------------------------------------------------------------------------------

--------------------------------------------------------------------------------
 打包project
        ./Release.sh  <Project directory name> [-s <Name>] [-e] [-d] [-a] [-b <Build number>]
 打包workspace
        ./Release.sh  <Project directory name> [-w] [-s <Name>] [-e] [-d] [-b <Build number>] [-v <Version number>]
 参数说明：
     <Project directory name>    第一个参数：所要打包的项目的根目录文件夹名称         
     -w                          workspace打包，不传默认为project打包
     -s <Name>                   对应workspace下需要编译的scheme（不传默认取xcodeproj根目录文件名）
     -e                          打包前是否先编译工程（不传默认不编译）
     -d                          工程的configuration为 Debug 模式，不传默认为Release
     -a                          打包，Version版本号自动＋1（针对多次打测试包时的版本号修改）
     -b <Build Num>              Build版本号，指定项目Build号
     -v <Version Num>            Version版本号，指定项目Version号
  注意，参数-a 与 -v 互斥，只能选择传其中一种参数！！
--------------------------------------------------------------------------------

--------------------------------------------------------------------------------
 ReleaseDir文件目录说明：

 |___shellPackageDemo                                所要打包的项目的根目录
 |___ReleaseDir                              打包相关资源的根目录
    |___Release.sh                           Release.sh打包脚本
    |___ExportOptions.plist                  -exportOptionsPlist 配置文件
    |___ArchivePath                          打包文件输出路径
       |___shellPackageDemo                          打包项目名称
          |___1.0.0                          打包版本号
             |___2017_08_29_16/15/20         打包时间（格式：年_月_日_时/分/秒）
                |___shellPackageDemo_1.0.0.xcarchive 导出的.xcarchive文件
                |___shellPackageDemo.ipa             导出的.ipa文件
                |___LogPath                  打包日志



**********打包完成自动化上传 fir / 蒲公英 第三方平台************
要上传到 fir / 蒲公英 第三方平台，都需要注册一个账号，获得token，之后才能进行脚本化操作。

1. 自动化上传fir

安装fir-clifir的命令行工具 需要先装好ruby再执行

gem install fir-cli

#上传到fir
fir publish ${ipa_path} -T fir_token -c "${commit_msg}"


2.自动化上传蒲公英

#蒲公英上的User Key
uKey="7381f97070*****c01fae439fb8b24e"
#蒲公英上的API Key
apiKey="0b27b5c145*****718508f2ad0409ef4"
#要上传的ipa文件路径
IPA_PATH=$(cat text.txt)

rm -rf text.txt

#执行上传至蒲公英的命令
echo "++++++++++++++upload+++++++++++++"
curl -F "file=@${IPA_PATH}" -F "uKey=${uKey}" -F "_api_key=${apiKey}" http://www.pgyer.com/apiv1/app/upload






