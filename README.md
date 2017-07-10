# UITest SpecFlow example

This project demonstrates how to use SpecFlow with Xamarin.UITest and is based on the the [page object pattern example](https://github.com/xamarin-automation-service/uitest-pop-example).

## Running these tests on your Mac

1. Add "Straight8's SpecFlow Integration" extension to Visual Studio for Mac
    1. Go to the "Visual Studio" menu and click "Extensions..."
    1. Search for "SpecFlow" and install
    1. You might also want the "FileNesting" extension to help keep everything tidy
    1. Restart Visual Studio
1. Clone this repo
1. Build
1. Run*

_*If you want to run this on a physical iOS device, you will need to clone and build the app from [source](https://developer.xamarin.com/samples/test-cloud/TaskyPro/TaskyPro-Calabash/) in order to get an IPA file that is compatible with your device._

## SpecFlow Implementation

1. Create a new SpecFlow NUnit Library Project (under Other -> Miscellaneous in the new project dialogue).

1. Remove all the NuGet packages and reinstall SpecFlow.NUnit version 1.1.1, SpecFlow version 2.1.0, and NUnit version 2.6.4.

    _Note: the version numbers are very important. Until [Test Cloud supports NUnit 3](https://testcloud.ideas.aha.io/ideas/XTA-I-124), your tests will not run unless you use these exact versions._

1. Manually add the following files to your project (making sure to change the namespaces to match your own):
    * [AppManager.cs](Xamarin.UITest.SpecFlow/AppManager.cs)
    * [BaseTestFixture.cs](Xamarin.UITest.SpecFlow/BaseTestFixture.cs)
    * [BasePage.cs](Xamarin.UITest.SpecFlow/BasePage.cs)
    * [PlatformQuery.cs](Xamarin.UITest.SpecFlow/PlatformQuery.cs)

1. Use the SpecFlow file templates to add a new feature file.
    * This will add two files to your project: MyTest.Feature and MyTests.feature.cs.
    * The first file is where you will write your scenarios for this feature and the second file is an autogenerated backing file that you cannot edit directly.
    * You will want to add another empty class file to your project and name it MyTestsFeature.cs (the same name as the partial class in MyTests.feature.cs)
    * Replace the class definition in this file with:
        ```csharp
        [TestFixture(Platform.Android)]
        [TestFixture(Platform.iOS)]
        public partial class MyTestsFeature : BaseTestFixture
        {
            public MyTestsFeature(Platform platform)
                : base(platform)
            {
            }
        }
        ```
        This makes sure that your app gets set up properly before each test and lets NUnit find all your tests to run.

1. Add a step definition file for each page in your app. Each step will call the corresponding method in the corresponding page object.

1. Follow the [page object pattern](https://github.com/xamarin-automation-service/uitest-pop-example) to build pages that interact with your app.

## Contributors

* [Charles Wang](https://github.com/chawang)
* [Ethan Dennis](https://github.com/erdennis13)
* [Matisse Hack](https://github.com/MatisseHack)
* [Sweekriti Satpathy](https://github.com/Sweekriti91)