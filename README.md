# 一点编程理解记录

1.编程是思想，结合自己语言优势的思想，简单的转化成其他语言很简单，但是未必精髓。  
2.To C代码做错误处理的时候多输出默认值，让程序可用；To D代码要多报错，明确错误，及时stop！  
3.设计模式也是视情况而定的。  
4.js的数据类型内存模式：原始值和引用型。JS原始值是不可变的，使用上是正常的栈值，复制传递都是用的该值副本，比较也是比较的长的是否一样，其实是不同的值。引用值则是存在堆内存中，复制传递比较都是对其引用的。  
5.测试读写文件比读写数据库更快，与我想的正相反。  
6.文件编码越往底层越大，eg.同一份文件转码为base64要比binary要小。  
7.内存泄漏总结一句话就是：这份内存一直被占引用，并因为程序重复执行这种占用持续增加；程序不释放，垃圾回收也不能释放！  
8.框架~前端框架？什么叫做框架，而jQuery为什么不能叫做框架？我的理解，jQuery是JS它的运行环境是脱离不了JS运营环境的，而React等不一样，它该叫做运行时（RunTime到底是什么，暂时没有深刻理解）或者运行环境，比如V8把js转化为机器码，React是把reactjs转化为react码，再把这个转化为js码,js码跑在了js RunTime上。好像Node一样底层实现是C++，等于定义了一种JS与C++的逻辑关系。如果现在把jsDOM（与浏览器交互的JS简称），放在和C++同级别的地位，那么Reactjs就和js处于同一地位。所以Reactjs可不可以用其他不是js的语言实现哪？当然可以！eg.VUE的指令，完全不是js语言从此验证vue.js和react.js其实真是是像我们广义讲js的语言。其实它完全可以指定自己的语言逻辑！再深一点现在React这个运行时，相对与js运行环境和浏览器环境它有相当于语言，或者它可以直接等同于jQuery这样的语言就是一种封装jsDOM！不对，不是封装，没有封装这个React运行时是直接与浏览器沟通的，它就是jsDOM。优秀的是它在这个沟通上面设置了一层隔离，虚拟DOM,这个去识别Reactjs的语法，所以现在要想实现一个reactjs没有的语法，就像vue一样实现一些指令，其实就是在面向这个虚拟DOM编程，这个虚拟DOM可能翻译一句语法到jsDOM。那么指令是不是可以直接利用现用虚拟DOM的一个函数只是做一下封装！这个如果能找到这个函数应该很简单！更吊一点直接跳过这个虚拟DOM直接与jsDOM沟通，这个层面其实就是相当于jQuery的逻辑了，可能也不符合方法重用的理论，是在重复设计方法。这个可能就是React操作原生DOM留下的后门！所以这套东西的核心在哪？虚拟DOM怎么去执行jsDOM？怎么高效的去执行jsDOM？塑造一套指令系统直接去执行虚拟DOM的方法我感觉不会很难，继续修炼我相信到这个层次还是有可能的！  
9.React.js的更新与不更新？常规讲的React性能优势到底是什么？在我的理解里就是使用者要区分你写的JSX不是真实DOM,也就说你在这个组件里放一个log，每次外部组件渲染内部组件每次就会log出一些东西，但是这些变化是在React优化范围内的，它是在缓存中的，并不会更新真实DOM,怎么优化利用这个缓存的东西哪？就是生命周期shouldComponentUpdata,PureComponent,函数式组件做的。 https://juejin.im/post/5a12603f6fb9a0451c39ff9c 同时附录一个字节跳动工程师的掘金文章讲的东西像React的issue被打回的文章！恐怕没有理解React设计原理！当然并不是讲就可以肆无忌惮的乱干，网络请求，Redux的函数编程式的输出值是真实存在的！（这个还是不完全具体正确的，这个利用过程是更细度的，如果不是shouldComponentUpdata,PureComponent,函数式，还是会走协调的对比差异！总之意识中要有JSX或者说React组件不是真实DOM,你看见的打印不要想着这个DOM重新走了一边浏览器渲染过程）  
10.完全的实战经验一条，接住google开发者工具处理bad外部UI框架H-ui,这个UI多烂？它用到很多的js库然后自己封装函数调用库接口，把库的参数给干掉，只留下用的到的参数！这时候你发现翻库文档也不是，翻它的文档也没有！所有文件还封装到一个入口源文件也找不到？怎么办？！google开发者工具，找到一个整个框架的全局变量打印，找到这个外层方法，点开[[FunctionLocation]]是源文件！[[Scopes]]直接把这个文件转化成Object然后你就可以继续下翻知道找到源文件    
11.TypeScript:类型化js，省去了动态语言编译时的处处判断，却不能省去动态性的判断，同时也限制了js的灵活性。
12.关于web图片加载时间问题，看了谷歌图片和百度图片，真的没有特别hack的方法，就是一点一点下载，在程序没有问题就是堆服务器配置，谷歌域外明显比百度图片慢很多，你说这是技术问题吗？不是，这两者的区别就是网速带宽！所以对图片优化还是硬件因素起至关重要的因素。再然后就是想方法迂回优化了，谷歌图片一个极小的缩略图在初次加载页面时候加载，点击开来后台算法根据质量参数输出压缩图片（这算一个比较hack的地方，压缩出肉眼不易看出区别的小图片）。所以基本大部分时间我们看到的都是压缩图只是肉眼不易察觉。再然后用户下载！确实下载的原图至少是能请求到最高质量的图片！（百度这个地方看到的和下载的是一样大小的图片）  
13.并发顺序显示:实现并发请求，在能确认请求完成的之后(then or await后)，一个执行显示的函数按编号对应丢进发布数组中，这个发布器的执行函数，死循环以第一个值判断跳出条件，有值unshift取出执行。  
14.个人感受箭头函数让JavaScript更混乱更不宜于新手了   
15.js、node做网络应用绝对是绰绰有余的，但是感觉还是只能停留在应用层面的语言，并不能完全解放生产力，不能完全体现编程的终极思想，所以未来准备学一门真正的解放生产力的语言，把编程融入生活解决一些实际的问题，而不是只是做产品。初步选择Golang，梯子已经切到go版本，利用脚本实现开机自启、config配置。非常优秀，这才是编程，解决问题！  
16.lerna是什么？做了什么？在github中托管的很多大开源项目中你会发现，这些项目不像我们个人项目一个人下项目哪一个。那种是以组织命名，细看源码该项目下很多包并且这些包很多被引用在项目中。我想这就lerna，把项目的依赖工具集都抽在一个node_modules中统一管理，依赖关系清晰，文件结构、路径也能使用相对于node_modules来的绝对路径，因此不会因为拆包分包造成混乱。那么怎么做到这些哪？lerna指定的一个packages的文件夹，把项目分成两部分，一部分在根目录管理的，一部分在packages中分目录中管理的。根目录就是正常的，分目录如果也正常安装依赖也就是每个packages的分目录一个依赖，到这里就该lerna做的事了，遍历packages分目录的package.json抽出依赖关系，对比相同的包是否有不同版本（可以给出报告，根据配置默认安装高低版本），在根目录一个执行npm install，把packages的子目录作为npm包放到node_modules。所以门槛在哪?就是要学习学node命令行开发   
17.动态加载，需要时加载，加载之后通知，去对应更新。关键点：需要时，加载后通知。更新放在React里更新是很简单的事，放在正常的程序中应该是函数形式。以怎样的机制判断需要？加载后通知接回调或者订阅？这里就有一个事，一处进异步是不是带动处处都进异步。  
18.单设备登录与单点登录摸索，单设备：主要是userID与token的关系，同一用户生成每次登录给不同的token并更新userID与token的键值对；所有请求携带并对比token。单点：集中生成token，每个服务的验证不自己验证对比，去找中央节点既定逻辑验证，这个逻辑能加入userID与token的对应关系，登出置空这个关系登出就ok了。  
19.webpack插件开发，webpack可以理解为一个串行流水线，插件开发就是利用整个串行过程中不断给出的广播事件函数做出处理。这个过程会暴露出一些关键的对象或者配置。所以有个取巧的办法就是利用webpack现有的处理机制，我们把自己插件需要做的与webpack存在相同的任务交给它处理，也就是只是合理的时间节点把配置给更改-加入或者删除等。
20.Vue与React的区别，Vue像是一个写好的虚拟DOM的方案，能替用户准备好的标准就准备好；React更像是一个平台，基于它你可以做很多，小到高阶组件（这并不是react中的，很多高阶技术手段都是基于js思想形成的解决方案），大到做一个runtime。所以说哪个更简单可能要看个人喜欢哪种思考方式。  
21.学习antDesign源码的体会，对JavaScript的关注点一直在语言本身，忽略了赋能Js部分（这也是我喜欢写React的原因）。再加之有React、Vue这种虚拟DOM框架的封装更是偏离到了上层抽象部分，下一步要集中提升这部分能力，去学习React的封装抽象。  
22.umd模式打包结果，自执行函数判断是否由define.amd、exports，或者自定义变量作为exports传递给实际函数即正式代码包裹函数。  
