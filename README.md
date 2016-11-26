# 优化OC代码编写
##命名规范
**文件命名**：项目名前缀+文件名+类型后缀。
例如：MFHomeView、MFHomeViewController、MFHomeModel  
 
**视图命名**：一般视图有几种，列表(List)、详情(Detail)、添加(Add)、编辑(Edit)、混合视图(视功能以及对应模块来定)。规范：Model+限定与修饰+ViewController
例如：ProductListViewController   

**常量命名**：
k+分类类型前缀(类名等等)+驼峰命名。 具体到类的常量要以相关的类名作为前缀
例如：k_Api_LoginUrl
例如：k_ZOCSignInViewController_FadeOutAnimationDuration   

**全局变量命名**：以_global开头。
例如：_globalUserName;   


**成员变量命名**：
在变量前面加上下划线_。
例如：UIButton *_btnCancel;   

**通知命名**：
前缀+相关的类名+Did(已经发生)|Will(将要发生)+动词(Change、Show、Hide等)+Notification
例如：UIKeyboardWillShowNotification
     UIKeyboardDidShowNotification
     UIKeyboardWillHideNotification
     UIKeyboardDidHideNotification   

**方法命名**：
**1.**+或- 要与返回类型间留一个空格 ，参数返回不要直接返回id，传递的参数要名义，例如传递的是Image对象，就写Image，不要写NsData，参数不要传递delegate。
**2.**方法名称要表达好要做的事情，这个方法要什么数据，这个方法做什么事情。
                   业务层：(find、edit、remove、add、[常用动词：do、go、wait等待、start开始、close关闭、open打开、show显示、hide隐藏、draw画])
                   数据层：(search、update、delete、insert)
                 例如：- (NSDictionary *)exifDataOfImage:(UIImage *)image atIndexPath:(NSIndexPath *)indexPath;

**分类命名**：
扩展类名+(前缀)+分类功能描述。分类里的方法名和属性名以类名为准，如有前缀就要在属性和方法前加上前缀。如果参数过多则每个参数单独一行。方法调用也是如此，一般保留原格式。
例如：NSString+URLEncoding、NSString+XXURLEncoding

例如二：

    @property (assign, nonatomic) CGFloat xx_offsetX;
    + (UIImage *)xx_arrowImage;
 例如：
 
    - (void)doSomethingWith:(GTMFoo*)theFoo rect:(NSRect)theRect  
    interval:(float)theInterval {  }  


方法调用示例：
例如：[myObject doFooWith:arg1 name:arg2 error:arg3];
亦或：

    [myObject doFooWith:arg1  (使用冒号对齐)
                   name:arg2  
                  error:arg3];  

**委托名**：
功能名+Delegate
例如：ReplyViewDelegate

**事件命名**：
使用事件通用名词，如Click、Load、Press
例如：- (void)btnAvatarClick;

**枚举命名**：
例用如下格式

    typedef NS_ENUM(NSInteger, Test1) {
        Test1A = 0,
        Test1B = 1,
        Test1C = 2,
        Test1D = 3
    };
**.h .m @intefrace命名：**

    分别列出属性，方法，并进行功能、控件、模块归类
    @interface DateilViewController : UIViewController
    {
        //变量
        NSString *_dataString;
    }
    //头部
    @property (weak, nonatomic) IBOutlet UILabel *customerNameLabel;//产妇姓名 
    @property (weak, nonatomic) IBOutlet UILabel *comeInTimeLabel;/**<入住日期 */
    
    //套餐信息
    @property (weak, nonatomic) IBOutlet UILabel *serviceTimeLabeL;/**<服务期限 */
    @property (weak, nonatomic) IBOutlet UILabel *packageCostLabel;/**<套餐金额 */
    
    //数据对象
    @property (nonatomic, strong) NSDictionary *supplyDateilDict;
    @property (nonatomic, strong) NSMutableArray *supplyArray;
    
    //方法
    - (void)handleData;
    - (void)createView;
    @end

**属性命名**：

    属性	             简写	             示例
    NSArray           Array	            userArray
    NSDictionary	  Dict	            userDict
    NSSet	          Set	            userSet
**控件命名：**
描述+后缀简写

    控件	             简写	             示例
    UIView	          View	            markView
    UIButton	      Button	        loginButton
    UILabel	          Label	            titleLabel
    UIScrollView      ScrollView       leftScrollView
    UITableView	      Tbv	           userTbv
    UICollectionView  collectionView	userCollectionView
    UIImageView	      Img	            avatarImg
    UIWindow	      Win	            sliderWin
    UIAlertView	      Alert             orderAlert
    UIActionSheet	  ActionSheet       userActionSheet
    UITextField	      Txtf	            userNameTxtf
    UITextView	     Txtv	            userNameTxtv
    UINavigationController nav          nav
    UINavigationBar	  navBar	        topNavBar
    UITabBarController	tabBar          tabBar
    UISwitch	       switch	        sexSwitch
    UISlider	      slider	        sliderProgress
    UIImagePickerController	imgPicker	imgPicker
    UIWebView	      webView	        webView
    UIActivityIndicatorView	Indicator	loadingIndicator
    UIProgressView	  progressView      progressView
    UISegmentedControl	segmentedControl	segmentedControl
