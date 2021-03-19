# Dependable API Evolution

The problem that prompted me to write this: I am sick and tired of APIs that do not evolve and that have old warts that are not fixed. At the same time I hate APIs that make every update to multi hour 'joy-ride' of debugging and finding out why the heck my system doesn't work anymore.

For this I think that [Semantic Versioning](https://semver.org) is just not enough.

As an API provider you should adopt a dependable API evolution strategy that gives your users timely updates and new functionality, makes updating to a your newest version a breeze and joy because of new features instead of a reason for despair because of the amount of work it requires.

As an API user you should demand this so that you can send you patches and actually hope that they will get into the next version in a timely manner while it is not a burden to update to new revisions. And then there is the small part of actually enjoying an API that works and is extended in a good and healthy way.

Consider libraries like jQuery or Apples Cocoa where it is pretty much a no brainer to update to the newest version immediately. At the same time, they stay current and adapt and absorb new emerging patterns in a timely manner while fixing old warts and making the framework more and more consistent all the time. (Ok, some warts are not fixeable, but they try very hard)

I think it is Common Sense to do **Dependable API Evolution**, but for some reason it hasn't yet caught on as common knowledge - and there is no easy way to refer anyone to a document that explains it. So here I go.

# Problems

- API's suddenly change names / types / behaviour from version to version
- API's are suddenly removed from version to version without a warning period
- Bugs/ Inconsistencies in APIs are not fixed
- New and improved patterns or API designs are not adapted in a timely matter

Extremes to avoid:

* The *Python Standard Library Syndrome*: Your Library is so *stable* that a module has to be dead/ unmaintained for 3-5 years before you consider adding it to your library. Some symptoms: API changes rarely, your API has very inconsistent naming, and design pattern use varies widely across your API. Also many of the non core modules have alternatives in the wild that have a vastly more fluent / short / powerful / consistent / modern APIs. Consider the Python standard library. Almost no development happens in there, many of it's modules are 10 and more years old with only the most required bugfixes going in. Not even the standard naming convention of python is used consistently throughout it's API.

* The *Python 3k Syndrome*: Your users stick with an old version of your API and are very reluctant to update. Symptoms: You are forced to release new versions of it instead focussing your engineering on the newest version. You add Interims Versions, i.e evolutions of the old API version to make it easier for your users to switch to the newest version. You release new versions of your new API that add in old features again to make it easier for your users to upgrade. Consider the introduction of Python 3.0. Nobody used it. Three major revisions where required (3.0, 3.1, 3.2) before the community is actually considering its adoption. (And now - 2021 -  some 12 years after this text was written, there is still a lot of software around that is on Python 2).

* The *Thousands of Patches Flying in Close Formation Syndrome*: Different parts of the API have very different fluency to it and don't match very well. Symptoms: Knowing one part of the API doesn't make it any easier to guess the names and workings of other parts of your API. Documentation cannot be consolidated by talking about the Design Patterns adopted by your framework, but instead is separated from each other and also very needed because you need to look at it for every module anew.

* The *DOM API Syndrome*: Different implementations / versions of your API are so inconsistent, that it is almost impossible for users to consume all of them. Symptoms: There are adapter packages around to wrap your API and make it easier for users to actually use them and allow them to target different versions of that API that are in use in the wild. Consider the success of jQuery that does nothing that hiding the DOM-APIs behind something sane and manageable. (2021 me here - the web has started to tackle this problem, but boy, is this still a nightmare. Just the fact that projects like [can I use](https://caniuse.com) are so much needed…)

* The *Ruby Debugger Syndrome*: Different versions of your API change so much that consumers are unable to evolve an API that builds on it. Symptoms: Different versions of your API have different incompatible packages that implement the same functionality in an incompatible way. Backwards compatibility is virtually impossible. Consider the different Ruby-Debugger gems that have sprung up for the various versions of the interpreter. 'ruby-debug' for Ruby 1.8, 'ruby-debugger19' and later 'debugger' for Ruby 1.9, 'byebug' for Ruby 2.0 and it seems Ruby 2.1, already needs another different debugger package. Maybe it is 'pry' now...

* The *Version 2 Rewrite Syndrome*: Symptoms: You have a branch in your repository that contains your next version, because it's so much different that you really need to retain a branch of the current version to apply bugfixes while you finish up the next version. Again, Python 2 and 3 comes to mind as an abhorrent example of this problem. 12 years after the release of Python 3.0 the, old version 2 branch was still around and kind of alive as small features where added, bugs fixed. Thats a problem - not a great achievement.

# Solutions

* Have a clear deprecation cycle and use it. It should stretch over multiple versions, and depending on the size or importance of that Deprecated API, this could be several major versions.
* Your deprecation cycle should contain these steps (which could itself be a multi version rollout)
  * Deprecated APIs are clearly marked in the documentation and source.
  * There is a clear statement in the source or documentation what the expected alternative is. What is the the developer expected to do / use instead?
  * Using a deprecated API should emit a warning.
  * Deprecated API is removed from the documentation. Still using it raises a warning.
  * Switch that warning to an error for developers, while only warning users.
  * Then and only then it should disappear. 
 
  This is the single most important thing to do, everything else follows from this.
* Don't just change / remove API. You released it? It's out there. Deprecate it but retain it for a time and then remove it! Document what users are expected to do instead. This documentation should be referred to / included in the warning that is raised when that API is used.
* Document warts that you cannot fix anymore because they are too engrained in the API and are too widely adopted. It is important that your users understand that this is a wart and nothing to use as an example for others or patches that they send you. This ensures that your errors of the past are not repeated.
* Never miss an opportunity to change your API to make it more uniform and or adopt a deeper pattern across it.
* Focus a major part of your documentation on the patterns that underly your API and then don't repeat yourself in every part of the documentation but just refer to it.

Do this and your API becomes more and more coherent over time. Users of such an API can often just use  a broad lisit of your API packages / objects / methods that are easy to scan / search. With that they can get an overview of what is available at a glance. They will often not need detailed documentation as they can just guess how stuff works, what stuff is named, how error handling works, … All of that makes for coding that is enjoyable and code just flows out of your fingers.

Also, users will update in a heartbeat allowing you to actually focus on newer versions, instead of having to maintain long term stable old versions and waste developer time on this rather non productive stuff.

What do you think? Should I set up a webpage like  [semver.org](http://semver.org)? Do we need stickers like ![Dependable API Evolution](https://img.shields.io/badge/Dependable%20API%20Evolution-1.0-success)?
