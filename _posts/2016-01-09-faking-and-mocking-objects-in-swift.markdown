---
layout: post
title: Faking and Mocking in Swift
modified:
categories: blog
excerpt: Testing functions that returns values is usually straight forward. Call the function with or without parameters, and assert the expected value. In some situations where your function does not return a value, this could be when you call some function based on user input, like a button click, it is not always straight forward to test that you have the wanted behavior. This is where you need some other means of sensing the wanted outcome.
tags: [TDD, Swift, Mocks, Fake]
image:
  feature:
date: 2016-01-09T09:54:42+01:00
---

Testing functions that returns values is usually straight forward. You simply call the function with or without parameters, and assert the returned value with an expected result. In some situations where your function does not return a value, this could be when you call some function based on user input, like a button click, it is not always straight forward to test that you have the wanted behavior. This is where you need some other means of "sensing" the outcome. This situation is quite common in viewcontrollers. This is where mocks or fakes can come in handy. Because they can act as stand-in objects for your real objects, and you can then sense the outcome through them rather than through the real objects. There is a difference between fakes (or test doubles) and mocks, which is best described by Martin Fowler in his article [Mocks Aren't Stubs][mocks_arent_stubs].

This article will use fakes/test doubles, since it currently is not possible to use any mocking frameworks in a pure swift environment.

It is however possible to use mocks with your swift class if it inherits from NSObject, and you write your tests in Objective-C, as described in this [article][ocmock] at OCMock.

In Objective-C there are several available frameworks that support mocking. The one I have had best experience with is the one written by Jon Reid, which you can find here: [OCMockito][ocmockito].

Down to business.

Here is an example of a testcase that uses a fake:

{% highlight swift %}
import XCTest

class SearchingViewControllerTests: XCTestCase {
    var searchingViewController:SearchingViewController!
    var searchPerformerFake = SearchPerformerFake()
    let textField = NSTextField()

    func setup() {
      searchingViewController = SearchingViewController()
      searchingViewController.searchPerformer = searchPerformerFake
      searchingViewController.searchField = textField
    }

    func testCanPerformSearch() {
      textField.stringValue = "DummyText"
      searchingViewController.performSearch(nil)
      XCTAssertEqual(searchPerformerFake.didPerformSearchWithText, "DummyText", "Unexpected search text")
    }

    class SearchPerformerFake: SearchPerformer {
      var didPerformSearchWithText=""

      override func runSearch(searchText:String) {
        didPerformSearchWithText = searchText
      }
    }
}
{% endhighlight %}

Here is what the implementation of the SearchingViewController might look like:

{% highlight swift %}
class SearchingViewController: NSViewController {
  @IBOutlet searchField:NSTextField!
  var searchPermformer = SearchPerformer()


  @IBAction func perfomSearch(sender:AnyObject?) {
      let searchText = textfield.stringValue
      self.performSearch(searchText)
  }

  func performSearch(searchText:String) {
    searchPermformer.runSearch(searchText)
  }
}
{% endhighlight %}

## Why should you go through the hazzle of introducing fakes?

This way of testing has the advantage that you are in full control, and you do not have to rely on any complexities going on in the SearchPerformer. After all, the only thing you should care about at this point is that the viewcontroller does what it is supposed to. And if SearchPerformer is a class you have written yourself, you have already tested that it performs in the expected way. And better yet if it is not a class you have written yourself, you can still subclass it. But be careful, if your fake starts to have complex logics in it, you should probably reconsider if you are really testing the right thing. I have also found it very helpful to use fakes when testing async callback functions when dealing with XPC-services, as this can sometimes be very cumbersome to test.

Another plus is that you can implement the fake inside your test class, which keeps the involved parts close. However sometimes I have found it an advantage to have the fake classes as separate files together under for example a "TestHelpers" group, especially when some of them are involved in more than one test case.

Good luck, and happy testing.

[mocks_arent_stubs]: "http://martinfowler.com/articles/mocksArentStubs.html"
[ocmockito]: "https://github.com/jonreid/OCMockito"
[ocmock]: "http://ocmock.org/swift/"
