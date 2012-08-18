#PullToRefreshView

PullToRefreshView is a pull-to-refresh implementation that's very easy to implement.

This fork uses only an image (no "pull/release to refresh", or "last updated" text), and centers the image horizontally in the pull-to-refresh area.

##Usage

1. Add the four files (`PullToRefreshView.{h,m}`, `arrow.png` and `arrow@2x.png`) to your project.

2. Add the Quartz framework to your project if you haven't done so yet.

3. `#import "PullToRefreshView.h"`

4. Add an ivar: `PullToRefreshView *pull; // or whatever you want to name it`.

5. In loadView or viewDidLoad, add this (and be sure to release in dealloc/viewDidUnload, etc):

		pull = [[PullToRefreshView alloc] initWithScrollView:<your scroll view here>];
		[pull setDelegate:self];
		[<your scroll view here> addSubview:pull];

6. In `viewDidUnload`, add calls to: `[pull containingViewDidUnload];` to unwind the view hierarchy.

7. Implement two delegate methods:

		// called when the user pulls-to-refresh
		- (void)pullToRefreshViewShouldRefresh:(PullToRefreshView *)view;
		// called when the date shown needs to be updated, optional
		- (NSDate *)pullToRefreshViewLastUpdated:(PullToRefreshView *)view;
	
8. Call `-finishedLoading` on the `PullToRefreshView` when you're finished loading (or get an error, etc).

That's it! No need to forward on `UIScrollView` delegate methods or anything silly like that.
 