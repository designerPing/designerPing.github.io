---
layout: post
title: "盲人摸象般探索，终于发表第一篇GitHub文章"
date: 2024-10-11
categories: blog
---

经过一早上的盲人摸象式的操作，终于按照设想的初步框架搭建出了个人博客网站，成功上传了第一篇博客文章。
下文记录我的操作方式：

- ChatGPT询问怎么搭建Github个人博客，会给出详细的页面操作步骤：
    - 注册Github账号；
    - 创建仓库；
    - 在setting的Pages里设置域名，具体见官方文档https://docs.github.com/en/pages/quickstart；
    - 至此，一个空白的博客已创建。
- 接着，把博客模板应用到个人博客上，上述的官方文档有提及，但是我看得很模糊，于是继续问ChatGPT。
    - 首先把个人博客仓库保存在本地，同时把模板的仓库clone下来，我选择的是minimal；
    - 接着把配置文件夹复制到本地的个人仓库里，主要包括四个文件夹：_includes, _layouts, _saas, _assets。
    - 接下来开始边预览边修改内容，本地预览需要安装一些Jekyll的插件，我直接用git上传到GitHub上预览，也很方便。git status, git add . , git commit -m "xxx" , git push origin main, 从不认识这几个命令，到盲打，很有意思。
- 首页显示文章列表。官方提供的几个模板里，没有显示文章列表，继续调整
    - 创建一个_posts的文件夹，创建完文件夹后，需要调整_layouts文件夹里的defaul.html 内容。 
    - 模板默认加载的是根目录的index.md文件，需要把section里的内容做调整
    ''' 
       <section>
        <h2>Blog Posts</h2>
        {% for post in site.posts %}
          <!-- <p>Debug: Found post with title "{{ post.title }}"</p> -->
          <article>
            <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
            <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
            <div class="post-excerpt">
              {{ post.excerpt }}
            </div>
          </article>
        {% endfor %}
      </section>
      '''
      - 接着在_posts文件夹里创建几个md文件，文件格式需要统一 YYYY-MM-DD-title.md 格式，并且头部需要加上：
      '''
---
layout: post
title: "我的第一篇文章"
date: 2024-10-11
categories: blog
---
'''    
      - 正常情况下，在首页可以看到文章列表了，记住时间不能是未来，否则当前没法展示预览。
- 文章详情页，上述操作完，文章的链接显示的内容和首页一样，这时需要调整post.html的样式
    - 找ChatGPT生成一个够用的样式就行；
    - 图片的显示，图片的路径问题，使用'![示例图片assets](/assets/img/sunshine.webp)',其余总结如下：
'''
![示例图片images](/_posts/images/sunshine.webp | relative_url) /不能展示图片

![示例图片没带相对路径images](/_posts/images/sunshine.webp) /github仓库可以，但是web不行

<img src="{{ "_posts/images/sunshine.webp" | relative_url }}" alt="示例图片html" /> /不能展示图片

![示例图片assets](/assets/img/sunshine.webp) /可以展示图片

![绝对路径图片](/designerPing.github.io/assets/img/sunshine.webp) /不能展示图片
'''

至此，博客搭建和文章上传算是圆满完成，*★,°*:.☆(￣▽￣)/$:*.°★* 。