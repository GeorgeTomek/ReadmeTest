# Apprentice HoloLens Application

Unity3D Application for HoloLens device 

## Build process
#### Prerequisites:
- Unity 2017.4.6f1 with UWP support
- Visual Studio 2017 with UWP development, Windows 10 SDK (10.0.16299.0) and Game development with Unity

#### Unity:
To edit the project inside Unity Editor you have to make sure that all [directives](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if)(#if) are set to false. If Unity Editor shows a lot of errors complaining about missing reference than do the following. Navigate to Scripts folder and open any of the available C# scripts with Visual Studio. Then press CTRL + H, and fill values based on the image below.

![Replace All Image](https://github.com/ApprenticeFS/apprentice-hololens/blob/development/GitResources/replace_all.png)

Either click on highlighted button or press ALT + A to replace all values. After that click on Save All (CTRL + SHIFT + S).

Now we can build our project. File > Build Settings and make sure everything corresponds to the image below.

![Build Settings Image](https://github.com/ApprenticeFS/apprentice-hololens/blob/development/GitResources/build_settings.png)

Click on Build and select the output folder (create an empty folder called "Build" next to our Unity project folder)

#### Visual Studio:
If Unity successfully built our project we now have an UWP project in "Build" folder. Open ApprenticeHoloLens solution and navigate to **Package.appxmanifest**, right click and select View Code. Here we need to add this block of code to enable WebRTC functionality

```
  <Extensions>
    <Extension Category="windows.activatableClass.inProcessServer">
      <InProcessServer>
        <Path>WebRtcScheme.dll</Path>
        <ActivatableClass ActivatableClassId="WebRtcScheme.SchemeHandler" ThreadingModel="both" />
      </InProcessServer>
    </Extension>
  </Extensions>
```

This goes between 

```
</Capabilites>
```
and 
```
</Package>
```

Next on the program is updating NuGet packages. Right click on ApprenticeHoloLens Solution and select **Manage NuGet Packages for Solution**. Here we select Microsoft.NETCore.UniversalWindowsPlatform package and check both projects. In Version dropdown menu select atleast 6.1.7 and click on Install. This is important for our communication with Amazon S3.

Navigate to Assembly-CSharp project > Scripts folder and select one of the scripts. We need to change all the directives(#if) to true. Please follow the instruction above (**Unity Section**) but this time switch **#if true** with **#if false**. Save All and now we should be able to build and deploy our application into HoloLens.
If you are not sure how to deploy UWP app please follow [this tutorial](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio)
