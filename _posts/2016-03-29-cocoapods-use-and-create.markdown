---
layout: post
title:  "cocoapods use and create"
date:   2016-03-29 03:00:08
categories: jekyll update
comments: false
---
### Install

```
sudo gem install cocoapods
```
### Init
Enter project directory 
    
 ```
 pod init
 ``` 
    
find Podfile，enter

  ```
    platform :ios, '8.0'
    use_frameworks!

    target 'MyApp' do
      pod 'AFNetworking', '~> 2.6'
      pod 'ORStackView', '~> 3.0'
      pod 'SwiftyJSON', '~> 2.3'
    end
  ```

Enter project directory 

 ```
 pod install
 ```  
then
 
 ```
 $ open App.xcworkspace
 ```
import

```
#import <Reachability/Reachability.h>
```   

#Publish cocoapod

### 1、Create the Project
under your work directory（demo as **BlinkingLabel** )
  
```  
pod lib create BlinkingLabel
```
need answer some question
 
 ```
 language swift 
 demo app 选择 YES
 ```
### 2、Updating Your Pod's Metadata  

three file

* **.podspec**: version，author，homepage
* **README**: some introduce of you project
* **LICENSE**:MIT

under  **BlinkingLabel/Podspec Metadata/BlinkingLabel.podspec** find  **.podspec** 。
   
```
pod lib lint BlinkingLabel.podspec
``` 
check **.podspec**，will warning
 
```
    > pod lib lint BlinkingLabel.podspec
    
    -> BlinkingLabel (0.1.0)
    - WARN  | The summary is not meaningful.
    - WARN  | The description is not meaningful.
    - WARN  | There was a problem validating the URL      https://github.com/<GITHUB_USERNAME>/BlinkingLabel.
 
    [!] BlinkingLabel did not pass validation.
        You can use the `--no-clean` option to inspect   any issue.
```
some recommend value

* **s.summary:** A subclass on UILabel that provides a blink.
* **s.description:** This CocoaPod provides the ability to use a UILabel that may be started and stopped blinking.
* **s.homepage:** https://github.com/obuseme/BlinkingLabel (replace obuseme with your GitHub username)

but  no github repo，goto github new **Repository** call **BlinkingLabel** 

```
    git add .
    git commit -m “Initial Commit"
    git remote add origin https://github.com/  <GITHUB_USERNAME>/BlinkingLabel.git // replace <GITHUB_USERNAME> with your github.com username
    git push -u origin master
```
execute
   
```
pod lib lint BlinkingLabel.podspec
```
output

```
    > pod lib lint BlinkingLabel.podspec                                
 
    -> BlinkingLabel (0.1.0)
 
    BlinkingLabel passed validation.
```
     
### 3、Add code
under  **Pods/Development Pods/BlinkingLabel/Pod/Classes/** delete **ReplaceMe.swift** ,create **BlinkingLabel.swift**, input

 ``` 
    public class BlinkingLabel : UILabel {
    public func startBlinking() {
        let options : UIViewAnimationOptions = ［.Repeat,.Autoreverse]
        UIView.animateWithDuration(0.25, delay:0.0, options:options, animations: {
            self.alpha = 0
            }, completion: nil)
    }
 
    public func stopBlinking() {
        alpha = 1
        layer.removeAllAnimations()
    }
    }
 ```
open **BlinkingLabel/Example for BlinkingLabel/ViewController.swift** ,input
 
 ```   
    import UIKit
    import BlinkingLabel
 
    class ViewController: UIViewController {
 
    var isBlinking = false
    let blinkingLabel = BlinkingLabel(frame: CGRectMake(10, 20, 200, 30))
 
    override func viewDidLoad() {
        super.viewDidLoad()
 
        // Setup the BlinkingLabel
        blinkingLabel.text = "I blink!"
        blinkingLabel.font = UIFont.systemFontOfSize(20)
        view.addSubview(blinkingLabel)
        blinkingLabel.startBlinking()
        isBlinking = true
 
        // Create a UIButton to toggle the blinking
        let toggleButton = UIButton(frame: CGRectMake(10, 60, 125, 30))
        toggleButton.setTitle("Toggle Blinking", forState: .Normal)
        toggleButton.setTitleColor(UIColor.redColor(), forState: .Normal)
        toggleButton.addTarget(self, action: "toggleBlinking", forControlEvents: .TouchUpInside)
        view.addSubview(toggleButton)
    }
 
    func toggleBlinking() {
        if (isBlinking) {
            blinkingLabel.stopBlinking()
        } else {
            blinkingLabel.startBlinking()
        }
        isBlinking = !isBlinking
    }
    }
 ```
enter Example， pod install

 ``` 
    > cd Example 
    > pod install
    Analyzing dependencies
    Fetching podspec for `BlinkingLabel` from `../`
    Downloading dependencies
    Installing BlinkingLabel 0.1.0 (was 0.1.0)
    Generating Pods project
    Integrating client project  
 ```   
run Example project

### 4、upload Pod

####1、Add Tag

 ```
    > git tag 0.1.0
    > git push origin 0.1.0
    Total 0 (delta 0), reused 0 (delta 0)
    To https://github.com/obuseme/BlinkingLabel.git
    [new tag]         0.1.0 -> 0.1.0
 ```   
  warning： Tag be same with s.version of .podspec

####2、valiate
```
pod spec lint BlinkingLabel.podspec
```   
  output：
    
   ```   
   > pod spec lint BlinkingLabel.podspec 
   -> BlinkingLabel (0.1.0)
   Analyzed 1 podspec.
   BlinkingLabel.podspec passed validation.
   ```
#### 3、push pod to **Specs Repository**
 
 ```
 pod trunk push BlinkingLabel.podspec
 ```   
 output：
  
```
     > pod trunk push BlinkingLabel.podspec 
     Updating spec repo `master`
 
     Validating podspec
     -> BlinkingLabel (0.1.0)
 
    Updating spec repo `master`
 
     - Data URL: https://raw.githubusercontent.com/CocoaPods/Specs/f7fb546c4b0f80cab93513fc228b274be6459ad2/Specs/BlinkingLabel/0.1.0/BlinkingLabel.podspec.json
     - Log messages:
    - June 29th, 20:40: Push for `BlinkingLabel 0.1.0' initiated.
    - June 29th, 20:40: Push for `BlinkingLabel 0.1.0' has been pushed (1.701885099 s).
```
All done

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
