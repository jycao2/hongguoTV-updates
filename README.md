# 红果 TV · 原生客户端与自动更新

[下载最新版 APK](https://github.com/jycao2/hongguoTV-updates/releases/latest) · [构建状态](https://github.com/jycao2/hongguoTV-updates/actions/workflows/release.yml)

Android 8.0+，Kotlin / Media3，单 APK，无需部署服务。非官方、自用电视客户端。

首次手动安装带更新功能的正式版后，应用在前台浏览时每 6 小时检查一次新版，下载并校验后提示安装。播放时停止更新请求；无需 GitHub 登录。设置 → 版本与更新可手动检查或关闭自动下载。Android 8 仍需允许本应用安装未知来源应用，并确认系统安装；并非静默安装。

保留短剧/漫剧浏览、搜索、收藏、观看记录、续播、选集、全局清晰度与倍速。沿用原发布签名，覆盖安装保留本机数据。平台账号同步尚未接通。

本仓库只包含可发布的原生源码及构建文件，使用 GPL-3.0。main 每次更新会通过 GitHub Actions 运行测试、Release lint，生成签名 APK，再发布 APK、对应源码、update.json 和校验和。源码不包含发布私钥；签名密钥仅配置于 Actions Secrets。

构建开发 APK（JDK 17、Android SDK 36）：

```sh
./kotlin-tv/gradlew -p kotlin-tv :core:test :app:assembleDebug
```

正式构建使用 `scripts/build-kotlin.sh`；签名配置见 [原生构建说明](kotlin-tv/README.md)。自动版本号为 10000 + workflow run_number，versionName 为 0.9.0+run_number。Release 的 update.json 记录确切版本和源码提交，复现时传入 HONGGUOTV_VERSION_CODE 与 HONGGUOTV_VERSION_NAME。

Android 8 实体电视的解码、音频、遥控器和系统安装入口仍需实机确认。