**DataManager层命名规范：**
使用Find、Edit、Remove、Add描述操作内容。
示例：

    -(void)FindUserInfo:(void (^)(AADataResultModel *))complate;

**异常处理层：**code3自定义跳转业务(如登出、并清除相应数据)，code2参数错误，tips提示。other回到视图层，单独处理。

**单例替换**,单例存在的生命周期是整个应用的生命周期、如果不是整个应用生命周期的状态不要用单例保存 (例如：用户登录的信息，用户登录的信息的生命周期是直到用户退出，而不是一直跟随整个应用的生命周期)。替换方案->pincache（缓存库）。

**1.代码编写顺序：**先是**life cycle(程序生命周期)**，然后是**Delegate**（代理）方法实现，然后是**event response**(事件响应)，然后才是**getters and setters**(viewOrAttribute的getters和setters)。
示例：
    
    #pragma mark - liftCycle
    - (void)viewDidLoad {
        [super viewDidLoad];
    }
    
    - (void)viewWillAppear:(BOOL)animated{
        [super viewWillAppear:animated];
    }
    
    #pragma mark - delegate
    //代理委托代码 tableview,txextfield
    #pragma mark - UITableViewDelegate
    
    #pragma mark - UIScrollViewDelegate
    
    #pragma mark - UITTextViewDelegate
    
    #pragma mark - eventRespone（eg: UITableViewDelegate & UITableViewDataSource Support）
    //事件响应对应代码
    
    #pragma mark Notification
    
    #pragma mark - getters and setter（所有属性都使用getter/setter）
    //view加载等代码

2.**-viewDidLoad中，做为逻辑的入口**，代码会变少但是变清晰，代码如下：

    [self.view addSubview:self.topView];
    [self.view addSubview:self.bgView];
    [self.view addSubview:self.tabView];
**然后重写view的getter方法**，包括View和frame这些都可以使用({...})语法使代码结构化层次化：

    - (UIView *)topView{
        if (!_topView) {
            _topView = ({
                UIImageView *imgBg = [UIImageView new];
                imgBg.frame = CGRectMake(0, 0, 320, 49);
                imgBg;
            });
        }
        return _topView;
    }
一个方法中，代码多的情况下可用{}进行逻辑块划分。

3.**代理Delegate写到一块去**，写好代理块注释：
如UITableViewDelegate的方法要写上：#pragma mark - UITableViewDelegate。这样可以方便阅读和查看代理 实现

4.**event response(事件响应)专门开一个代码区域**
所有button、gestureRecognizer的响应事件都放在这个区域里面，不要到处乱放。

5.**关于private methods(私有方法)**，正常情况下ViewController里面不应该写
不是delegate方法的，不是event response方法的，不是life cycle方法的，就是private method了。对的，正常情况下ViewController里面一般是不会存在private methods的，这个private methods一般是用于日期换算、图片裁剪啥的这种小功能。这种小功能要么把它写成一个category，要么把他做成一个模块，哪怕这个模块只有一个函数也行。

ViewController基本上是大部分业务的载体，本身代码已经相当复杂，所以跟业务关联不大的东西能不放在ViewController里面就不要放。另外一点，这个private method的功能这时候只是你用得到，但是将来说不定别的地方也会用到，一开始就独立出来，有利于将来的代码复用。（引用之http://casatwy.com/iosying-yong-jia-gou-tan-viewceng-de-zu-zhi-he-diao-yong-fang-an.html）

6.**AOP划分服务逻辑**(对于像日志、异常系统、统计这种服务型代码，尽可能使用aop进行逻辑划分，避免过多耦合和干预ViewController的职责)

下面使用oc runtimer机制实现最常用的统计代码集成，以友盟统计为例，页面pv是衡量浏览量的主要指标，基本是必须集成的统计之一，页面pv由页面的进入和页面的结束组成，那么这就需要我们在viewController的生命周期中的viewWillAppear和viewWillDisappear里进行代码集成：

    //页面进入统计：
    - (void)viewWillAppear:(BOOL)animated
      {
            [super viewWillAppear:animated];
            [MobClick beginLogPageView:@"PageOne"];
      }
    页面退出统计：
    - (void)viewWillDisappear:(BOOL)animated 
      {
            [super viewWillDisappear:animated];
            [MobClick endLogPageView:@"PageOne"];
    }   

