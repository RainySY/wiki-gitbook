# index

这里我选择的是 [PixelExperience](https://github.com/PixelExperience) 的类原生源码进行编译

以 Ubuntu为列

### 注：建议在非root用户下进行编译

```
wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip
unzip platform-tools-latest-linux.zip -d ~
`
```

编辑 `~/.profile`文件

```
vim ~/.profile
```

在最下面加入

```
# add Android SDK platform tools to path
if [ -d "$HOME/platform-tools" ] ; then
    PATH="$HOME/platform-tools:$PATH"
fi
```

以上是为了adb环境

## 安装依赖环境

```
sudo apt install
cd ~/
git clone https://github.com/akhilnarang/scripts
cd scripts
./setup/android_build_env.sh
```

## 拉取源码

```
mkdir -p ~/bin
mkdir -p ~/android/pe
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

若在`curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo`卡住

或是没有科学工具，可尝试运行此命令

```
export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'
```

若是本地网络极差，无法拉取Google源码

可尝试运行此命令

```
git config --global url.https://mirrors.bfsu.edu.cn/git/AOSP/.insteadof https://android.googlesource.com
```

再次编辑`~/.profile`

```
vim ~/.profile
```

在最下面加入

```
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```

添加Git用户

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

定义repo目录

```
cd ~/android/pe
repo init -u https://github.com/PixelExperience/manifest -b eleven
repo sync -j$(nproc --all) -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

这次我们拉取的是Android R的源码

### 等待源码同步完成

等到出现`success`字符时，表示源码全部同步完成，且无错误产生

此时我们便可以进行下一步，选择机型

## 选择机型

```
source build/envsetup.sh
lunch aosp_$devices-userdebug
```

`$devices`为设备代号，请自行替换

详情可以去寻找自己机型的相关数据

[PixelExperience-Devices](https://github.com/PixelExperience-devices)此为PixelExperience ROM的官方设备库

## 开始编译

为了加快编译速度，我们可以加一些ccache

```
export USE_CCACHE=1
export CCACHE_EXEC=/usr/bin/ccache
ccache -M 50G
```

开始编译

```
croot
mka bacon -j$(nproc --all)
```

等待编译结束后

```
cd $OUT
```

寻找 `‘PixelExperience_`开头的文件，此为我们本次编译所产生的ROM包

这次教程并无太多细节

若有疑问可以质询我，或者前往 AKR社区寻找大佬的帮助

我只是个菜鸡
