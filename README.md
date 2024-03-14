# ArcadeLinkage

这是一个帮助音游直播机台实现自助录像、直播等功能的开源项目.  能极大方便录制内录手元等视频

**这个项目代码较乱，实现方式比较抽象（网络意义上的），如造成了阅读屎山时的障碍十分抱歉QwQ**

## 架构

- `ALLS.WebAPI`: 非常简单的API实现，为其他应用提供后端服务
- [alls_recorder](https://github.com/Kgym-Hina/alls_recorder): 基于Flutter开发的跨平台应用，用于在自助录像功能识别用户和下载视频
- [ArcadeLinkage.UI](https://github.com/Kgym-Hina/ArcadeLinkage.UI): 基于Unity开发的桌面应用，用于为录播机台提供用户界面
- [alls_obs_ad](https://github.com/Kgym-Hina/alls_obs_ad): 可选的支持项。展示一个和后端同步的公告窗口，用于直播间中显示
- [ALLS.DirectStart](https://github.com/Kgym-Hina/ALLS.DirectStart): 可选的支持项。如机厅不能给机子持续供电，则使用这个程序进行直播自启动

## 接入

如需要想直接使用现成的成品，请提交 Issues 或使用 QQ 309109713 联系我提交机厅信息~

除了接入默认API以外，你也可以自行实现WebAPI的接口，并在编译 `alls_recorder` 和 `ArcadeLinkage.UI` 时对相应配置更改即可~

## 使用

### 预备条件

- 有一台公网能够访问的服务器 (如接入默认API则不需要)
- 有一台能直播推流的电脑
- 七牛云账号
- 店家对机台改装的允许
- 摄像头至少一枚（用于识别二维码，直播手元需要的摄像头不在这里提及）

### 硬件连接

请见 [HARDWARE](HARDWARE.md)

### 部署

1. 将 `OBS Studio`, `ArcadeLinkage.UI`, `alls_obs_ad`（可选）, `ALLS.DirectStart`（可选） 下载到直播机上
2. 配置好直播机和街机游戏的硬件连接和OBS设置
3. 开启`alls_obs_ad`，按提示配置好后可设置OBS窗口采集
4. 在 `OBS Studio` 中设置好直播需要的场景，并开启 Websocket 连接. 保持默认端口 `4455` 以及关闭鉴权
5. 打开目录 `%userprofile%\AppData\LocalLow\DeltaGames\ALLS_UI\` 新建 `config.json`，并按照[项目中文档](https://github.com/Kgym-Hina/ArcadeLinkage.UI)配置
6. 打开`ArcadeLinkage.UI`主程序，在开始画面测试摄像头是否正常工作。在确认正常工作后点击摄像头预览画面即可保存
7. 使用系统自带服务管理器（Windows 服务、systemd等）或启动脚本进行顺序启动，启动顺序从先到后如下

`alls_obs_ad`, `OBS Studio`, `ArcadeLinkage.UI`, `ALLS.DirectStart`

至此，客户端部署完毕，可以在 [alls_recorder](https://github.com/Kgym-Hina/alls_recorder) 中进行请求视频录制，下载已录制视频
