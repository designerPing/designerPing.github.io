---
layout: post
title: "盲人摸象般探索，终于发表第一篇GitHub文章"
date: 2024-10-11
categories: blog
---

经过一早上的盲人摸象式的操作，终于按照设想的初步框架搭建出了个人博客网站，成功上传了第一篇博客文章。
下文记录我的操作方式：

- ChatGPT 询问怎么搭建 GitHub 个人博客，会给出详细的页面操作步骤：
    - 注册 GitHub 账号；
    - 创建仓库；
    - 在 Settings 的 Pages 里设置域名，具体见官方文档 <https://docs.github.com/en/pages/quickstart>；
    - 至此，一个空白的博客已创建。
- 接着，把博客模板应用到个人博客上，上述的官方文档有提及，但是我看得很模糊，于是继续问 ChatGPT。
    - 首先把个人博客仓库保存在本地，同时把模板的仓库 clone 下来，我选择的是 minimal；
    - 接着把配置文件夹复制到本地的个人仓库里，主要包括四个文件夹：_includes, _layouts, _sass, _assets。
    - 接下来开始边预览边修改内容，本地预览需要安装一些 Jekyll 的插件，我直接用 git 上传到 GitHub 上预览，也很方便。`git status`, `git add .`, `git commit -m "xxx"`, `git push origin main`，从不认识这几个命令，到盲打，很有意思。
- 首页显示文章列表。官方提供的几个模板里，没有显示文章列表，继续调整。
    - 创建一个 `_posts` 的文件夹，创建完文件夹后，需要调整 `_layouts` 文件夹里的 `default.html` 内容。
    - 模板默认加载的是根目录的 `index.md` 文件，需要把 `<section>` 里的内容做调整：
    
      ```html
      <section>
        <h2>Blog Posts</h2>
        {% raw %}{% for post in site.posts %}{% endraw %}
          <!-- <p>Debug: Found post with title "{{ post.title }}"</p> -->
          <article>
            <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
            <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
            <div class="post-excerpt">
              {{ post.excerpt }}
            </div>
          </article>
        {% raw %}{% endfor %}{% endraw %}
      </section>
      ```

    - 接着在 `_posts` 文件夹里创建几个 `.md` 文件，文件格式需要统一为 `YYYY-MM-DD-title.md`，并且头部需要加上：

      ```markdown
      ---
      layout: post
      title: "我的第一篇文章"
      date: 2024-10-11
      categories: blog
      ---
      ```
    
    - 正常情况下，在首页可以看到文章列表了，记住时间不能是未来，否则当前没法展示预览。
- 文章详情页，上述操作完，文章的链接显示的内容和首页一样，这时需要调整 `post.html` 的样式：
    - 找 ChatGPT 生成一个够用的样式就行；
    - 图片的显示，图片路径的问题，使用 `![示例图片assets](/assets/img/sunshine.webp)`，其余总结如下：

      ```markdown
      ![示例图片images](/_posts/images/sunshine.webp | relative_url) / 不能展示图片

      ![示例图片没带相对路径images](/_posts/images/sunshine.webp) / GitHub 仓库可以，但是网页不行

      <img src="{{ "_posts/images/sunshine.webp" | relative_url }}" alt="示例图片html" /> / 不能展示图片

      ![示例图片assets](/assets/img/sunshine.webp) / 可以展示图片

      ![绝对路径图片](/designerPing.github.io/assets/img/sunshine.webp) / 不能展示图片
      ```

至此，博客搭建和文章上传算是圆满完成，*★,°*:.☆(￣▽￣)/$:*.°★* 。

————————————————————
在上传博客文章后，发现文章页面的样式不尽如人意，于是调整，结果默默无闻地调整了将近2天时间。
总结出来的经验：
- 不要单纯依靠AI输出，会前后矛盾，要了解AI修改了哪些地方的代码；
- 如果是简单的问题，不要已有的复杂情况修改，而是先归零后，逐步用加法控制变量，以达到预期效果。

这样一个简单的样式调整，如果是前端开发，估计1分钟的事情，而小白的我花了2天时间。
没关系，逐步找准自己的节奏，不要妄想一步到位。