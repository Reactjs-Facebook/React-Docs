We wanted to test it out on a real project, so here we go. What you are about to read is our experience with React Native after the completion of a small real project.

These are the advantages of the React Native libraries everybody on the internet is talking about:

Performance rates close to those of the native platforms.
No need to duplicate the business logic and UI particularly for every platform. The code base is unified.
No need to know multiple languages, JavaScript is just enough (sort of).
Write one source code and happily run it on different platforms.
React Native is growing by leaps and bounds.
Significant time & cost savings.
And what not.
With that said, React Native seem to be quite low on disadvantages so far. Most of them are referred to in the “this is still a fairly new technology” type of context. Further on, I’ll try to either confirm these points or debunk the hell out of them.

Project Toolbox

So these are the technologies and tools used in the project:

Environment:

Atom + Nuclide + Flow + ESlint + a whole bunch of various helper packages that uhm… help. Early on I tried to figure out which of them would be useful and which not, but then I got tired of that and installed everything they recommend in tutorials and help guides.
I really recommend setting up Flow. You don’t want to end up without a static type checking.
The ESlint linter must also be set up. There are some other linters, you definitely need one, otherwise, the quality of your JS code will leave much to be desired.
Xcode, Android Studio.
Npm, yarn are the package managers and as I found out along the way, yarn is way more stable so I suggest using yarn.
Frameworks & Libraries:

React Native.
Redux + Saga. Invest some time into learning these two great things. I won’t go down a rabbit hole here, but Redux is perfect for storing your app’s state and Saga is good at implementing different side effects. They work well in conjunction and significantly improve project development and maintenance.
Firebase Authentication, Storage, Realtime Database.
Multiple open-source libraries and components expanding the capabilities of React Native.
Project Development Sequence

The first thing I stumbled upon was setting up Atom. Unfortunately, nothing works out of the box here. I spent an entire day installing and tuning different packages, however, this is a one-time operation and I believe a web developer familiar with all this mumbo jumbo would get through this much faster. After that, on the exit I had a static type check due to Flow, a static analyzer with autocorrect due to ESLint, and autocomplete and snippets due to God knows who because I installed a bunch of different packages.

Having grasped the magic of JS and React Native by reading the original documentation and pretty much all the articles I could find, I moved on to the first project tasks.

I actually was surprised by how good everything was going down — the components were easily customized through the styles, layouts worked perfectly with FlexBox. Nothing was lagging and was really magically working.

First Mistake

This is where I messed up for the first time. I was only testing for iOS and having launched the app on Android, I realized some styles that work fine on iOS are broken for Android. In most cases, to fix an issue or find a workaround, all you need is to dig into the “issues” section of React Native on GitHub and try some of the methods from there.

However, the success of this might depend on a wide variety of factors from style combinations to components hierarchy in your render method. This did not bug me much, as all I had to do is to test every component’s workability on all the platforms. In fact, finding workarounds for this type of issues accumulatively takes way too much time.

Third-Party Libraries

As I was moving on, I found out that the standard React Native components were not enough but there is an abundance of custom third-party libraries and components for React Native. And there really is something to choose from, while the quality and stability of the majority of components leave a lot to be desired. Even the connection to a lot of iOS components turns into a serious quest. For Android, the command react–native link is usually enough. I worked up the following algorithm:

Install as it is recommended for the package. As a rule, it’s the yarn add + pod install + comboreact–native link.
If this doesn’t work, try to do the same manually but without react–native link but with the use of cocoapods.
If this doesn’t work either, try copying all the native dependencies of the library into your project.
If the previous step failed epically as well, take the entire library, copy it to a separate folder, find the problem in the library settings, fix it, and then connect with the help of yarn add and a local path to the fixed library.
Using this many open-source components made me feel like a sapper on a minefield with no clue of where the next explosion is going to be. To make it worse, one component may work just fine on one platform and fail on the other, as under the common JS wrapper, native libraries for every platform may differ and so does their behavior. With that said, a bug might be in a native library or in the JS wrapper (if there is a logic and it’s more than just methods mapping), or even in the native wrapper of the native library — as weird as it gets.

