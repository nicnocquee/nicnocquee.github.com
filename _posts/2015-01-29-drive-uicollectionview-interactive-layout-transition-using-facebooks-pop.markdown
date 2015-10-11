---
layout: post
title: "Drive UICollectionView interactive layout transition using Facebook's Pop"
date: 2015-01-29 11:30:53 +0900
comments: false
categories: [ios]
---

UICollectionView has a method to change layout easily: `setCollectionViewLayout:animated:completion:`. And according to documentation, if you implement the delegate's `collectionView:transitionLayoutForOldLayout:newLayout:` you can customize the behaviour or the cells and decoration views during transition.

<!-- more -->

> Implement this method if you want to return a custom UICollectionViewTransitionLayout object for use during the transition. A transition layout object lets you customize the behavior of cells and decoration views when transitioning from one layout to the next. Normally, transitioning between layouts causes items to animate directly from their current locations to their new locations. With a transition layout object, you can have objects follow a non linear path, use a different timing algorithm, or move according to incoming touch events.

> If your delegate does not implement this method, the collection view creates a standard UICollectionViewTransitionLayout object and uses that object to manage the transition.

But strangely, that delegate's method is not called when we change layout using `setCollectionViewLayout`. Somebody in [stackoverflow](http://stackoverflow.com/a/23009119/401544) provided a workaround by calling collection view's `startInteractiveTransitionToCollectionViewLayout:` method instead.

```objc
[self.collectionView startInteractiveTransitionToCollectionViewLayout:self.finalLayout completion:nil];
[self.collectionView finishInteractiveTransition];
```

The problem is we cannot control the speed of the animation. What I wanted is to "animate" the `UICollectionViewTransitionLayout`'s `transitionProgress` property.

```objc
[UIView animateWithDuration:0.3 delay:0 usingSpringWithDamping:1 initialSpringVelocity:1 options:UIViewAnimationOptionCurveEaseInOut animations:^{
    transition.transitionProgress = 1;
} completion:^(BOOL finished) {}];    
```

But since transitionProgress is not animatable, this doesn't work. This is where [Facebook's Pop](https://github.com/facebook/pop) comes to rescue. Using Pop, we can animate custom properties.

```objc
// CustomTransitionLayout is subclass of UICollectionViewTransitionLayout
CustomTransitionLayout *transition = (CustomTransitionLayout *)[self.collectionView startInteractiveTransitionToCollectionViewLayout:self.finalLayout completion:nil];
	
POPSpringAnimation *springAnimation = [POPSpringAnimation animation];
POPAnimatableProperty *property = [POPAnimatableProperty propertyWithName:@"com.photos.transition" initializer:^(POPMutableAnimatableProperty *prop) {
   prop.readBlock = ^(id obj, CGFloat values[]) {
       values[0] = [obj transitionProgress];
   };
   prop.writeBlock = ^(id obj, const CGFloat values[]) {
       [obj setTransitionProgress:values[0]];
   };
   prop.threshold = 0.01;
}];
springAnimation.springBounciness = 8;
springAnimation.property = property;
springAnimation.fromValue = @(progress);
springAnimation.toValue = @(1.0);
springAnimation.completionBlock = ^(POPAnimation *anim, BOOL finished){
   if (finished) {
       [transition setTransitionProgress:1];
       [self.collectionView finishInteractiveTransition];
   }
};
[transition pop_addAnimation:springAnimation forKey:NSStringFromSelector(@selector(transitionProgress))];
```
    
This way, the value of `transitionProgress` will gradually change from 0 to 1. If you implement UICollectionViewTransitionLayout's `layoutAttributesForElementsInRect:` method and set the attributes of each cell based on the value of `transitionProgress`, you can create a custom layout animation transition.