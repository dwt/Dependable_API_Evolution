# Dependable API Evolution

The problem that prompted me to write this: I am sick and tired of APIs that do not evolve and that have old warts that are not fixed. At the same time I hate APIs that make every update to multi hour 'joy-ride' of debugging and finding out why the heck my system doesn't work anymore.

For this I think that 'Semantic Versioning' is just not enough, as an API provider you should adopt a dependable API evolution strategy that gives your users timely updates and new functionality, makes updating to a your newest version a breeze and a case for joy because of the new features instead of a reason for despair because of the amount of work it requires to 

For your users it means that they can send you patches and actually hope that they will get the next version that includes them in a timely manner into their hand, getting new features regularly and will enjoy using your API so much more than any alternative because of it.

Consider libraries like jQuery or Apples Cocoa where it is pretty much a no brainer to update to the newest version immediately. At the same time, they stay current and adapt and absorb new emerging patterns in a timely manner while fixing old warts and making the framework more and more consistent all the time. (Ok, some warts are not fixeable, but at they try very hard)

I think it is Common Sense to do <<Dependable API Evolution>>, but for some reason it hasen't yet cought on as common knowledge and there is no easy way to refer anyone to a document that explains it. So here we go.

## Problems

- API's change names / types / behavior from version to version
- API's removed from version to version
- Bugs/ Inconsistencies in APIs are not fixed
- New and improved patterns or api designs are not adapted in a timely matter

TODO: explain what changes I mean  names (functions, classes, methods, arguments)

Extremes to avoid:

* The 'Python Standard Library Syndrome': Your Library is so 'stable' that a module has to be dead/ unmaintained for 3-5 years before you consider adding it to your library. Some symptoms: API changes rarely, many of the non core modules have alternatives in the wild that have a vastly more fluent / short / powerfull / consistent / modern API. Consider the python standard library. Almost no development happens in there, many of it's modules are 10 and more years old with only the most required bugfixes.

* The 'Python 3k Syndrome': Your users stick with an old version of your API and are very reluctant to update. Symptoms: You are forced to release new versions of it instead focussing your engineering on the newest version. You add Interims Versions, i.e evolutions of the old API version to make it easier for your users to switch to the newest version. You release new versions of your new API that add in old features again to make it easier for your users to upgrade. Consider the introduction of Python 3.0. Nobody used it. Three major revisions where required (3.0, 3.1, 3.2) before the community is actually considering it's adoption.

* The 'Thousands of Patches Flying in Close Formation Syndrome': Different parts of the API have very different fluency to it and don't match very well. Symptoms: Knowing one part of the API doesn't make it any easier to guess the names and workings of other parts of your API. Documentation cannot be consolidated by talking about the patterns adopted by your framework, but instead is separated from each other and also very needed because you need to look at it for every module anew.

* The 'DOM API Syndrome': Different implementations / versions of your API are so inconsistent that it is almost impossible for users to consume all of them. Symptoms: There are adapter packages around to wrap your API and make it easier for users to actually use them and allow them to target different versions of that API that are in use in the wild.

* The 'Ruby Debugger Syndrome': Different versions of your API change so much that consumers are unable to evolve an API that builds on it. Symptoms: Different versions of your API have different incompatible packages that implement the same functionality in an incompatible way. Backwards compatibility is virtually impossible.

(not sure this is not something that should be included above)

* The 'Version 2 Rewrite Syndrome': Symptoms: You have a branch in your repository that contains your next version, because it's so much different that you really need to retain a branch of the current version to apply bugfixes while you finish up the next version.

## Solutions

* Have a deprecation cycle and use it. Deprecated API should be clearly marked in the documentation and source. Using it should emit a warning at some point. At some point it should not be in the documentation anymore and using it should raise a warning. Then and only then it should disapear. This is the single most important thing to do as everything else follows from this.
* Don't just change / remove API. You released it? It's out there. Deprecate it but retain it for a time and then remove it! Document what users are expected to do instead. This documentation should be referred to / included in the warning that is raised when that API is used.
* Document warts that you cannot fix anymore because they are too engrained in the library and are too widely adopted. It is important that your users understand that this is a wart and nothing to use as an example for other patches that they send you and the errors of the past do not repeat themselves.
* Never miss an opportunity to change your API to make it more uniform and or adopt a deeper pattern across it.
* Focus a major part of your documentation on the patterns that underly your API and then don't repeat yourself in every part of the documentation but just refer to it.
* Provide lists of your API packages / objects / methods that are easy to scan / search. This allows your users to get an overview of what is availeable at a glance. They will often not need detailed documentation as they can just guess how stuff works and what it does.

Goals:
- Make it easy for your users / consumers to timely update to new versions of your api
- Ideally you only ever have one version of your API to maintain


Think you have an improved way to say what this page wants to say? Send a pull request.