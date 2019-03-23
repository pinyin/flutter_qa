# 一个关于Flutter入门的非官方Q&A

> 本文内容可能存在偏见、疏漏或错误，欢迎[贡献您的问题及答案](https://github.com/pinyin/flutter_qa)。
> 建议参阅[官方FAQ](https://flutter.dev/docs/resources/faq)以获得更多信息。

**Q: Flutter能解决什么样的问题？**

Flutter允许你用同一个代码库同时编写iOS和Android上的原生应用。

在今年的Google I/O上，Flutter可能会推出[将同一代码库扩展到Web上](https://events.google.com/io/schedule/)的方案。

相比传统前端项目，在Web上运行的Flutter应用[可以获得更好的表现力](https://www.youtube.com/watch?v=5IrPi2Eo-xM&feature=youtu.be)。

**Q: Flutter能运行在哪些平台上？**

目前官方支持的平台包括iOS和Android，并且即将发布对Web平台的官方支持。

此外也存在把Flutter运行在[桌面平台](https://github.com/google/flutter-desktop-embedding)上的实验性项目。

也有开发者成功把Flutter运行在树莓派上。

**Q: Flutter与其他跨平台开发方案有什么区别？**

按照官方的说法，Flutter允许你控制屏幕上的每一个像素。

因此总体来说，Flutter可以赋予开发者更强的表现力。

与一些使用原生组件的方案（例如React Native）相比，Flutter并不使用原生组件，从而隔离了不同平台上原生组件API的区别。理想情况下，Flutter项目的代码可以不必修改而直接编译到不同平台上。

与直接使用Web技术的方案（例如PWA和嵌入web view）相比，Flutter项目可以被编译到平台的原生代码，因此可以很容易地获得更高的性能和更自由的视觉效果。

与其他一些完全控制显示的方案（例如Unity3D）相比，Flutter专注于UI实现，因此学习成本更低。

**Q: 从整个系统的角度，Flutter为我做了哪些事？**

Flutter提供了一个对渲染层的统一抽象。

![https://github.com/flutter/flutter/wiki/The-Engine-architecture](https://raw.githubusercontent.com/flutter/engine/master/docs/flutter_overview.svg?sanitize=true)

从这个角度上看，Flutter在功能上比起大部分UI框架更接近于Unity3D这类游戏框架，同时又保持了UI框架较低的学习成本。

同时，受益于Dart语言，Flutter框架有极高的开放性。开发者甚至可以在应用运行时修改框架本身（上图中绿色的部分），然后在几秒内看到自己修改的影响。这给用户定制自己的Flutter发行版提供了方便。

**Q: Flutter包括哪些基本概念？**

较为基础的概念包括Widget，Element和Render Object。

开发者只要[会使用Widget就可以完成一个应用](https://flutter.dev/docs/development/ui/layout/tutorial)。

**Q: Flutter的基本概念之间是怎样互动的？**

开发者通过创建和设置Render Object告诉Flutter自己希望在屏幕上渲染哪些像素，通过创建Widget告诉Flutter自己希望界面上存在哪些Render Object。Flutter用Element记录Widget和Render Object之间的关系。

由于可以通过Widget创建和设置Render Object，在大部分情形下，开发者可以通过Widget实现所有需求，不需要直接使用Render Object。但是，了解Render Object的存在有利于开发者理解错误信息。

由于Render Object负责渲染，所以Render Object之间需要进行交互以决定不同Render Object所占据的视图尺寸。不同类型的Render Object中可能有不同的布局算法，因此Render Object在与另一个Render Object交互时需要掌握对方类型的知识，并提供对方所需要的数据类型。如果Render Object不了解自己将要交互的Render Object的类型，应用就会出错。这部分错误目前无法被Dart的类型检查捕获，只能从文档中了解并在运行时发现。如果发现Render Object丢出错误，可能是使用了布局算法不兼容的Widget。

Widget是不可变的。为了通过不可变的Widget操作可变的Render Object，Flutter内部使用Element记录Render Object的状态信息。通过不断创建存有不同数据的Widget，用户可以向Flutter要求自己所需要的界面，也就是声明式的UI编程，类似XML或者HTML。

**Q: 我来自React社区，怎样把我的知识复用到Flutter上？**

很多Flutter应用中的概念可以在React中找到对应的设计。

- Widget：对应React.ReactElement。
- State：对应React.Component。
- Render Object：对应HTML或者CSS。

State是有状态Widget中保存状态的部分，参见[StatefulWidget](https://docs.flutter.io/flutter/widgets/StatefulWidget-class.html)。

**Q: Widget是不可变的，为什么会出现有状态组件（StatefulWidget）？**

StatefulWidget里面包含一个创建State的工厂方法，工厂方法仍然不可变，而方法返回的State是可变的。

**Q: 运行在Web平台上的Flutter，会比原生Web应用（React/Angular/Vue..）更慢吗？**

Web平台上的Flutter还没有发布，只是透露了一些[技术信息](https://medium.com/flutter-io/hummingbird-building-flutter-for-the-web-e687c2a023a8)。从已知的信息来看，Web平台上的Flutter可能会比原生Web应用更流畅。
Flutter的一些开发者来自于Chromium项目，因此一些影响Web性能的设计（例如复杂的布局算法）[在Flutter中被避免了](https://flutter.dev/docs/resources/inside-flutter)。

**Q: Flutter中怎样实现动画？**

如上所述，Flutter的布局效率非常高，因此可以每帧进行一次布局来实现动画。

与Web及其他很多平台上的transform类似，Flutter也支持在完成布局的组件像素的坐标上应用线性变换达到不同的渲染效果。因为不需要调用布局算法，这样实现动画往往可以获得更高的性能。

**Q: 听说Flutter的最初发布是在14年，现在只是改了个名字？**

Flutter公开发布于2017年，之前只有原型存在。作为对照，React的原型在11年出现，13年才开源。
通过原型判断软件项目的前途，意义不大。

**Q: 为了跟踪Flutter的新闻，我应该关注哪些地方？**

Flutter的Reddit https://www.reddit.com/r/FlutterDev/
官方YouTube频道 https://www.youtube.com/channel/UCwXdFgeE9KYzlDdR7TG9cMw
各种Awesome Flutter收集者 https://www.google.com/search?q=awesome+flutter
Medium上的收集 https://medium.com/flutter-community
当然，还是要推荐一下本文所在的专栏 https://zhuanlan.zhihu.com/unifrontend
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMyMTY1MTkyXX0=
-->