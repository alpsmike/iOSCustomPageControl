# iOSCustomPageControl
Android style page control

![      ](\pageControl.gif "")       

---
---

### Features

* Swipable tab bar
* Clickable tab to move to specific page
* Current page indicator with fade effect on non current title
* Easy to modify code
* Lazy loading for smoother performance ( Provide view controller instances only when moved to that page )
* Easy to setup color theme
* Many customisation parameters

---
---

### Customisation parameters

```obj-c
//Initial visible page
@property(readwrite) int            iFirstVisiblePageNumber;

//Color theme
@property(readwrite) UIColor        *colorTitleBarBackground;
@property(readwrite) UIColor        *colorTabText;
@property(readwrite) UIColor        *colorPageIndicator;
@property(readwrite) UIColor        *colorPageOverscrollBackground;

//UI Size related customisation
@property(readwrite) int            iTitleViewHeight;
@property(readwrite) int            iPageIndicatorHeight;
@property(readwrite) UIFont         *fontTitleTabText;

//Bounce effect on/off
@property(readwrite) BOOL           bEnablePagesEndBounceEffect;
@property(readwrite) BOOL           bEnableTitlesEndBounceEffect;

//Title tabview show indicator when more tabs available to left/right
@property(readwrite) BOOL           bShowMoreTabAvailableIndicator;

```

<em>This UI control can be used on all iPhones, iPods & iPads running iOS 6.0 and above.</em>

---
---

### Adding to your project


* Add Follwing 5 control files to your project from ADPageControl directory located under "ControlFiles/" or from demo project

```
'ADPageControl.h'
'ADPageControl.m'
'ADPageModel.h'
'ADPageModel.h'
'ADPageControl.xib'
```

---
---

### How to use ?


```obj-c

//1. IMPORT
  "#import "ADPageControl.h"
```

```obj-c
//2. DECLARE
  ADPageControl *_pageControl; //Declare
```  

```obj-c  
//3. SETUP PAGE MODEL USING CLASS "ADPageModel"

    //page 0
    ADPageModel *pageModel0 = [[ADPageModel alloc] init];
    UIViewController *page0 = [UIViewController new];
    page0.view.backgroundColor = [UIColor colorWithRed:1 green:204.0/255 blue:204.0/255.0 alpha:1.0];
    pageModel0.strPageTitle = @"Reeed";
    pageModel0.iPageNumber = 0;
    pageModel0.viewController = page0;//You can provide view controller in prior OR use flag "bShouldLazyLoad" to load only when required
    
    //page 1
    ADPageModel *pageModel1 = [[ADPageModel alloc] init];
    pageModel1.strPageTitle = @"Greeeeeeeen";
    pageModel1.iPageNumber = 1;
    pageModel1.bShouldLazyLoad = YES;
    
    //page 2
    ADPageModel *pageModel2 = [[ADPageModel alloc] init];
    pageModel2.strPageTitle = @"Blueeee";
    pageModel2.iPageNumber = 2;
    pageModel2.bShouldLazyLoad = YES;
    
    //page 3
    ADPageModel *pageModel3 = [[ADPageModel alloc] init];
    pageModel3.strPageTitle = @"Yeeellow";
    pageModel3.iPageNumber = 3;
    pageModel3.bShouldLazyLoad = YES;
```

```obj-c
//4. INITIALIZE PAGE CONTROL

    _pageControl = [[ADPageControl alloc] init];
    _pageControl.delegateADPageControl = self;
    _pageControl.arrPageModel = [[NSMutableArray alloc] initWithObjects:pageModel0,pageModel1,pageModel2,pageModel3, nil];
```

```obj-c
//5. OPTIONAL CUSTOMISATION PARAMETERS SETUP

    _pageControl.iFirstVisiblePageNumber = 1;
    _pageControl.iTitileViewHeight = 40;
    _pageControl.iPageIndicatorHeight = 4;
    _pageControl.fontTitleTabText =  [UIFont fontWithName:@"Helvetica" size:16];
    
    _pageControl.bEnablePagesEndBounceEffect = NO;
    _pageControl.bEnableTitlesEndBounceEffect = NO;
    
    _pageControl.colorTabText = [UIColor whiteColor];
    _pageControl.colorTitleBarBackground = [UIColor purpleColor];
    _pageControl.colorPageIndicator = [UIColor whiteColor];
    _pageControl.colorPageOverscrollBackground = [UIColor darkGrayColor];
	
    _pageControl.bShowMoreTabAvailableIndicator = NO;
	
```

```obj-c
//6. ADD AS SUBVIEW
    _pageControl.view.frame = CGRectMake(0, 20, self.view.bounds.size.width, self.view.bounds.size.height - 20);
    [self.view addSubview:_pageControl.view];
```

```obj-c
//7. CONFORM TO DELEGATE 

//7.A : Conform <ADPageControlDelegate>

//7.B : HANDLE LAZY LOADING BY PROVIDING VIEW CONTROLLERS (Optional : Applicable only if you want to lazy load view controllers)


-(UIViewController *)adPageControlGetViewControllerForPageModel:(ADPageModel *) pageModel
{
    NSLog(@"ADPageControl :: Lazy load asking for page %d",pageModel.iPageNumber);

    if(pageModel.iPageNumber == 1)
    {
        UIViewController *page1 = [UIViewController new];
        page1.view.backgroundColor = [UIColor colorWithRed:204.0/255 green:1 blue:204.0/255 alpha:1.0];//Light Green

        return page1;
    }
    else if(pageModel.iPageNumber == 2)
    {
        UIViewController *page2 = [UIViewController new];
        page2.view.backgroundColor = [UIColor colorWithRed:204.0/255 green:204.0/255 blue:1 alpha:1.0];//Light Blue

        return page2;
    }
    else if(pageModel.iPageNumber == 3)
    {
        UIViewController *page3 = [UIViewController new];
        page3.view.backgroundColor = [UIColor colorWithRed:1 green:1 blue:204.0/255 alpha:1.0];//Light Yellow

        return page3;
    }

    return nil;
}

//7.C : Get index of currenty visible page (Optional)

-(void)adPageControlCurrentVisiblePageIndex:(int) iCurrentVisiblePage
{
    NSLog(@"ADPageControl :: Current visible page index : %d",iCurrentVisiblePage);
}


```


---
---

### Requirements

* ADPageControl works on iOS 6.0 & above versions and is compatible with ARC projects. 
* There is no need of other frameworks/libraries.

---
---

### Other details

* XCode : Developed using 6.1
* Base sdk used while development : 8.1
* Compatible devices : iPhone, iPad, iPod

---
---

### TODO

* Component polishing
* More generalizations

---
---
## License

iOSCustomPageControl is available under the MIT license. See the LICENSE file for more info.