You may ask, why not write components and libraries yourself? But then what’s the point of using React Native at all? We are in a scenario of a business project and trying to save time/money on development, aren’t’ we?

The Killer Feature

React Native Hot/Live reload is a great feature allowing to write the code and right away see the changes without the complete rebuilding of the app. The thing is, this feature is vital for React Native due to the unpredictability and rawness of the latter and the third-party packages, where you constantly have to check the results of the actions you take.

Developing on the native platforms does not require that many builds, usually the device/emulator check is performed once the functionality is done or almost done. In between, you just write your code and do not really fear to deliver a result different from what you’ve expected it to be.

My React Native Experience

To sum up all the implications:

Performance

Performance close to that of a native platform. Really so. Up until you have a simple UI, no complex computations and processing, and the number of components is low. If these are not quite the features of your project, without a doubt you’ll face the productivity issues and memory usage. Some of them can be solved by means of Saga, partially Debounce and Throttle plus the correct component partition to avoid the re-rendering of everything upon the smallest changes. Some of the issues just won’t resolve and you’ll have to deal with them.

Duplication

No need to duplicate the business logic and UI particularly for every platform. The code base is unified. True. Again, if your business logic is not too complicated or resource-consuming and the native platform integration does not go beyond React Native. Also, if the UI is identical for both platforms. However, most of the large projects do not satisfy these two conditions, the UI adapts to the specifics of a platform, and the logic of the application requires at least support of concurrency. On top of that, if you need some functionality that React Native lacks, you’ll have to implement them separately for each platform.

Uniformity

No need to know multiple languages, JavaScript is just enough (sort of). Sorry folks, not this time. Stray from normal path, and the project will require deep knowledge of native platform from you. If you don’t have those, you’ll end up with a project that works on some mysterious force and God knows how. And if you do have the specific knowledge, and your project has the specific design, performance, and stability requirements, then why would you set yourself up to the restrictions and hassle of React Native?

Single source

Write one source code and happily run it on different platforms. Nope. Write one source code, cross your fingers, make a sacrifice, and then wait for a viable result maybe. I should say though, the feeling of delight seeing the app not crashing in this circumstance is stronger than in native development.

Growth

React Native is growing by leaps and bounds. It really is, even too fast. Imagine you are working on a project and somewhere in the middle of the development st, ge you find a critical error in a third-party library, or worse — in React Native itself. But this is not so much of an issue due to the newer versions being regularly released and chances are the error might be fixed in a newer version. All you need to do is update to the latest version. Where can this lead us? Correct — the regressive testing of the entire application. This is half the trouble. If your luck fails you, the third-party components and libraries might turn out to be incompatible with the newer version of React Native.

Efficiency

Significant time & cost savings. This is the most arguable point, I believe. If you are up to implementing a quick prototype or a small MVP with no specific requirements quality-wise, in stability, and performance. If you don’t need UI adaptations to a platform, or your app is not heavy on the platform-specific functionality, you can benefit from React Native. In any other case, you will not only fail to save time, but waste a lot of developer energy on a product that won’t be even close to a native one. In case you are simply not equipped with iOS/Android developers but you are in for mobile development, a front-end developer with React Native is the option for you.

Final Conclusion

New technologies marching towards cross-platforming and cost reduction is a thing of beauty. However, the tool to reach that has to be selected depending on the task. Regardless of how good and popular it is, it has to be relevant. For example,

There is no need to use the early React Native for larger projects with deep integration into native platforms and high standards for stability and performance. This is won’t be cost-cutting.
I urge you to not use the serverless solutions (Firebase, AWS Mobile Hub) for heavy-loaded systems with complex logic, i.e. where there has to be a full-blown back end with a custom API.
All these attempts usually fail and as the result lead to more additional costs to fix the repercussions of the wrong initial choice.
