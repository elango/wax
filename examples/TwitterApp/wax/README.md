Wax
===

Wax is a framework that lets you write iPhone apps in [Lua](http://www.lua.org/about.html). It bridges Objective-C and Lua using the Objective-C runtime. With Wax, anything you can do in Objective-C is **automatically** available in Lua! What are you waiting for, give it a shot!

Setup
-----

1. Download wax [http://github.com/probablycorey/wax/downloads](http://github.com/probablycorey/wax/downloads)

2. From the command line, **cd** into wax folder and type **rake install**. This will install an xcode project template.

3. Open up xcode and create a new **Wax** project, it should be located under the **User Tempates** section. 

4. Build and Run! You've got lua running on the iPhone!

5. Start editing **wax/data/scripts/AppDelegate.lua** to make your app!

Why?
----

I love writing iPhone apps, but would rather write them in a dynamic language than in Objective-C. Here are some reasons why many people prefer Lua + Wax over Objective-C...

* Automatic Garbage Collection! Gone are the days of release and autorelease.

* Less Code! No more header files, no more static types, array and dictionary literals! Lua enables you to get more power out of less lines of code.

* Access to every Cocoa, UITouch, Foundation, etc.. framework, if it's written in Objective-C, Wax exposes it to Lua automatically. All the frameworks you love are all available to you!

* Super easy HTTP requests. Interacting with a REST webservice has never been eaiser

* Lua has closures, also known as blocks! Anyone who has used these before knows how powerful they can be.

* Lua has a build in Regex-like pattern matching library.


You get all of this with Lua, with no downside!

Examples
--------

How would I create a UIView and color it red?
    
    -- forget about using alloc! Memory is automatically managed by Wax
    view = UIView:initWithFrame(CGRect(0, 0, 320, 100))
    
    -- use a colon when sending a message to an Objective-C Object
    -- all methods available to a UIView object can be accessed this way
    view:setBackgroundColor(UIColor:redColor())

What about methods with multiple arguments?

    -- Just add underscores to the method name, then write the arguments like
    -- you would in a regular C function
    UIApplication:sharedApplication():setStatusBarHidden_animated(true, false)

How do I send an array/string/dictionary

    -- Wax automatically converts array/string/dictionary objects to NSArray,
    -- NSString and NSDictionary objects (and vice-versa)
    images = {"myFace.png", "yourFace.png", "theirFace.png"}
    imageView = UIImageView:initWithFrame(CGRect(0, 0, 320, 460))
    imageView:setAnimationImages(images)

What if I want to create a custom UIViewController?

    -- Created in "MyController.lua"
    --
    -- Creates an Objective-C class called MyController with UIViewController
    -- as the parent. This is a real Objective-C object, you could even 
    -- reference it from Objective-C code if you wanted to.
    waxClass{"MyController", UIViewController}

    function init()
      -- to call a method on super, simply use self.super
      self.super:initWithNibName_bundle("MyControllerView.xib", nil)
      return self
    end

    function viewDidLoad()
      -- Do all your other stuff here
    end
    
You said HTTP calls were easy, I don't believe you...

    url = "http://search.twitter.com/trends/current.json"
    
    -- Makes an asyncronous call, the callback function is called when a 
    -- response is received
    wax.http.request{url, callback = function(body, response)
      -- request is just a NSHTTPURLResponse
      puts(response:statusCode())
      
      -- Since the content-type is json, Wax automatically parses it and places
      -- it into a Lua table
      puts(body)       
    end}
    
Which API's are included?
-------------------------

They all are! I can't stress this enough, anything that is written in Objective-C (even external frameworks) will work automatically in Wax! UIAcceleration works like UIAcceleration, MapKit works like MapKit, GameKit works like GameKit, Snozberries taste like Snozberries!

Created By
----------
Corey Johnson (probablycorey at gmail dot com)

Acknowledgements
----------------

[Aman Gupta](http://github.com/tmm1): For adding YAJL JSON support.

[Apple](http://www.apple.com/iphone/): For creating such an awesome development platform.

More
----
* [Feature Requests? Bugs?](http://github.com/probablycorey/wax/issues) - Issue tracking and release planning.
* [Mailing List](http://groups.google.com/group/iphonewax)
* [IRC: #wax](irc://chat.freenode.net/#wax) on http://freenode.net
* Quick question or problem? IM **probablyCorey** on AIM

Contribute
----------
Fork it, change it, commit it, push it, send pull request; instant glory!


The MIT License
---------------
Copyright (c) 2008
Rob Ellis, Brock Whitten, Brian Leroux, Joe Bowser, Dave Johnson, Nitobi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.