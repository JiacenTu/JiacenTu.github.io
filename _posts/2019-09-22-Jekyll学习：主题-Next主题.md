---
title:  "Jekyll学习：主题"
date: 2019-09-22 15:02:00 +0800
categories: jekyll
tags: jekyll 主题
---
> 摘要：如何更改主题

## 通过配置文件更改主题

jekyll的主题可以自由更换，一种是在 [rubygems](https://rubygems.org) 上搜索jekyll-theme，如果是国内，可以登陆 [国内rubygems](http://gems.ruby-china.com/) 。搜索到喜欢的主题后，就可以在配置中更改配置，从而更改主题。

操作步骤如下：

1. 更改Gemfile

	在[目录结构](/jekyll/Jekyll学习-目录结构)一文中，介绍了Gemfile文件是用来管理依赖的。jekyll默认主题是 minima ，所以在Gemfile中有如下默认配置
	```yml
	# 默认主题minima
	gem "minima", "~> 2.5"
	```

	更换主题，可以看作添加了一个主题依赖，所以在Gemfile文件中添加如下配置
	```
	# 以jekyll-theme-primer为例
	gem 'jekyll-theme-primer', '~> 0.5.3'
	```

2. 更改_config.yml
	
	\_config.yml是配置文件，需要在这里指定使用主题，更改如下配置
	```yml
	# 默认
	theme: minima
	# 更改为
	theme: jekyll-theme-primer
	```

3. 重新运行服务器
	
	依次运行以下命令
	```sh
	$ bundle update
	$ bundle install
	$ bundle exec jekyll serve --trace
	```
	理想情况下是能够顺利运行成功，但是，没错这里有但是，前提是gem的依赖不发生冲突。

	在我写这篇文章的时候是2019年9月份，jekyll已经更新到4.0.0，自动生成的依赖也都是比较新的版本，但是大部分主题都是较早的时候开发出来的，他们依赖的版本都比较老，各种依赖之间发生了新老版本的冲突，我找到的主题需要的jekyll版本大多是3.5，3.7，但是自动生成的Gemfile中，例如tzinfo依赖jekyll版本在3.7 到 5.0，导致无法运行。这种情况就需要挑选依赖不冲突的主题，或者对自动生成的Gemfile文件进行更改。

	本人新手，折腾了好几个小时勉强运行了起来，但是效果不是很美观，所以就不列出自己的配置了。

	
## 直接clone主题

以本人为例，本人使用的是[Next主题](http://theme-next.simpleyyt.com/)，简约而不简单。步骤如下：

1. clone项目
	
	从github上clone项目至本地，附链接：[Next主题](https://github.com/Simpleyyt/jekyll-theme-next)

2. 运行项目
	
	进入项目根目录下，依次运行以下命令
	```sh
	$ bundle update
	$ bundle install
	$ bundle exec jekyll serve --trace
	```

3. 本地显示
	
	本地访问 lhttp://localhost:4000
	

