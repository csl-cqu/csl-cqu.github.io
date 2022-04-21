# Cyber Security Laboratory Website

这是重庆大学网络安全实验室的主页源代码仓库。该网站采用[Hugo](https://gohugo.io/)框架构建，并在[GitHub Pages](https://pages.github.com/)部署，网站整体框架从[LoveIt](https://github.com/dillonzq/LoveIt)模板修改而来。

## 快速开始
因为本网站采用[GitHub Action](https://github.com/features/actions)自动构建并发布，所以如果只是更新网站中的部分内容（例如修改团队成员信息、添加publication）则没有必要在本地配置开发环境，甚至没有必要将本仓库克隆到本地，而是简单的对data目录下的数据文件进行修改并提交即可。下面介绍一些常见维护场景的操作方法

### 添加 Publication
编辑data目录中对应年份的文件publications文件，目前有2020-2022以及用与存放更早期数据的publications0000.yaml。记录的格式如下：

```yaml
- title: "文章标题"
  highlight: 强调部分，例如"Best Paper", "Oral", "Spotlight"等
  authors: 文章作者
  publication: 期刊或者会议名称
  link: 文档连接（没有则不要此项）
  ccf_rank: CCF分级（没有则不要此项）
  cqu_rank: 实验室分级（没有则不要此项）
```

值的注意的是如果需要增加一个年份，则需要在data目录中创建对应年份的publicationsxxxx.yaml文件，然后编辑`layouts/shortcodes/publications-en.html`以及`layouts/shortcodes/publications-zh.html`，添加对应内容即可，例如增加2023则在`<h2 id="2022">2022</h2>`上方添加如下内容
```html
<h2 id="2023">2023</h2>
<ul>
    {{ range .Site.Data.publications2023 }}
        <li>
            <p><b><a href="{{ .link }}">{{ .title }}
                {{ if .highlight }}
                <span style="color: red;">
                    ({{ .highlight }})
                </span>
                {{ end }}
            </a></b></p>
            <p>{{.authors}}</p>
            <p><i>{{.publication}}</i>
                {{ if .ccf_rank }}
                , <b>CCF Rank {{.ccf_rank}}</b>
                {{ end }}
                {{ if .cqu_rank }}
                , <b>CSL@CQU Rank {{.cqu_rank}}</b>
                {{ end }}
            </p>
        </li>
    {{ end }}
</ul>
```

### 添加 Team Member
在data目录中team_en.yaml以及team_zh.yaml添加个人信息即可，格式如下：
```yaml
- name: 名字
  photo: 照片
  info: 职称
  email: 邮箱
  biography: 个人简介
  position: 身份，可选director、member、phd、master
  interests: 研究兴趣，只有phd和master需要
```
其中照片文件应该放置在static/team目录中。

### 发布新闻
在data目录中news_en.yaml以及news_zh.yaml中添加新闻即可，格式如下：
```yaml
- title: 新闻标题（支持在其中使用html标签）
  date: 发布日期
  icon: 一个Emoji图标（可选）
  author: 作者
  detail: 详情（可选，支持在其中使用html标签）
```

**注意**：每次添加新闻总应该添加在数据文件的最上方

### 发布学术沙龙
在content/seminars中创建一个新的文件夹，然后在其中添加index.en.md和index.zh-cn.md（可以只添加一个语言版本）具体格式参考content/seminars/basic-markdown-syntax。

### 维护首页
#### 修改文字内容
直接编辑content/_index.en.md和content/_index.zh-cn.md文件即可。

#### 修改轮播图
首先将需要的图片放置在static/slide目录中，然后编辑data/slide.yaml指定想要轮播展示的图片的文件名，这里图片的个数不受限制。

#### 修改Quick Links
编辑data目录中quick_link_en.yaml和quick_link_zh.yaml即可，格式如下：
```yaml
- title: 超链接文本
  link: 链接地址
```

## 本地开发
Step 1: 安装 Hugo，[参考文档](https://gohugo.io/getting-started/installing/)。

Step 2: 克隆仓库
```bash
# --recursive 选项是为了将主题submodule一并克隆
git clone --recursive git@github.com:csl-cqu/csl-cqu.github.io.git
```

Step 3: 完成开发
