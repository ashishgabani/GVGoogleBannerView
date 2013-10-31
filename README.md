GVGoogleBannerView
==================

Google-AdMob-Ads-SDK banners in interface builder with handy delegate callbacks.

Normally requesting a banner from Google's AdMob Ads SDK involves code like this:

```objective-c
- (void)viewDidLoad {
  [super viewDidLoad];

  // Create a banner of the standard size
  self.bannerView = [[DFPBannerView alloc] initWithAdSize:kGADAdSizeBanner];

  // Configure
  self.bannerView.adUnitID = MY_AD_UNIT_ID;
  self.bannerView.rootViewController = self;

  // Add to view
  [self.view addSubview:self.bannerView];

  // Load the ad, enable testing on simulator
  GADRequest *request = [GADRequest request];
  request.testDevices = @[GAD_SIMULATOR_ID];
  [self.bannerView loadRequest: request];
}
```

Using GVGoogleBannerView however, you simply drag a UIView into your interface, set its size to the required banner size, change its class to GVGoogleBannerView and set its `googleBannerViewDelegate` outlet to the view controller.

Your view controller must then implement the only required delegate method:

```objective-c
- (NSString *)googleBannerViewAdUnitID {
  return MY_AD_UNIT_ID;
}
```

GVGoogleBannerView also (optionally) adds a close button to the banner, makes it a lot easier to provide extra targeting parameters and has easy delegate callbacks for when banners are opened or closed. You can for example add a content inset to your tableview, scrollview or collectionview:

```objective-c
- (void)googleBannerViewOpened:(GVGoogleBannerView *)googleBannerView {
    self.collectionView.contentInset = UIEdgeInsetsMake(0, 0, googleBannerView.frame.size.height, 0);
    self.collectionView.scrollIndicatorInsets = UIEdgeInsetsMake(0, 0, googleBannerView.frame.size.height, 0);
}

- (void)googleBannerViewClosed:(GVGoogleBannerView *)googleBannerView {
    self.collectionView.contentInset = UIEdgeInsetsZero;
    self.collectionView.scrollIndicatorInsets = UIEdgeInsetsZero;
}
```