# 基于 n8n 全自动发布微信公众号

## n8n 是什么

<div align="center">
  <img width="700" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://raw.githubusercontent.com/n8n-io/n8n/master/assets/n8n-screenshot-readme.png" />
</div>


n8n 是一个开源的自动化 AI 工作流平台，让我们可以避免通过编写代码的方式完成所需要做的工作，比如：

- 自动化发布微信公众号
- 数据分析 + 生成报表
- 爬虫（比如价格监控，比如价格变化的时候通知我）
- 等等......

## 操作流程

目标：让 AI 自动作诗并自动发布到公众号上

### 前置准备

#### 1. 安装 node 环境

直接去[官网](https://nodejs.org/zh-cn/download)，按照官网的说明进行安装

<div align="center">
  <img width="600" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/703c677a-8c70-4d43-8122-3d0e7e85f691" />
</div>

#### 2. 启动 n8n

```
npx n8n
```

然后按 `o` 就可以自动打开浏览器，然后就可以看到登陆的页面

<div align="center">
  <img width="700" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/c59b3f4b-98d4-4231-a4af-886b3726babd" />
</div>

#### 3. 安装社区节点

在左下角点击 `...` -> settings

<div align="center">
  <img width="434" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/8a85122c-a120-4cec-9f80-dd9e6009dd85" />
</div>

然后点击 `Community nodes` -> `Install`

<div align="center">
  <img width="700" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/97663bbb-d655-4c63-8dd4-e3e72b5f0832" />
</div>


在打开的弹窗中搜索 `n8n-nodes-wechat-offiaccount` 然后点击 `Install`

<div align="center">
  <img width="400" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/be6dd8e7-8a11-425a-8482-b4b5b5f0637d" />
</div>

回到主页可以搜索到 wechat 相关的工具就说明已经安装成功了！

<div align="center">
  <img width="700" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/872555b5-51f7-4d77-85a0-fee0ce1bb3ff" />
</div>

#### 4. 跑通创建草稿流程

##### 跑通上传素材

首先上传草稿需要用到图片作为封面，为了简单演示我们可以先用本地的图片（后续也可以使用诸如 Nano Banana 生成后插入）

我们需要找到 `Read/Write Files From Disk` 节点

<div align="center">
  <img width="300" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/c5aa89c7-3741-4440-9a4f-3a7ccaca5ac0" />
</div>

可以任意选一张本地的图片，然后点击 `Execute Step` 后就像我这样了：

<img width="2880" height="1624" alt="CleanShot 2025-11-02 at 23 49 07@2x" src="https://github.com/user-attachments/assets/343095a6-5917-4343-8ad5-988ba8f3d1ce" />

接下来我们需要把图片上传到公众号平台上，找到 `Wechat Official Account Node` 找到 `素材 新增其他类型永久素材`

<div align="center">
  <img width="300" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/29a9811f-d1cc-4290-854a-603136b53347" />
</div>

为了在执行的过程中正确知道要上传到哪个公众号上（而不是其他人的），我们需要拿到自己微信公众号的 `AppID` 和 `AppSecret`，因为背后其实就是调用微信平台的接口，需要鉴权

我们在登陆微信公众号后点击`设置与开发` -> `开发接口与管理`

<img width="2880" height="1630" alt="CleanShot 2025-11-02 at 20 04 24@2x" src="https://github.com/user-attachments/assets/32d0107a-1159-4ae5-9b17-45a319f8cc76" />

然后在`基本配置` -> `账号开发信息` 里就可以看到了

然后回到刚才的节点，点击下面这个按钮把 `AppID` 和 `AppSecret` 填上就好了

<img width="2880" height="1624" alt="CleanShot 2025-11-02 at 23 56 20@2x" src="https://github.com/user-attachments/assets/c843eb03-7c30-4afd-ba60-f936c2e6743a" />

然后把这两个节点连起来，就像我这样


<div align="center">
  <img width="250" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/756a25ae-1211-4347-b595-654ed9613fd5" />
</div>

还是点击 `Execute Step` 就可以在素材库里找到了

<img width="2880" height="1622" alt="CleanShot 2025-11-02 at 23 54 13@2x" src="https://github.com/user-attachments/assets/2a1f0c79-61a4-4089-b7e7-e43554b7c333" />


`Wechat Official Account Node` 点击 `新建草稿`

<div align="center">
  <img width="300" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/b25bf852-f23b-47eb-91cb-77d21ca5a683" />
</div>

##### 跑通上传内容

现在我们继续去 `Wechat Official Account Node` 找到 `新建草稿`

```
[{
   "article_type":"news",
   "title": "每日一诗",
   "content": "床前明月光",
   "thumb_media_id": "{{ $json.media_id }}"
}] 
```

注意这里的 `thumb_media_id` 就是上一个节点，也就是上传素材库里的一个字段

<img width="2880" height="1630" alt="CleanShot 2025-11-03 at 00 00 53@2x" src="https://github.com/user-attachments/assets/b0724f8f-efbd-4d33-9c76-d762f483f634" />

最后我们继续点击 `Execute Step`，不出意外的话现在我们就可以在草稿箱里找到我们刚才创作的诗句了

<img width="2880" height="1630" alt="CleanShot 2025-11-03 at 00 03 25@2x" src="https://github.com/user-attachments/assets/1d3b7e47-4ce8-4c00-9224-76f0bffa092d" />



### 5. 打通 AI 创作

现在我们已经可以自动化发布文章了，接下来我们要做的一个事情就是彻底解放双手，创作也让 AI 来搞

找到 AI Agent 节点

<br />


<div align="center">
  <img width="300" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/9ff2c468-776c-44cd-81b0-51c52454b7c2" />
</div>

<br />

然后我们需要给这个 Agent（智能体）配置一个模型

<br />

<div align="center">
  <img width="300" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/a7e712f3-f768-42e6-88a0-4907328c37fe" />
</div>

<br />


你可以选任何模型，比如 DeepSeek、ChatGPT、Gemini 等等，但是这里需要你的 API Key，比如我这里是 DeepSeek

<br />

<img width="2880" height="1624" alt="CleanShot 2025-11-03 at 00 07 57@2x" src="https://github.com/user-attachments/assets/3c038d60-f1db-483b-8064-ea72191ad941" />

<br />

创建账号后需要把你从 [DeepSeek 官网](https://platform.deepseek.com/api_keys)获取的 API Key 配置上

最后我们可以把这些节点全部连接起来，并在最前面配置上 `On chat message` trigger

<br />

<div align="center">
  <img width="700" alt="CleanShot 2025-11-02 at 19 45 52@2x" src="https://github.com/user-attachments/assets/43cb542b-aebf-463d-ad17-bfcd3d90ecc1" />
</div>

<br />

同时为了 AI Agent 创作的诗句能被正常的使用到，我们需要修改一下新建草稿节点

<br />

<img width="2880" height="1626" alt="CleanShot 2025-11-03 at 00 27 20@2x" src="https://github.com/user-attachments/assets/8bd3d34b-f993-4245-b14f-ccb45b74c25a" />

<br />


```
[{
   "article_type":"news",
   "title": "每日一诗",
   "content": {{ JSON.stringify($('AI Agent1').item.json.output)}},
   "thumb_media_id": "{{ $json.media_id }}"
}] 
```

<br />

<img width="2872" height="1626" alt="CleanShot 2025-11-03 at 00 28 04@2x" src="https://github.com/user-attachments/assets/b8c05b2d-5154-4575-805d-9235ebeb7a07" />


### 总结

我们介绍了从用户需求到 AI 创作再到发布公众号的整个核心流程。基于这套流程你可以继续扩展，例如：

- 更美观的公众号排版（需要让 AI 生成 HTML 格式的文章，感兴趣的可以提 Issue 我后面再创作一篇）
- 在创作前你自动爬取当日最新的网络数据
- 定时发布、发布以后邮件通知你
- Multi Agent（增加一个或多个做更多事情，例如对文章进行 review）
- 等等...




