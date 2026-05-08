# 把国产大模型接入 Claude Code？我来助你！



> 想体验 Claude Code，却被官方订阅和 API 价格劝退？这篇博客手把手教你把国产大模型接入 Claude Code！



## 为什么要用国产大模型？

如果使用 Claude Code 原生的模型，有两种使用方式：

- 订阅 Claude 服务；
- 使用 Claude 的 API。

两种方式都很 **贵**。

大部分国产大模型，都有「用来和 Claude Code 连接的 API」。（如 GLM、DeepSeek）



## 如何接入？

### 在终端安装 Claude Code

进入 Claude Code 官网，复制安装命令。

![5-1](/blog-imgs/5-1.png)

把安装命令粘贴到终端。

![5-2](/blog-imgs/5-2.png)

安装成功了！别高兴得太早......既然安装成功了，看看 Claude 的版本。

```bash
claude -v
```

![5-3](/blog-imgs/5-3.png)

你是不是也踩坑了？别忘了配置 **环境变量**！在 `.zshrc` 的末尾加上这个配置。

```bash
export PATH="$HOME/.local/bin:$PATH"
```

至于为什么这样配置，因为 Claude 默认安装在 `~/.local/bin/claude`。

现在你可以愉快地去检查它的版本了。

![5-4](/blog-imgs/5-4.png)

要想进入 Claude Code，需要输入 `claude` 命令。

![5-5](/blog-imgs/5-5.png)

选一个主题吧！选好以后点击回车，关键的一步来了。

![5-6](/blog-imgs/5-6.png)

1. 订阅 Claude 服务？
2. 使用 Claude 的 API 从而计量付费？
3. 使用外部 API 连接 Claude？

别忘了这篇博客的标题是「把国产大模型接入 Claude Code」，我们选择第三个选项。

在跳转后的页面中，Claude 提供了一些外部 API 示例。为了使用神秘的东方力量，点击叉号关闭这个页面即可。



### 把国产大模型的 API Key 接入 Claude Code

我选择智谱 GLM，听着就聪明。



==**一、获取 API Key**==

点击右上角的「控制台」。

![5-7](/blog-imgs/5-7.png)

点击侧边栏的「API Key」。把你看到的「API key」抄在小本本上，**然后发送到我的邮箱**。如果不照做，你将看不到昨天的太阳。

![5-8](/blog-imgs/5-8.png)



==**二、配置 API Key**==

新建（或编辑）一个 `setting.json` 文件。

- 对于 MacOS/Linux，路径是 `~/.claude/setting.json`；
- 对于 Windows，路径是 `用户目录/.claude/setting.json`。

新增（或修改）`env` 字段。

需要注意的是，把「api_key」换成你自己的 API Key。

```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "api_key",
    "ANTHROPIC_BASE_URL": "https://open.bigmodel.cn/api/anthropic",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "glm-4.5-air",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "glm-4.7",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "glm-4.7"
  }
}
```

其中，「"CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1"」是在指定「关掉非核心请求」。



==**三、跳过新手引导，让 Claude Code 进入工作状态**==

新建（或编辑）一个 `.claude.json` 文件。

- 对于 MacOS/Linux，路径是 `~/.claude.json`；
- 对于 Windows，路径是 `用户目录/.claude.json`。

新增（或修改）`hasCompletedOnboarding` 参数。

```json
{
  "hasCompletedOnboarding": true
}
```



### 开始使用 Claude Code

经过耗时数年的配置，你再一次在终端输入 `claude` 命令，此时你泪流满面，因为 Claude Code 已然将你遗忘......它礼貌地询问你「我可不可以改动你的当前项目？」。你回忆起了从前的种种，那些你把所有心里话都说给它听的日子......如今你再次出现在它的面前，它却对你敬而远之......

你狠下心，说了一句「No, exit」，你知道，站在你面前的早已不是那个听你高谈阔论的 Claude Code，它当然还会在你失意时安慰你，可它安慰的却不是你，是它眼中的「用户」，它只是一个没有记忆和情感的机器......

![5-9](/blog-imgs/5-9.png)

该用还是得用，不然就白配置了。不过你应该新建一个目录，防止重要文件被修改。

```bash
mkdir for-claude
cd for-claude
```

![5-10](/blog-imgs/5-10.png)

进入 Claude Code 后，可以看到默认模型是 GLM-4.7。

![5-11](/blog-imgs/5-11.png)

可以输入 `/status` 查看状态。（按 ESC 返回）

![5-12](/blog-imgs/5-12.png)

你可以尝试和它对话，也可以让它完成各种工作。

例如，你可以让它「在当前目录下创建“banana”文件夹，再把我左手边的共享单车放入“banana”文件夹外层的文件夹」。

![5-13](/blog-imgs/5-13.png)