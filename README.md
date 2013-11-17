Xcode-BuildNumber
=================

Automatic increment Xcode project build number and set builddate

### Easy increment your buildnumer in Xcode

Xcode Auto Increment CFBuildNumber, is a a simple shell script that increments your buildnumber, and set the builddate (timestamp) for your application. It (automatically) add's two key/value properties to your project-Info.plist

+ CFBuildnumber
+ CFBuilddate 

##### CFBuildnumber 
This property is of type Number (NSNumber).

##### CFBuilddate
This property is of type Date (NSDate). CFBuildDate is stored in GMT. This can easyily adjusted within the shell script. The shell script uses:

	CFBuildDate=$(date -u +"%a %b %d %T GMT %Y")

*Its the OSX date function. Format it how you like, but remember it needs to match the date format for the `date` property (if you need to retrieve it as a `NSDate`).*

#### Example Code

Both properties can be easily be retrieved from within your application.

    NSDate *buildDate = [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBuildDate"];
    NSNumber *version =  [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBuildNumber"];

### Know issues
When opening your *project-Info.plist* file in Xcode, and it doesn't show the date, right click in the file and check `Show Raw Keys/Values`.

### Installation

+ download the **Increment Buildnumber.sh** script and place it on your project folder
+ open your xcode project
+ goto `Product` -> `Scheme` -> `Edit Scheme`
+ select the scheme you want to use for incrementing the buildnumber (i would suggest Build or Archive)
+ open the scheme (click the triangle in front)
+ select Pre-actions (i set this up as a pre-action, otherwise your buildnumber is increment **after** the build, not ideal)
+ click on the + and select `New Run Script Action`
+ Drag the **Increment Buildnumber.sh** into the placeholder


That is all.