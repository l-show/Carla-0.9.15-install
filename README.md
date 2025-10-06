# Carla-0.9.15-install / CARLA 编译指南 / Conda环境
Installation tutorial for Carla-0.9.15 compiled version
# 1. 安装前置软件
## 1.1 系统要求
操作系统：64位系统<br>
磁盘空间：至少165GB<br>
GPU：6GB（推荐8GB）<br>
## 1.2 软件要求
以下软件版本是截至2025年10月6日的推荐版本：<br>
CMake 3.30.4<br>
Git 2.46.2<br>
Make 3.8.1<br>
7zip<br>
建议将所有软件安装到统一目录（例如 D:\Software），以便后续管理环境变量。<br>
## 1.3 设置环境变量
将上述软件路径添加到系统环境变量中。<br>
## 1.4 安装 Python 及依赖项
通过ANACONDA.NAVIGATOR配置python-3.8.20（确保版本与 CARLA Python API 兼容，建议使用 3.8）<br>
<img width="960" height="541" alt="image" src="https://github.com/user-attachments/assets/dd318ff2-39fc-4239-99b9-570ab5a65b06" />
在命令行中确认 python -V 和 py -V 显示相同的版本。<br>不需要，后续可以解决
安装以下依赖项：<br>
pip3 install --upgrade pip<br>
pip3 install --user setuptools<br>
pip3 install --user wheel<br>
<img width="1044" height="87" alt="image" src="https://github.com/user-attachments/assets/fbb910a2-3294-4879-a4e3-3c17a24544a2" />
<img width="1237" height="109" alt="image" src="https://github.com/user-attachments/assets/5ce8e5d1-8e28-4299-9441-c291d76659ce" />
<img width="904" height="277" alt="image" src="https://github.com/user-attachments/assets/e6f9e6bc-04b3-453c-bf35-94a60cc48da8" />
## 1.5 安装 Visual Studio 2019
下载地址：[Visual Studio 2019 Community](https://c2rsetup.officeapps.live.com/c2r/downloadVS.aspx?sku=community&channel=Release&version=VS2019&source=VSLandingPage&cid=2030:310c1dac731b4525bdef19486f31261b)<br>
官网只有VS2022版本，以下给出VS2029版本链接<br>
<https://c2rsetup.officeapps.live.com/c2r/downloadVS.aspx?sku=community&channel=Release&version=VS2019&source=VSLandingPage&cid=2030:310c1dac731b4525bdef19486f31261b><br>
在安装过程中勾选以下选项：
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5fed638f-d8d4-418b-947c-088c7fa2b14f" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b0971f3e-95ef-4254-9d53-ed2f80af94bf" />
Desktop development with C++<br>
Game development with C++<br>
<img width="1536" height="1020" alt="image" src="https://github.com/user-attachments/assets/e37d5da7-ca02-46dc-97f2-10399caff5ca" />
## 1.6 安装 Unreal Engine
下载 Unreal Engine 源码： UnrealEngine-carla.<br>
选择UE4.26分支版本
<img width="2479" height="1755" alt="image" src="https://github.com/user-attachments/assets/d31aecb0-3b28-44ba-9967-0807170a1450" />
github主页：<https://github.com/CarlaUnreal/UnrealEngine/tree/carla><br>
<img width="513" height="99" alt="image" src="https://github.com/user-attachments/assets/d9a072f1-b1cb-40e5-ac45-75a7bdfe9734" /><br>
399MB解压需要20-25分钟<br>
解压会产生两层UnrealEngine-carla路径记得删除一层
在解压后的文件夹中先后执行以下两个命令：<br>
Setup.bat<br>
需要2h<br>
GenerateProjectFiles.bat<br>
小于20s<br>
用vs2019打开解压出来的UE4.sln文件，在上方选择栏中选择编译工具“Development Editor”、“Win64”和“UnrealBuildTool”选项，在解决方案资源管理器中右键选择UE4项目，点击生成（Build）<br>
使用 VS2019 打开 UE4.sln，选择 “Development Editor”、“Win64”和 “UnrealBuildTool” 选项，右键点击 UE4 项目并选择生成（Build）。<br>
需要20min<br>
<img width="416" height="168" alt="image" src="https://github.com/user-attachments/assets/ce1a4ce3-76df-42e5-8d23-20e7085a2af9" />
等待成功之后在\UnrealEngine\Engine\Binaries\Win64下点击UE4Editor.exe，第一次加载会很慢，卡在45%或者75%，95%是正常的，等待渲染好出现UE界面即可。<br>
<img width="416" height="188" alt="image" src="https://github.com/user-attachments/assets/864a741c-7089-4ecf-819e-3a4afc083549" />
设置环境变量 UE4_ROOT 指向 Unreal Engine 的安装目录。<br>
# 2. 安装 CARLA
## 2.1 下载 CARLA 源码
根据所需版本下载 CARLA 源码：<br>
必须使用git，否则后续需要手动改版本，麻烦<br>
open git bash here<br>
设置 HTTP 代理<br>
export HTTP_PROXY="http://127.0.0.1:7890"<br>
设置 HTTPS 代理<br>
export HTTPS_PROXY="http://127.0.0.1:7890"<br>
设置所有协议的代理 (通常 Git 也能识别这个)<br>
export ALL_PROXY="socks5://127.0.0.1:7890"<br>
取消所有的代理<br>
unset HTTP_PROXY<br>
unset HTTPS_PROXY<br>
unset ALL_PROXY<br>
端口号为自己VPN软件的端口号<br>
git clone -b 0.9.15 https://github.com/carla-simulator/carla.git<br>
## 2.2 下载 CARLA 资产库
打开 carla/Util/ContentVersions.txt 文件，根据版本选择对应的资产库下载链接。例如，0.9.15 版本资产库：<br>
https://carla-assets.s3.us-east-005.backblazeb2.com/20231108_c5101a5.tar.gz<br>
将下载的文件解压重命名至 carla/Unreal/CarlaUE4/Content/Carla 目录。<br>
其中需注意，carla已不再使用该txt文件中下载链接指向的AWS云服务，新的资产库文件使用backblazeb2云服务，下载链接应更新为https://carla-assets.s3.us-east-005.backblazeb2.com/PUT_FILE_ID_HERE.tar.gz。<br>
解压需要几分钟，注意路径是Content/Carla<br>
# 准备开始编译！！！
## 2.3 编译 Python API
### 版本更新-2025/10/06
先在D:\carla0.9.15\Util\InstallersWin路径下修改install_zlib.bat中51行set ZLIB_VERSION=1.2.13为1.3.1<br>
再在D:\carla0.9.15\Util\InstallersWin路径下修改install_xercesc.bat中49行set XERCESC_VERSION=3.2.3为3.2.4<br>
将下载好的boost_1_80_0.zip放在路径D:\carla0.9.15\Build下，没有就先新建一个<br>
### 端口代理
在 Visual Studio 2019 的 x64 Native Tools Command Prompt 中执行以下命令设置aconda路径<br>
set PATH=%PATH%;C:\ProgramData\anaconda3\condabin;C:\ProgramData\anaconda3\Scripts;C:\ProgramData\anaconda3\Library\bin<br>
cd进入路径并激活conda环境<br>
D:\carla0.9.15>conda activate Carla-0915<br>
(Carla-0915) D:\carla0.9.15>python -V<br>
Python 3.8.20<br>
启动网络代理，Clash of Android端口7890<br>
set HTTP_PROXY=http://127.0.0.1:7890<br>
set HTTPS_PROXY=http://127.0.0.1:7890<br>
set ALL_PROXY=socks5://127.0.0.1:7890<br>
查看是否代理成功env|grep -i proxy<br>
(Carla-0915) D:\carla0.9.15>env|grep -i proxy<br>
ALL_PROXY=socks5://127.0.0.1:7890<br>
HTTPS_PROXY=http://127.0.0.1:7890<br>
HTTP_PROXY=http://127.0.0.1:7890<br>
### 开始编译 Python API
(Carla-0915) D:\carla0.9.15>make PythonAPI<br>
make PythonAPI时保持VPN稳定<br>
如果遇到编译错误，检查依赖包是否安装完整。可参考官方文档和其他社区博客进行故障排除。<br>
# 3. 常见问题及解决
## 3.1 编译问题
zlib 版本问题：确保使用正确版本的 zlib，若安装失败，手动下载并解压。

Gtest 安装失败：如果安装失败，可删除 D:\carla0.9.15\carla0.9.15\Util\BuildTools 下的 Gtest 配置，改为手动安装。

缺少依赖文件：如 OSM2ODR.h 文件缺失，请检查 carla/Build 目录下的依赖文件，必要时手动下载。

## 3.2 Git 配置
设置代理加速 Git 下载：

export HTTP_PROXY="http://127.0.0.1:7890"
export HTTPS_PROXY="http://127.0.0.1:7890"
export ALL_PROXY="socks5://127.0.0.1:7890"
## 3.3 编译时缺失 xerces-c_3.lib
在 carla/Unreal/CarlaUE4/Plugins/Carla/CarlaDependencies/lib 下缺少 xerces-c_3.lib 文件时，复制对应文件至该目录即可解决问题。

## 3.4 fatal error C1083 问题
在 Setup.bat 文件中添加以下内容来解决 Version.h 找不到的错误：


set carla_version="0.9"
##4. 其他注意事项
使用 Conda 环境：确保 conda 在 x64 Native Tools Command Prompt 中正确配置，使用以下命令设置环境变量：

set PATH=%PATH%;C:\ProgramData\anaconda3\condabin;C:\ProgramData\anaconda3\Scripts
代理加速下载：若下载速度过慢，使用 VPN 或临时代理解决问题：


set HTTP_PROXY=http://127.0.0.1:7890
set HTTPS_PROXY=http://127.0.0.1:7890
