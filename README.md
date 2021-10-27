# index

## 国内环境导致的无法同步

可尝试使用清华源同步谷歌源码 替换已有的 AOSP 源代码的 remote 将 .repo/manifests.git/config 内的

```
url = https://android.googlesource.com/platform/manifest
```

修改为

```
url = https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest
```

或者不修改源文件，直接执行

```
git config --global url.https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/.insteadof https://android.googlesource.com
```

**温馨提示：** **如果网络环境不是太差，挂科学都无法同步，我并不建议使用国内镜像** **国内镜像大多都有一些奇奇怪怪的问题**

## 常见的错误

```
error: RPC failed; result=18, HTTP code = 200MiB/s

fatal: The remote end hung up unexpectedly

fatal: 过早的文件结束符（EOF）

fatal: index-pack failed
```

出现该错误一般是因为 文件太大了，以及墙的原因。。。需要扩大一下传输限制 **解决方法**

```
git config http.postBuffer 524288000
```

后面的数字是字节 自行调节至合适的大小
