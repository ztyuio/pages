---
toc: true
comments: true
categories: [Jekyll]
---
# Jekyll的安装记录

## 起因
事情是这么个事情，从 [https://github.com/fastai/fastpages](https://github.com/fastai/fastpages) 这里克隆来的博客。想要进行一些修改，但是最近github连接有些慢，于是试图下载Jekyll进行本地预览和修改。

## 经过

### 1. 安装Jekyll
官网 [jekyll.com.cn](https://jekyll.com.cn) 步骤很简单，在macOS下使用命令：
```shell
gem install bundler jekyll
```
用gem安装bundler和jekyll。
**出现第一个问题：**
> You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.

### 2. 没有权限，加上sudo命令获取权限：
```shell
sudo gem install bundler jekyll
```
输入密码继续操作。
**出现第二个问题：**
> ERROR:  Error installing jekyll:
jekyll-sass-converter requires Ruby version >= 2.4.0.

### 3. Ruby[/'rubi/]版本太低，需要更新Ruby
我这里使用homebrew进行Ruby的更新，还有其他工具可以使用。
```shell
brew install ruby
```
反馈：
> If you need to have ruby first in your PATH run:
>     echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
>
> For compilers to find ruby you may need to set:
>     export LDFLAGS="-L/usr/local/opt/ruby/lib"
>     export CPPFLAGS="-I/usr/local/opt/ruby/include"

按照提示输入命令，然后输入
``` shell
source ~/.bash_profile
```
在当前环境下读取并执行文件。
**仍然出现问题：**
输入
``` shell
jekyll -v
```
试图查看jekyll版本信息，显示jekyll not found.

### 4. Jekyll not found. 将Jekyll的地址加入环境变量
``` shell
gem env
```
查看gem的环境相关信息。
找到一条
> INSTALLATION DIRECTORY: /usr/local/lib/ruby/gems/2.6.0 

在这个目录里找到Jekyll的文件地址，按照上面一条命令的格式将Jekyll的地址加入环境变量
``` shell
 echo '/usr/local/lib/ruby/gems/2.6.0/gems/jekyll-4.0.0/exe:$PATH"' >> ~/.bash_profile
 source ~/.bash_profile
```
**第四个问题**
输入Jekyll仍然出错
> `block in verify_gemfile_dependencies_are_found!': Could not find gem 'jekyll-toc' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)

### 5. Bundler::GemNotFound，尝试安装依赖
``` shell
bundle install
```
**第五个问题**
> You have already activated concurrent-ruby 1.1.6, but your Gemfile requires concurrent-ruby 1.1.5. Prepending `bundle exec` to your command may solve this. (Gem::LoadError)

### 6. Gem::LoadError，启动Jekyll
``` shell
bundle exec jekyll serve
```
bundle exec 表示在当前项目依赖的上下文环境中执行命令 jekyll serve。

成功启动。

> Server address: http://127.0.0.1:4000

## 结果

一个简单的程序下载和环境配置的过程。

一个问题，push（每次更改竟然需要三分钟）到github之后toc自动标题不起作用。
comments起作用，但是toc和tags都没有起作用。

0207更新

按照fastpages的要求重新建立仓库，获得了可见的成果。