这种类型的代码是要在所有的ViewController里都要写的，那么我们每个ViewController都写一遍？要是业务改变更换统计集成代码不需要友盟了，哪么不就每个页面都需要重新替换，哪得要猴年马月，聪明的你说不定想到，这还不简单，使用继承这不就解决这个问题了么，所有ViewController都继承统一的父ViewController，嗯，这个是有点道理，但是这就要求我们创建项目的时候需要创建好唯一的父类ViewController，并且所有的ViewController都要继承于它，对于项目已经进行到中期了，项目没有唯一的父类ViewController该怎么办呢？写一个？再把所有的ViewController翻出来继承于父ViewController,想想都要加班的节奏，讨厌死啦。而且项目中并不是所有ViewController类都继承于UIViewController,有可能继承UITableViewController,UIConllectionViewContrtoller,对于这类继承了其它扩展类型的ViewController，我们又该怎么办，fack重写一下吧，OMG...,想想都应该叫老板，给我来碗“泪流满面”，说回重点，对于以上所说的问题，我们可以使用oc 的runtimer机制完美解决。

    oc runtimer可以参考：
    http://www.cocoachina.com/ios/20150120/10958.html 
    http://my.oschina.net/panyong/blog/298631 

简单多说一下，什么是runtimer机制，说白了就是运行时机制，它的作用是可以动态注入代码，动态创建类，创建属性等等。专业人士称它为黑魔法。下面就以runtimer机制修改上面的代码：

**1.**创建一个UIViewController的category，并引入

    #import <objc/runtime.h>

**2.**实现+(void)load方法，并在load方法实现方法注入，代码如下：

    + (void)load {
     static dispatch_once_t onceToken;  dispatch_once(&onceToken, ^{
         Class class = [self class]; 
         swizzleMethod(class, @selector(viewDidLoad), @selector(aop_viewDidLoad));
          swizzleMethod(class, @selector(viewDidAppear:), @selector(aop_viewDidAppear:));
          swizzleMethod(class, @selector(viewWillAppear:), @selector(aop_viewWillAppear:));
          swizzleMethod(class, @selector(viewWillDisappear:),@selector(aop_viewWillDisappear:));
         });
    }
    
    void swizzleMethod(Class class, SEL originalSelector, SEL swizzledSelector)   {
         Method originalMethod = class_getInstanceMethod(class, originalSelector);
         Method swizzledMethod = class_getInstanceMethod(class, swizzledSelector);
       BOOL didAddMethod =    class_addMethod(class,originalSelector,method_getImplementation(swizzledMethod),
       method_getTypeEncoding(swizzledMethod));if (didAddMethod) {
       class_replaceMethod(class,swizzledSelector,method_getImplementation(originalMethod),
       method_getTypeEncoding(originalMethod));
       } else {
           method_exchangeImplementations(originalMethod, swizzledMethod);
        }
    }
    
    - (void)aop_viewDidAppear:(BOOL)animated {
        [self aop_viewDidAppear:animated];
    }
    
    -(void)aop_viewWillAppear:(BOOL)animated {
        [self aop_viewWillAppear:animated];
        [MobClick beginLogPageView:NSStringFromClass([self class])];
    }
    
    -(void)aop_viewWillDisappear:(BOOL)animated {
        [self aop_viewWillDisappear:animated];
        [MobClick endLogPageView:NSStringFromClass([self class])];
    }
    
    - (void)aop_viewDidLoad {
       [self aop_viewDidLoad];
         if ([self isKindOfClass:[UINavigationController class]]) {}
    }
上面代码出现了一个陌生的单词swizzleMethod，swizzleMethod是利用 Runtime 特性把一个方法的实现与另一个方法的实现进行替换。
swizzleMethod是一个非常好用的特性，代码库，框架的封装常常可以看到它哦。
swizzleMethod是个好东西，但是使用上也要规范的整理在一起，swizzleMethod很容易造成调试上的困难。

    第三方对swizzleMethod的封装：
    Aspects:https://github.com/steipete/Aspects
        http://www.ios122.com/2015/08/aspects/
    
    AOP相应注入Deom:https://github.com/okcomp/AspectsDemo
    
    swizzleMethod参考：
    http://blog.csdn.net/yiyaaixuexi/article/details/9374411
    http://blog.csdn.net/mangosnow/article/details/34908365
    
    SEL(@selector)参考：
    http://blog.csdn.net/fengsh998/article/details/8612969

**7.Block代替delegate**,尽量使用block,对于有大量的delegate方法才考虑使用protocol实现.

