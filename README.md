# learn_django
学习Django的笔记
好久没来了！我指的是学习Python这件大事。
之前按照书上的说法，做web应用程序，最好用Django,然后搭建一个虚拟环境，所以后来偶遇了 Anaconda。
说说 Anaconda 的一些命令吧， conda list,列出所有安装在conda中的包，conda env list,查看当前有哪些虚拟环境，默认有一个（base）的环境
接着创建一个虚拟环境，通常要加上python的版本，( conda create -n env_name python=3.6 ) 括号内的指令让你创建一个 3.6版本的虚拟环境
----接着，要激活该环境，没办法，我也纳闷，为什么不是创建了就等于激活了，这个不管，还是需要按照步骤来的，在(Linux下激活：source activate env_name)
(windows 下激活：activate env_name)，退出的方法是 （Linux:source deactivate, windows:deactivate）
接下来肯定就是安装 django 啊！！！在进入虚拟环境后，安装django , pip install django==1.8 (版本号 ，虽然现在2.0以上了，不过暂时还是1.8全面)
试试吧，2.0版本应该可以的，不过暂时先1.8,听说是 2.0的路由完全变了，也不兼容1.8的，好了，装完之后，输入 conda list,就可以看到了。
----

然后就是创建一个工程了(django程序)，也许你会说项目，不过 工程 比较适合吧。
1.输入命令，django-admin startproject project_name_app, 当然了，在该工程名字下面，还有一个一模一样的工程名字，为什么呢，首先，第一个是我们的工程名字，其实可以理解为我们的公司的名字，第二个是我们公司的总裁部门，总裁部门里面有 manage.py urls.py settings.py 还有一个，嗯，总之有4个吧，总裁部门有4个秘书，太棒了。要记住的是，在公司还有其他部门，所以以后的部门和总裁一样，处于平行的，比方说，软件部门，那么总公司文件夹下，就有 总裁部门，软件部门，嗯，他俩是平行的，而不是软件部门在总裁部门里面，明白了吧。
2.启动程序啊，不过你需要确定你在总裁部门里面先，就是如今到总裁文件夹（cd 总裁文件夹），然后输入命令 python manage.py runserver, 说说 runserver,因为manage.py 是特殊的，通常我们运行一个 py 文件，就是 python .py ,而 manage 呢，是 想根据你执行什么命令的，所以需要看你的需求,如果你看到一些命令，且包括
http:127.0.0.1:8000 那么恭喜你，成功了，打开你的浏览器，输入网址就行了。''''补充一句，在你打开网页去看的时候，为了继续工作，你打开第二个终端窗口，此时你依然要进入到虚拟环境才行，所以到你创建虚拟环境的那个目录，然后输入命令（conda activate env_name）,切记不要输入错了虚拟环境的名字，不然就进不去了，后续的工作也就无法展开了。。。

提醒一下，进行到上面的一步，如果打算在 pycharm 中运行的话，需要重新配置，很简单啊，因为你第一步创建的时候加了 python 的版本啊，所有你来到 pycharm，肯定是要配置虚拟环境下面的 python 才行啊，具体配置， File-settings-exsting-preter-（因为是conda,所以在安装anaconda 目录下面的 envs目录 下的 python.exe 对，选择这个就行了）。接着 右键 manage.py debug-run, 会发现提示错误，所以在右上角 manage 下拉三角符号 点击一下，edit configurations,
parameter:runserver,再重新 debug-run 就行了。

路由系统-urls, 包括1，还记得我们说过吧，总裁部门，里面都是秘书，秘书吧，负责一些文案，负责开会时间吧，就是一些很简单的议事会程。想想，我们要新开一个部门，比如说创建一个app,那意思是 一个负责业务或者一类具体业务的模块 的部门吧，就是要来干事的，所以我们输入命令 python manage.py startapp teacher,比如我们创建一个讲师团队，对，就是负责讲课的，这就是一个具体的业务。（提示：会多了一个 teacher 文件夹）,2，路由，按照具体的请求url，导入到一个相对应的业务处理模块的一个功能模块吧，打个比方，你去腾讯这个公司招人，门卫，绝对会问你要找谁吧，你说找工程部的老王，那就指定到某个房间去了，对不。

---lawan处理这个 urls 的 函数吧，可以理解吧，就是在总裁办公室里的 urls.py ，这个文件中的 urlpattern=[url(r'normalmap/', do_normalmap)],
好了，我们写了具体的路由，相当于去哪里找谁的一个地址，并且由 do_normalmap 来接待你，不过别忘记了，在你去写 do_normalmap 之前，这里必须导入那个办公室的电话号码先啊，毕竟你没有拨通，怎么保持通话先，是吧，所以我们 在 urls.py 下面写 from teacher import views as tv, 之前用 tv 是因为别和 django里面的原来的文档名字引起冲突，既然引入电话了，那么 urlpattern 里面的 url,也必须相应改为 tv.do_normalmap.
----


话说，好像还没说过究竟用 django，用来做的是那些方面吧？昨晚听课程后，仔细想想，如果js是管理前端的，那么django则是后端的，处理业务逻辑的。
---
接着在你创建 一个具体业务后，这个业务肯定有内容吧，别人肯定要访问你的，而内容就是 views.py, 那么别人就是通过 总裁部门里面的 urls 找到你的，至于你的具体地址，也就是哪一层楼哪一房间号，就是具体的网址 （比如 xx.com/sourorange/) 这个 sourorange 就是你的网址，那么人家进来你的网址，你要有东西给人家看吧，于是你就在业务块 也就是 views.py 里面写一些类似欢迎游客来你办公室的信息 ，在 views 里面 写 (from django.http import HttpResponse), 没错，需要写这么一句。接着，写一个函数，这个函数接受一个类型为 HttpRequest 的参数 ：
def do_normalmap(request):
  打印一句话，目的是在调用的时候，看命令行有没有执行这个函数
  print('you are in .. position')
  然后，这句话是肯定要写的，毕竟要返回东西给人家看看
  return HttpResponse('This is normalmap')

---好了，上面是我们学习的第一个路由，其实相当于，你打开github网站，返回一个页面给你，只不过我们暂时是返回一句话而已，内容不一样，但是大纲是一样的。接着再写一个路由，如果说上面那个路由是1.0版本，那么现在要写一个2.0版本，类似 （.../.../...） , 不难的，只是添加了参数而已，比如我们要在 urls.py 中，再写一个路由，就写 ulr(r'^withparam/?P<year>[0-9]{4}/?P<month>[0-9]{1,2}', tv.withparam) , 那么在views中，我们就应该写 withparam 函数了吧，所以写上:
  def withparam(request, year, month):
    return HttpResponse('This is with param {0}, {1}'.format(year, month))
  
 对，我们第二个带有参数的 路由，就是这样滴，然后再去网页输入 127.0.0.1:8000/withparam/2018/11 ,这样就可以返回信息了。


--------

走到这里，我们要想想，如果所有的路由都放在主路由，那么主路由会变得十分臃肿，就是道路会很堵，我们知道，项目中包括一个或者多个应用，每个应用都有对应的路由，所以，每个应用自己建立一个子路由会更加靠谱，然后去和主路由说一声，我们自己搭建，主路由你给我们通行证就好，其实这么做会更加的高效，并且通车率会大大提高，这是我们推荐你这么做的。

假设，我们要再写一个路由，那么，按照最开始的做法，就是直接在主路由添加路由，然后在应用的视图文件中写下对应的函数。现在，我们要改变这个做法，直接在应用中新建一个文件，比如你的应用是 teacher,那么文件名最好叫做 teacher_url,而不是和主路由的名称重复，当然了，除非你确实不会和主路由搞混；接着你需要去主路由登记一下，好让你的 teacher_url 直接通过，嗯，主路由要登记，方法还是照样，打开 urls 文件，导入应用中的子路由，也就是（from teacher import teacher_url）,再在 urlspattern 列表中(通常还是再末尾)，添加所谓的业务逻辑（也就是人家访问你的网址），比如添加:
url('r^teacher/', include(teacher_url)),既然在主路由下我们已经登记了，那么现在回到子路由中，也就是 teacher_url 文件，该文件的内容差不多和主路由一样的，所以你可以先复制主路由的内容进来先，然后我们在思考一下，还记得我们一开始的方式吗，没错就是写路由啊，写完了去 视图层 再写函数啊，这里也是一样的逻辑，只不过我们写的是子路由，然后要删除其余的路由，所以写法是 1, from . import views 2, urlspattern=[url(r'canglaoshi/', views.jiangshi),]
,   3， 又要去 views 文件了，肯定是写 jiangshi  这个函数了啊，
<pre>
def jiangshi(request):
  return HttpResponse('这个是新的子路由，不拥堵的')
</pre>  
  现在呢，去访问网址试试，比如127.0.0.1:8000/teacher/canglaoshi, 试试看吧
  
------ -- --

接着，假设我们要访问 127.0.0.1:8000/book/page-8 ,想想，那部分是不变的，哪部分是经常变动的，很明显，第几页，是会经常变动的，不可能直接第8页啊，所以这里就涉及到嵌套参数了，
## 捕获某个参数的一部分，
- 例如 URL index/page-3, 需要捕获数字3作为 参数，
'''
  url(r'index_1/(page-(\d+)/)?$', tv.index_1) # bad
  url(r'index_2/?:page-(?P<page_number>\d+)/)?$', tv.myindex_2) # good
