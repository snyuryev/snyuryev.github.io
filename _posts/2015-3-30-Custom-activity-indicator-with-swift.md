---
layout: post
title: Custom activity indicator with swift
---

Custom Activity Indicator View an element that provides user feedback on the progress of a task or process with an unknown duration. As long as the task or process continues, the activity indicator spins. A user does not interact with an activity indicator. It is very similar with UIActivityIndicatorView but uses custom image. Custom Activity Indicator View is subclass of UIView.

You can download [test project] (https://github.com/snyuryev/Custom-Activity-Indicator-View) with implemented custom activity indicator from my [Github repository] (https://github.com/snyuryev/Custom-Activity-Indicator-View) or go forward and implement it by yourself. Also in test project you may find template icons for custom activity indicator.

Open XCode and create new project. Choose swift for your project language. Then create new file and call it - CustomActivityIndicatorView.swift. Here is full listing for custom activity indicator:

```
import UIKit
import QuartzCore

class CustomActivityIndicatorView: UIView {
    
    // MARK - Variables
    
    lazy private var animationLayer : CALayer = {
        return CALayer()
    }()
    
    var isAnimating : Bool = false
    var hidesWhenStopped : Bool = true
    
    // MARK - Init
    
    init(image : UIImage) {
        let frame : CGRect = CGRectMake(0.0, 0.0, image.size.width, image.size.height)

        super.init(frame: frame)

        animationLayer.frame = frame
        animationLayer.contents = image.CGImage
        animationLayer.masksToBounds = true

        self.layer.addSublayer(animationLayer)
        
        addRotation(forLayer: animationLayer)
        pause(layer: animationLayer)
        self.hidden = true
    }

    required init(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    // MARK - Func
    
    func addRotation(forLayer layer : CALayer) {
        let rotation : CABasicAnimation = CABasicAnimation(keyPath:"transform.rotation.z")
        
        rotation.duration = 1.0
        rotation.removedOnCompletion = false
        rotation.repeatCount = HUGE
        rotation.fillMode = kCAFillModeForwards
        rotation.fromValue = NSNumber(float: 0.0)
        rotation.toValue = NSNumber(float: 3.14 * 2.0)
        
        layer.addAnimation(rotation, forKey: "rotate")
    }

    func pause(#layer : CALayer) {
        let pausedTime = layer.convertTime(CACurrentMediaTime(), fromLayer: nil)
        
        layer.speed = 0.0
        layer.timeOffset = pausedTime
        
        isAnimating = false
    }

    func resume(#layer : CALayer) {
        let pausedTime : CFTimeInterval = layer.timeOffset
        
        layer.speed = 1.0
        layer.timeOffset = 0.0
        layer.beginTime = 0.0
        
        let timeSincePause = layer.convertTime(CACurrentMediaTime(), fromLayer: nil) - pausedTime
        layer.beginTime = timeSincePause
        
        isAnimating = true
    }

    func startAnimating () {
        
        if isAnimating {
            return
        }
        
        if hidesWhenStopped {
            self.hidden = false
        }
        resume(layer: animationLayer)
    }

    func stopAnimating () {
        if hidesWhenStopped {
            self.hidden = true
        }
        pause(layer: animationLayer)
    }
}
```

Do not forget to add some image which should be animated in custom activity indicator view. Next, go to your view controller. Custom activity indicator could be simple declared this way in your class:

```
lazy private var activityIndicator : CustomActivityIndicatorView = {
  let image : UIImage = UIImage(named: "loading")!
  return CustomActivityIndicatorView(image: image)
}() 
```
where "loading" is your image in png format. 

Then simple add it to your view:

```
self.view.addSubview(activityIndicator)
```

And run animation:

```
activityIndicator.startAnimating()
```

To stop animation call:

```
activityIndicator.stopAnimating()
```

![Alt text](https://github.com/snyuryev/snyuryev.github.io/raw/master/images/customActivityIndicatorSwift.png "Loading indicator")