1.Block语法总结及示例如下：

    //1.普通代码块方式block
    returnType (^blockName)(parameterTypes) = ^returnType(parameters) {
        // block code
    };
    使用未例：
    int (^abc)(int a) = ^int(int a){
        return a+1;
    };
    int aa = abc(2);
    NSLog(@"%d",aa);
    
    //2.属性方式block
    @property (nonatomic, copy) returnType (^blockName)(parameterTypes);
    使用示例：
    1.定义属性
    @property (nonatomic,copy) int (^testblock)(NSString *);
    2.设置使用属性
    [self setTestblock:^int(NSString *a) {
        return 0;
    }];

    //3.方法参数block
    - (void)someMethodThatTakesABlock:(returnType (^)(parameterTypes))blockName {
        // block code
    };
    使用示例1：
    1.无参数型定义及实现：
    - (void)testBlockFun:(void(^)())completion{
     NSLog(@"执行");
        if (completion) { 
           completion();
        }
    }
    2.无参数型block调用：
    [self testBlockFun:^{
        NSLog(@"回调结束");
    }];

    使用示例2：
    1.带参数型定义及实现：
    - (void)testBlockFun:(int (^)(int a,int b))complate{
        if (complate) {
            int c = complate(3,5);
            NSLog(@"c:%d",c);
        }
    }
    2.带参数型block调用：
    [self testBlockFun:^int(int a, int b) {
        return a+b;
    }];

    // 4.作为参数
    [someObject someMethodThatTakesABlock: ^returnType (parameters) {
        // block code
    }];
    使用示例：
    1.定义及实现
    - (void) testBlockFun:(void (^)(NSString *))complate{
        if (complate) {
            complate(@"success");
        }
    }
    2.调用
    [self testBlockFun:^(NSString *str) {
       NSLog(@"str:%@",str);
    }];
    // 5.使用 typedef 定义
    typedef returnType (^TypeName)(parameterTypes);
    TypeName blockName = ^(parameters) { };
    
    使用示例：
    typedef void (^blockTestName)(NSString *);
    
    调用：
    [self setName:^(NSString *a){
    }];
    
    2.Block修改值：使用__block可以在block内部修改外部变量的值。
    
     __block int someIncrementer = 0;
     [someObject someMethodThatTakesABlock:^{
           someIncrementer++;
      }];
    
    3.Block循环引用，block会持有对象，block的对象也有block，会造成block的循环引用，解决方法：
      __weak typeof(self) weakSelf = self;//@weakify(self); 
      [self someMethodThatTakesABlock:^{
           [weakSelf action]; 
       }];
       
    Block weakSelf宏：
    #define WS(weakSelf)  __weak __typeof(&*self)weakSelf = self;
       
    在block里添加如下代码，可以防止循环引，又避免block内部self会无效的问题。
    __strong __typeof(weakSelf)strongSelf = weakSelf;
    // weakify
    #define weakify(var) __weak __typeof(var) weak_##var = var;
    
    // strongify
    #define strongify(var) \
    _Pragma("clang diagnostic push") \
    _Pragma("clang diagnostic ignored \"-Wshadow\"") \
    __strong __typeof(var) var = weak_##var; \
    _Pragma("clang diagnostic pop")


**8.错误处理注意：**
如下处理会有问题：

    NSError *error;
    [self trySomethingWithError:&error];
    if (error) {
    }
    
    //在成功的情况下，有些Apple的APIs记录垃圾值(garbage values)到错误参数(如果non-NULL)，那么判断错误值会导致false负值和crash。
    应该如下：
    
    NSError *error;
    if (![self trySomethingWithError:&error]) {
        // Handle Error
    }

    
**9.枚举、通知统一管理**

**10.多个target管理项目版本（开发、正式）**

**11.单例：**

    + (AccountManager *)sharedManager  
    {  
       static AccountManager *instance = nil;  
       static dispatch_once_t predicate;  
       dispatch_once(&predicate, ^{  
              instance  = [[self alloc] init];   
       });  
       return instance;  
    }  
**12.打印运行方法所在的Vc及方法名**

    NSLog(@"%s",__func__);
**13.参考额外文章 ：**
http://www.jianshu.com/p/3beb21d5def2
http://www.jianshu.com/p/06bab2058c53
**请求缓存：**
http://www.jianshu.com/p/fb5aaeac06ef
**http状态码汇总：**
https://github.com/ChenYilong/iOSDevelopmentTips/blob/master/Tips/HTTP%E7%8A%B6%E6%80%81%E7%A0%81%E6%B1%87%E6%80%BB.md


**Parse源码浅析系列（一）---Parse的底层多线程处理思路：GCD高级用法**
https://github.com/ChenYilong/ParseSourceCodeStudy/blob/master/01_Parse%E7%9A%84%E5%A4%9A%E7%BA%BF%E7%A8%8B%E5%A4%84%E7%90%86%E6%80%9D%E8%B7%AF/Parse%E7%9A%84%E5%BA%95%E5%B1%82%E5%A4%9A%E7%BA%BF%E7%A8%8B%E5%A4%84%E7%90%86%E6%80%9D%E8%B7%AF.md

