--- 
title: flask-babel i18n,i10n插件
layout: post
category: python
---

## 简介
[flask-babel][1] 是一个基于python babel 开发的flask插件, 用来解决的flask的国际化问题. 底层是gettext,基本所有的多语言都是用这个解决方案的.

## 安装
很简单的`pip install flask-babel`,顺便会安装上pybabel, 一个很好的工具, 下面会用到.  
另外[poedit][2]是一个非常好用的编辑po文件的工具, 其翻译提示功能能把基本的翻译都搞定.

## 配置
babel.cfg文件

```
[python: **.py]
[jinja2: **/templates/**.html]
slient=false
encoding = utf-8
extensions=jinja2.ext.autoescape,jinja2.ext.with_,webassets.ext.jinja2.AssetsExtension
```
当然如果没有使用webassets的话`webassets.ext.jinja2.AssetsExtension
`不用写    
这样配置文件就好了

## 模版文件
在模版文件里\{\{ _("en") \}\}这样的表示需要翻译的, 一会儿会自动生成一个message.pot文件里面就是需要翻译的内容. 其实这样\{\% trans \%\} en \{\% endtrans \%\}也行的, 这样大段文字就比较方便了.

## 提取pot文件, 生成po文件,编译成mo文件

```
$1 pybabel extract -F babel.cfg -o message.pot .
$2 pybabel init -i message.pot -d translations -l zh_CN 
```
然后会生成一个messages.po文件, 我们用poedit打开这个文件,将里面的翻译搞定,然后:    

```
$3 pybabel compile -d translations
```

如果以后页面有变化, 重新运行$1, `pybabel update -i message.pot -d translations`, $3 就行了.

## 配置flask项目
按照官网

```
from flask import Flask
from flask.ext.babel import Babel
app = Flask(__name__)
app.config.from_pyfile('mysettings.cfg')
babel = Babel(app)

@babel.localeselector
def get_locale():
    return request.accept_languages.best_match(['en', 'zh'])
```
就可以了, 这样会根据http的header去判断用户的语言.

* 但是我不喜欢这样做, 我喜欢像apple官网那样, 后面根据参数去选择语言. 这里有一个例子[simple][3]不错.

```
@app.before_request
    def before_request():
        if request.view_args is None:
            if 'lang_code' not in session.keys():
                return redirect('/zh' + request.full_path)
            else:
                return redirect('/'+session['lang_code']+request.full_path)

@bp.url_defaults
def add_language_code(endpoint, values):
    if current_app.url_map.is_endpoint_expecting(endpoint, 'lang_code'):
        values['lang_code'] = session['lang_code']
        g.lang_code = session['lang_code']
    values.setdefault('lang_code', g.lang_code)


@bp.url_value_preprocessor
def pull_lang_code(endpoint, values):
    session['lang_code'] = values.pop('lang_code')
    g.lang_code = session.get('lang_code', None)                
```
基本就是这样,使用url参数取得语言, 然后把语言参数去掉,传给views

## 后记
这东西使用起来还算方便, 国外的小团队开发的东西都会提供好几种语言,反观国内, 国际化做的实在差劲.


[1]:http:https://pythonhosted.org/Flask-Babel/ "文档官网"
[2]:http://poedit.net/ "Poedit 官网"
[3]:https://github.com/shankararul/simple-babel "flask-babel 例子"