'''
- 上述例子，会得到两个参数 ，但是 ?: 表示忽略此参数。
- 具体的实现是，在主路由中的<strong>urlspattern</strong>中编写一句： url(r'^book/(?:page-(?P<page_number>\d+)/)?$', tv.nestparam),注意一下，这里的 page_number ，是一个参数，应该和函数里面的那个参数保持一样， 然后再 视图文件 views 中，写一个 nestparam 函数
<pre>
def nestparam(request, page_number):
  return HttpResponse('Page number is {0}'.format(page_number))
</pre>
- 现在去网址输入 127.0.0.1:8000/book/page-10 试试看吧，这里的数字，你可以随便写

## 传递额外参数
- 参数不仅来自于URL，还可能是我们自己定义的内容
  '''
    url(r'extrem/$', tv.extremParam, {'name':'xiaoming'}),
  '''
- 附加参数同样适用于 include 语句，此时对 include 内所有都添加
- 具体的实现是，在主路由中的 <strong>urlspattern</strong> 中添加一句： url(r'^yourname/$', tv.extremParam, {'name': 'xiaoming'}), 这句话的意思是 传递了一个参数为 name , 值为 xiaoming 的数据到网址中，接着在 views 文件中编写 函数 extremParam:
<pre>
def extremParam(request, name):
  return HttpResponse('This guy called {0}'.format(name))
</pre>
- 输入 127.0.0.1:8000/yourname/，就可以看到效果了

## URl 的反向解析
- 防止硬编码 （也就是 用一个变量去赋值，而不是重复用某一个值，因为直接修改变量更简单）
- 本质上是对 每一个 URL 进行命名 （url(r'.....',tv...., name='somevalue'), 这里的 变量 name 的值 就是该 URL 的 名字）
- 具体写法：在 主办公室 urls.py 中继续添加一句，url(r'^iknowyourname/$', tv.revParse, name="askname"), 然后在  teacher 应用里的 views.py 视图文件中，首先，我们要写一句来引入反向解析这个函数，from django.core.urlresolvers import reverse ,（注意了，该reverse 函数，接受的是一个值），接着写一个函数：
<pre>
def revParse(request):
  return HttpResponse('Your requested URL is {o}'.format(reverse('askname')))
</pre> 
- 好了，去网址试试 127.0.0.1:8000/iknowyourname , 看完结果后，再把网页改成 knowyourname, 试试，有意思吧,<strong>注意，必须在视图函数中修改url()中的网址为 url(r'knowyourname/$', ..., ...), 才可以在网页中调试网址。


## views 视图，即 视图函数
- 接收 web 请求，然后返回 web 响应的事物处理函数
- 具体的写法，和之前介绍的路由 是一样的，大概就 三步，第一，在主路由中写 url(r'...', tv.hanshuming), 第二，在视图函数中views.py 中，写对应的函数名称，并且记得导入一个 HttpResponse
- 其他简单视图， django.http 给我们提供了很多类和 HttpResponse类似的简单视图，你可以通过 <kbd>ctrl + 鼠标左键</kbd>点击在视图函数中的 http,(就在你导入的那一行命令中)，通常多数是 return 就能解决了，不过有一个例外就是 <strong>Http404</strong> 为 Exception 子类，需要 raise 使用, 并且你还需要再导入 HttpResponse 后面再加上 Http404, 整个句子应该是 from django.http import HttpResponse, Http404。然后可以去尝试写一个 引发404错误的页面，还是在 views.py 中写一个引发404的函数,且在主路由下写 url(r'^exception/$', tv.exception),
<pre>def exception(request):
        raise Http404 # 如果直接引发这句，后面的 return 语句不会执行
        return HttpResponse('正常的返回字符串内容')
</pre>
这样，当你打开网页后，会出现一个有调试信息的404错误，当你去settings 中设置 DEBUG = False 和 ALLOWED_HOST =【'#'】, 请注意，这里里面的 井号必须改为 星号，不知道为什么填入 星号 会出现斜体，当你设置了这两个地方后，再重新去 127.0.0.1:8000/exception 后，会发现是一个标准的 404 页面。

## 重定向 redirect
- 这里说的重定向, 其实很简单，一个概念，网页中我们会遇到这样的情况，这个做个假设，有一个网址叫做 baidu.com, 我们一直登录这个网址来查询一些事情，有一天， baidu.com 改了网址，改为 baibai.com, 并且该网址肯定不想失去我们的访问啊，毕竟访问这个网址，他人气高，所以他会叫工程师吧，把原来的网址重新定到另一个方向，就是 baibai.com。当我们访问 baidu.com 的时候，页面会自动显示为 baibai.com, 明白不！！！
很简单的，好好想想就明白，浏览网页的时候，就有这种情况发生的。
接着我们来尝试实现这个想法，继续 导入，在视图函数中 views.py, 导入 from django.http import HttpResponse,HttpResponseRedirect, 嗯，然后再写一个函数，当然了，你要是熟练了前面我们的内容，就是 写路由，写视图，暂且就两个步骤，很简单，哪个先写都可以，就是要对应起来。
<pre>
def baidu(request):
    return HttpResponseRedirect('/baibai') 
    # 也可以用一个 reverse ，后期建议使用 reverse
    
def baidu_2(request):
    return HttpResponseRedirect(reverse('bai'))
    
def baibai(request):
    return HttpResponse('你好，这里是重定向后的页面')
</pre>
然后再 urls.py 中写三个url， url(r'^baidu', tv.baidu), url(r'^baidu_2', tv.baidu_2), url(r'^baibai', tv.baibai, name='bai').
现在你再去网址中输入 主机:8000/baidu, 会跳转到 /baibai, 再重新用 主机:8000/baidu_2 试试，也是跳到 baibai,建议后期尽量使用reverse,反向解析。


---------------------
接着， request 中的 GET，和 POST，通常这两个用的最多，也是比较常见的，
例如 网页是  ....com/?key1=value1&key2=value2 , 这是网页中 get 的例子，问号表示后面的是键值参数。在 views 中写一个视图函数来试试看吧。
<pre>
def method_get(request):
    # result 为将要返回的网址中的参数的内容
    result = ""
    # 键值在 get 方法中
    for k, v in request.GET.items():
      result += k + '-->' + v
      result += ","
    return HttpResponse('The request of get method result is {0}'.format(result))
</pre>

再去 urls 中写路由， url(r'method_get', tv.method_get), 主机:8000/method_get/?name=SourOrange&subject=Python, 如果还有其他键值对，你可以继续写下去，然后回车可以看到结果。

'说完get属性，再来说说 post 属性，post 属性不会再网址中暴露键值信息，嗯，这个是最特别的。基本上是这么来的，你发一个请求过来，我给你一个页面，你提交了信息后，我再跳转到一个页面，这么说，基本上 post 就是4个步骤了。实现的具体方法分为以为：1.编写路由 url(r'get_2', tv.method_get2),2，编写视图函数，3，编写一个页面，内容要有客户的信息，所以有一个提交按钮，提交按钮跳到指定的页面，4.编写提交后的页面，由于是练习，提交后的页面我们先返回一条信息就好。url(r'post_1', tv.method_post) 。
<pre>
def method_get2(request):
    # 这里会返回一个页面，有提交按钮
    # 需要提醒一下，虽然是跳到某个页面，但是前提依旧需要再这个函数下返回一个页面
    # 而不是直接 平白无故地就转到哪个页面哦
    
    return render_to_response('for_post.html')
</pre>

虽然，我们写了一个 for_post.html，不过，我们在哪里写啊，所以你要现在项目下建立一个 templates 文件夹，该文件夹和 teacher 文件夹是处于平行关系的，然后再 templates 下面建立一个 for_post.html ，其中包括表单内容，另外 <form action='/post_1' method='post'> 中的 action 是对应的网址，表单中可以包括姓名密码爱好等等一些内容，因为是练习，所以你不需要写很多东西进去。你还需要去写一个 url(r'post_1', tv.method_post) ，编写 method_post 视图函数。
<pre>
def method_post(request):
    result = ""
    # 注意，k,  代表了 html中的 form 中 input 标签的 name 属性
    # 而 v, 则是 用户输入后的信息，比如用户姓名填入 小明，则v 就是 小明
    for k, v in request.POST.items():
        result += k + '-->' + v
        result += ' ,'
    return HttpResponse("Get value of post is {0}".format(result))
</pre>
到这里，就写完了post属性了，不过你现在去网页尝试的话，在提交表单后，会出现 csrf 的提示信息，总之就是无法正常跳转到 另外一个页面，所以你返回去 settings 文件中，有个叫做 MIDDLEWARE_CLASSES 中的组，也许是第三行，反正有写 csrf 的就把给注释掉先，接着回去继续测试，你会发现可以了。
  
。。实际上,render_to_response('xx.html') 可以换做 render(request, 'xx.html'),并且如果你在 html 里面设置了一个变量,比如，简单的一句问候，
<pre>
<h1>Hello my little {{ name }}</h1>
</pre>
嗯，很明显，这是一个变量，但是具体来说，其实是一个字典中的键。显然我们要实现的话，需要再 render函数中添加一个对应的字典，很简单。实现方法是
<pre>
def render_test(request):
  d = dict()
  d['name'] = 'lover'
  return render(request, 'xx.html', context=d)
</pre>
当然实现完这个函数后，记得去写对应的路由，然后再打开网址试试看就行了。
        
