# Installation (CocoaPods)

It is strongly suggested to use [cocoapods](https://cocoapods.org) as it is the easiest way to embed the library in your project.

Your Podfile should include the sub project `SBTUITestTunnel/Server` for the app target and `SBTUITestTunnel/Client` for the UI test target.

    use_frameworks!

    target 'APP_TARGET' do
      pod 'SBTUITestTunnel/Server'
      pod 'GCDWebServer', :inhibit_warnings => true
    end

    target 'UITESTS_TARGET' do
      pod 'SBTUITestTunnel/Client'
    end


## 🔥 Installation issues (_framework not found_)

If you’re using CocoaPods v1.0 and your UI Tests fail to start, you may need to add $(FRAMEWORK_SEARCH_PATHS) to your Runpath Search Paths in the Build Settings of the UI Test target!

# Installation (Manual)

1. Add the `Server` folder to the app target
2. Add the `Client` folder to the ui test target
3. Add the `Common` folder to both targets
4. Download the latest release of [GCDWebServer](https://github.com/swisspol/GCDWebServer) then add the all the files under GCDWebServer/Core, GCDWebServer/Requests and GCDWebServer/Responses to a single `GCDWebServer` subfolder to your Xcode project.
5. Add $(SDKROOT)/<path to the GCDWebserver folder in 4.> to your header search paths (via Target > Build Settings > HEADER_SEARCH_PATHS)
5. Link to libz (via Target > Build Phases > Link Binary With Libraries)

If you're on an Objective-C project
1. In your AppDelegate #import "SBTUITestTunnelServer.h" and call [SBTUITestTunnelServer takeOff] as the first line in appDidFinishLaunching. **You need to wrap the import statement around an #if DEBUG conditional**, see [Setup](Setup.md) section for additional details.
2. Add #import "SBTUITunneledApplication.h" and #import "XCTestCase+AppExtension.h" on top of all your UI Test Cases files

If you're on a Swift project:
1. Add "SBTUITestTunnelServer.h" to the Application's bridging header file and call SBTUITestTunnelServer.takeOff() as the first line in appDidFinishLaunching. **You need to wrap the import statement around an #if DEBUG conditional**, see [Setup](Setup.md) section for additional details.
2. Add #import "SBTUITunneledApplication.h" and #import "XCTestCase+AppExtension.h" to your UITesting's bridging headers files

