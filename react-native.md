# React Native

## Upgrading from 0.55.4 to 0.60.0
Went through the diffs in React Native Upgrade Guide and changed all the necessary files.
Need to remove all the libraries from the Libarires folder in Xcode that are now gonna be included as a CocoaPod (this is all the react stuff)
and also any 3rd party libraries that changed.


If a 3rd party library hasnt changed the implementation to use Cocoa Pods, I encountered a problem. These libraries cannot find the React header
files (which are now included through cocoapods). Adding the header file path into Build Settings -> Header Search Paths also did not help.


What I did was to turn these libraries into cocoa pods.

WIP
