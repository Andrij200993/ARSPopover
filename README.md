# ARSPopover
Universal popover for iPhone and iPad that you can use in your projects. No custom drawing, no custom elements - everything is purely native.

|           iPhone             |           iPad           |
| ---------------------------- | ------------------------ |
| ![ARSPopover-iPhone][iPhone] | ![ARSPopover-iPad][iPad] |

[iPhone]: http://git.arsenkin.com/ARSPopover-iPhone.gif
[iPad]: http://git.arsenkin.com/ARSPopover-iPad.gif

## Installation

### CocoaPods
To install with [CocoaPods](http://cocoapods.org/), copy and paste this in your *Podfile* file:

    platform :ios, '8.0'
    pod 'ARSPopover', '~> 1.0'

### Non-CocoaPods way
You can always to do the old way - just drag the source files into your projects and you are good to go.

## Usage
Sample usage of the ARSPopover might look like this:

``` objective-c
- (IBAction)showPopoverWithWebView:(id)sender {
    ARSPopover *popoverController = [ARSPopover new];
    popoverController.sourceView = self.buttonWithWebView;
    popoverController.sourceRect = CGRectMake(CGRectGetMidX(self.buttonWithWebView.bounds), CGRectGetMaxY(self.buttonWithWebView.bounds), 0, 0);
    popoverController.contentSize = CGSizeMake(400, 600);
    popoverController.arrowDirection = UIPopoverArrowDirectionUp;

    [popoverController insertContentIntoPopover:^(ARSPopover *popover) {
        UIWebView *webView = [[UIWebView alloc] initWithFrame:popoverController.view.frame];
        webView.scalesPageToFit = YES;
        [webView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:@"http://google.com"]]];
        [popover.view addSubview:webView];
    }];

    [self presentViewController:popoverController animated:YES completion:nil];
}
```
### Required properties' configurations

In order to get a working popover, you need to specify next properties:

* `popoverController.sourceView` - The view containing the anchor rectangle for the popover.

``` objective-c
popoverController.sourceView = self.buttonWithWebView;
```

* `popoverController.sourceRect` - The rectangle in the specified view in which to anchor the popover.

``` objective-c
popoverController.sourceRect = CGRectMake(CGRectGetMidX(self.buttonWithWebView.bounds), CGRectGetMaxY(self.buttonWithWebView.bounds), 0, 0);
```

* `popoverController.contentSize` - The preferred size for the popover’s view.

``` objective-c
popoverController.contentSize = CGSizeMake(400, 600);
```

* And the last, most important thing - you have to call method `insertContentIntoPopover` and pass a block of code, which should add subviews to popover's view you wish to see.

``` objective-c
[popoverController insertContentIntoPopover:^(ARSPopover *popover) {
    UIWebView *webView = [[UIWebView alloc] initWithFrame:popoverController.view.frame];
    webView.scalesPageToFit = YES;
    [webView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:@"http://google.com"]]];
    [popover.view addSubview:webView];
}];
```

## License
ARSPopover is released under the [MIT license](http://opensource.org/licenses/MIT). See LICENSE for details.
