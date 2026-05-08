# 本地安装 OpenClaw，并把它接入 QQ



> 如果你想在本地部署 OpenClaw，并把它接入 QQ 进行对话控制，也许这篇博客对你有帮助。我将会从安装 OpenClaw 开始，带你一步步完成配置、使用、接入QQ 机器人以及卸载 OpenClaw。



**前排提醒**：如果 OpenClaw 使用不当，存在极高的安全风险。建议通过虚拟机/云服务器/备用机使用 OpenClaw。



## 在终端安装 OpenClaw

进入 OpenClaw 官网，复制安装命令。

![6-1](/blog-imgs/6-1.png)

安装成功了。

![6-2](/blog-imgs/6-2.png)

弹出了使用协议，需要注意的是，**OpenClaw 存在安全风险**，如果使用不当，可能会出现误删文件、泄露数据等问题。如果你选择无视这些风险，那就选择「Yes」进入下一步。

![6-3](/blog-imgs/6-3.png)



## 配置 OpenClaw

在「快速开始 QuickStart」、「手动配置 Manual」和「从 Claude 导入配置」三个选项中：

- 如果选择「快速开始 QuickStart」，将会使用默认配置启动 OpenClaw，后续可以在终端执行 `openclaw configure`，根据使用体验再修改配置；
- 如果选择「手动配置 Manual」，将要提前配置 API Key、模型提供商、默认模型、权限设置、工作目录等内容；
- 如果选择「从 Claude 导入配置」，将会从 Claude 导入配置......

我想去吃饭了，所以我选择「快速开始 QuickStart」，点击回车。

![6-4](/blog-imgs/6-4.png)

不出意外的话，你将要选择 OpenClaw 使用的大模型。

![6-5](/blog-imgs/6-5.png)

我选择 DeepSeek，因为最近 DeepSeek-V4 预览版本正式上线并同步开源，能力值得赞叹！

获取 API Key 的方式很简单。

![6-6](/blog-imgs/6-6.png)

![6-7](/blog-imgs/6-7.png)

输入 API Key 并选择模型以后，将要连接聊天平台。此处可以直接跳过，先体验网页界面聊天，后续手动接入 QQ。如果你不想体验网页版，可以在此处直接接入聊天平台。

![6-8](/blog-imgs/6-8.png)

后续会询问「是否需要搜索服务」，此处需求不大，而且需要额外配置 API Key，如果后续产生需求，可以手动配置，此处暂时跳过。

![6-9](/blog-imgs/6-9.png)

后续会询问是否给 OpenClaw 安装技能包，如果安装，OpenClaw将会解锁各种具体能力。我们点击「Yes」，并按需选择技能包。

此处的「ClawHub」是 OpenClaw 的官方技能市场，安装 ClawHub 以后，OpenClaw 可以随时搜索并安装社区里的技能包，从而扩展自己的能力。

值得注意的是，这种行为存在安全风险，部分技能包中携带着恶意代码。

点击空格从而选中技能包。

![6-10](/blog-imgs/6-10.png)

至于安装技能包的工具，选择 npm 即可。

![6-11](/blog-imgs/6-11.png)

后续会询问是否配置众多额外服务。为了快速上手体验，建议一律不配置，如果后续产生对应的需求，再手动配置也不迟。

最后选择在何处使用机器人，在网页中使用较为直观，建议选择在网页中使用。

![6-12](/blog-imgs/6-12.png)

选择以后，浏览器自动在网页中打开 OpenClaw 的控制面板。



## 在网页中使用机器人

![6-13](/blog-imgs/6-13.png)

可以控制它执行文件读写、终端命令执行、网页搜索等操作。

![6-14](/blog-imgs/6-14.png)

为了在 QQ 和机器人对话，需要把 OpenClaw 接入 QQ。



## 把 OpenClaw 接入 QQ

在浏览器搜索「QQ 开放平台」。

![6-15](/blog-imgs/6-15.png)

登录后，点击「创建 QQ  机器人」。

![6-16](/blog-imgs/6-16.png)

依次把三行命令复制到终端中执行即可。

![6-17](/blog-imgs/6-17.png)

接下来就可以在 QQ 上控制机器人了。

![6-18](/blog-imgs/6-18.png)



## 彻底卸载 OpenClaw

在终端执行一条命令，一路回车即可删除。 

```bash
openclaw uninstall
```

![6-19](/blog-imgs/6-19.png)

不过有些内容不会自动删除，需要额外执行命令。

对于 Mac/Linux 操作系统：

```bash
openclaw gateway stop
openclaw gateway uninstall
rm -rf "${OPENCLAW_STATE_DIR:-$HOME/.openclaw}"
npm rm -g openclaw || pnpm remove -g openclaw
rm -rf /Applications/OpenClaw.app
```

对于 Windows 操作系统：

```bash
openclaw gateway stop
openclaw gateway uninstall
schtasks /Delete /F /TN "OpenClaw Gateway"
Remove-Item -Recurse -Force "$env:USERPROFILE\.openclaw"
Remove-Item -Force "$env:USERPROFILE\.openclaw\gateway.cmd" -ErrorAction SilentlyContinue
npm rm -g openclaw
# 如果是用 pnpm 安装的，改为执行：pnpm remove -g openclaw
```

![6-20](/blog-imgs/6-20.png)
