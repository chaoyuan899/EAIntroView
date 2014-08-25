EAIntroView
===========

introduce page
####Use
、、、
#import "IntroductionViewController.h"
#import "EAIntroPage.h"
#import "EAIntroView.h"
#import "WelcomeViewController.h"
#import "LoginViewController.h"
#import "GuideViewController.h"
@interface IntroductionViewController ()<EAIntroDelegate>

@end

@implementation IntroductionViewController

- (id)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil
{
    self = [super initWithNibName:nibNameOrNil bundle:nibBundleOrNil];
    if (self) {
        // Custom initialization
    }
    return self;
}

- (void)viewDidLoad
{
    [super viewDidLoad];
     [self showIntro];
    // Do any additional setup after loading the view from its nib.
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}
-(void) showIntro{
    NSInteger version = [[NSUserDefaults standardUserDefaults] integerForKey:@"INTRO_PAGE_VERSION"];
    
    if (version >= INTRO_PAGE_VERSION) {
        GuideViewController *controller = [[GuideViewController alloc]init];
        UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController:controller];
        self.view.window.rootViewController = nav;
        return;
    } else {
        [[NSUserDefaults standardUserDefaults] setObject:@(INTRO_PAGE_VERSION) forKey:@"INTRO_PAGE_VERSION"];
        [[NSUserDefaults standardUserDefaults] synchronize];
    }
    
    
    EAIntroPage *page1 = [EAIntroPage page];
    if (isIPhone5) {
        page1.bgImage = [UIImage imageNamed:@"image-guide_01_i5.png"];
    } else {
        page1.bgImage = [UIImage imageNamed:@"image-guide_01.png"];
    }
    page1.showTitleView = NO;
    
    EAIntroPage *page2 = [EAIntroPage page];
    if (isIPhone5) {
        page2.bgImage = [UIImage imageNamed:@"image-guide_02_i5.png"];
    } else {
        page2.bgImage = [UIImage imageNamed:@"image-guide_02.png"];
    }
    page2.showTitleView = NO;
    
    
    EAIntroPage *page3 = [EAIntroPage page];
    if (isIPhone5) {
        page3.bgImage = [UIImage imageNamed:@"image-guide_03_i5.png"];
    } else {
        page3.bgImage = [UIImage imageNamed:@"image-guide_03.png"];
    }
    page3.showTitleView = NO;
    
    
    EAIntroPage *page4 = [EAIntroPage page];
    if (isIPhone5) {
        page4.bgImage = [UIImage imageNamed:@"image-guide_04_i5.png"];
    } else {
        page4.bgImage = [UIImage imageNamed:@"image-guide_04.png"];
    }
    page4.showTitleView = NO;
    EAIntroView *intro;
    if (isIPhone5) {
        intro = [[EAIntroView alloc] initWithFrame:self.view.bounds];
    }else{
        intro = [[EAIntroView alloc] initWithFrame:CGRectMake(0, 0, 320, 480)];
    }
      intro.pages = @[page1,page2,page3,page4];
    //    intro.showSkipButtonOnlyOnLastPage = YES;
    intro.skipButton.hidden = YES;
    intro.backgroundColor = [UIColor whiteColor];
    intro.delegate = self;
    intro.pageControl.pageIndicatorTintColor = [UIColor colorWithHex:0xe7e7e7];
    intro.pageControl.currentPageIndicatorTintColor = [UIColor colorWithHex:0xec5464];
    [intro showInView:self.view animateDuration:0.3];
}

-(void) introDidFinish:(EAIntroView *)introView{
    
    GuideViewController *controller = [GuideViewController new];
    UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController:controller];
    self.view.window.rootViewController = nav;
    return;

}
@end
、、、 
####效果图
![pic.gif](/Users/z/Desktop)
