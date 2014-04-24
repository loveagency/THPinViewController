THPinViewController
===================

iOS 7 style PIN screen for iPhone and iPad that can be displayed modally whenever the user needs to authenticate, e.g. when accessing a specially protected part of your app.

Features
--------

* Has iPhone portrait and iPad portrait and landscape layouts
* Supports variable PIN lengths
* Background and tint colors as well as text and color of the prompt can be customized

Screenshots
-----------

<img src="THPinViewController_iphone_4inch.png" width="49%" />
<img src="THPinViewController_iphone_3-5inch.png" width="49%" />
<img src="THPinViewController_ipad.png" width="98%" />

Usage
-----

	THPinViewController *pinViewController = [[THPinViewController alloc] initWithDelegate:self];
    pinViewController.backgroundColor = [UIColor lightGrayColor];
    pinViewController.promptTitle = @"Enter PIN";
    pinViewController.promptColor = [UIColor whiteColor];
    pinViewController.view.tintColor = [UIColor whiteColor];
    [self presentViewController:pinViewController animated:YES completion:nil];
	
	// mandatory delegate methods
	
	- (NSUInteger)pinLengthForPinViewController:(THPinViewController *)pinViewController
	{
	    return 4;
	}

	- (BOOL)pinViewController:(THPinViewController *)pinViewController isPinValid:(NSString *)pin
	{
	    if ([pin isEqualToString:self.correctPin]) {
	        return YES;
	    } else {
	        self.remainingPinEntries--;
	        return NO;
	    }
	}

	- (BOOL)userCanRetryInPinViewController:(THPinViewController *)pinViewController
	{
	    return (self.remainingPinEntries > 0);
	}
	
	// optional delegate methods
	
	- (void)pinViewControllerIncorrectPinEntered:(THPinViewController *)pinViewController {}
	- (void)pinViewControllerWillDismissAfterPinEntryWasSuccessful:(THPinViewController *)pinViewController {}
	- (void)pinViewControllerDidDismissAfterPinEntryWasSuccessful:(THPinViewController *)pinViewController {}
	- (void)pinViewControllerWillDismissAfterPinEntryWasUnsuccessful:(THPinViewController *)pinViewController {}
	- (void)pinViewControllerDidDismissAfterPinEntryWasUnsuccessful:(THPinViewController *)pinViewController {}
	- (void)pinViewControllerWillDismissAfterPinEntryWasCancelled:(THPinViewController *)pinViewController {}
	- (void)pinViewControllerDidDismissAfterPinEntryWasCancelled:(THPinViewController *)pinViewController {}

See the example project for more details.

Installation
-------

###As a Git Submodule

	git submodule add git://github.com/antiraum/THPinViewController.git <local path>
	git submodule update

###Via Cocoapods

Add this line to your Podfile:

    pod 'THPinViewController', '~> 1.0.1'
	
Compatibility
-------

THPinViewController requires iOS 7.0 and above. 

THPinViewController uses ARC. If you are using THPinViewController in your non-ARC project, you need to set the `-fobjc-arc` compiler flag for the THPinViewController source files.

License
-------

Made available under the MIT License.

Collaboration
-------------

If you have any feature requests or bugfixes feel free to help out and send a pull request, or create a new issue.
