I am facing a problem running older versions of Xcode on new Monterey OS.

[![](https://i.stack.imgur.com/VEc6f.png?s=64&g=1)](https://i.stack.imgur.com/VEc6f.png?s=64&g=1)

stackich

The solution is very simple. If you have the older version downloaded in your Applications folder for example, lets say `12.5.1` version, you just need to:

- Open Terminal
- Open Applications folder
- Drag the Xcode app into Terminal so it gets its path
- Then add this next to it: `/Contents/MacOS/Xcode`, so the full command will be something like `/Applications/Xcode-12.5.1.app/Contents/MacOS/Xcode`
- Press enter to run the command

Now you should be able to run it. You will note that when you open this version of Xcode, the Terminal will open too, but don’t close Terminal because it will close the Xcode too.[Here](https://developer.apple.com/download/all/?q=xcode) you can find older Xcode versions.

[![](https://www.gravatar.com/avatar/f9aab67045fa891d26b9a14a215a512a?s=64&d=identicon&r=PG&f=1)](https://www.gravatar.com/avatar/f9aab67045fa891d26b9a14a215a512a?s=64&d=identicon&r=PG&f=1)

Nimantha

Just change build version to build version of Xcode 13.1 (19466), run Xcode and change build version back to original (18212). First run of Xcode takes some time

```Plain
/usr/libexec/PlistBuddy -c 'Set :CFBundleVersion 19466' /Applications/Xcode_12.5.1.app/Contents/Info.plist

open /Applications/Xcode_12.5.1.app/

/usr/libexec/PlistBuddy -c 'Set :CFBundleVersion 18212' /Applications/Xcode_12.5.1.app/Contents/Info.plist
```

[![](https://i.stack.imgur.com/VEc6f.png?s=64&g=1)](https://i.stack.imgur.com/VEc6f.png?s=64&g=1)

stackich

This is how you get your xcode’s current build version.

```Plain
/usr/libexec/PlistBuddy -c "Print CFBundleVersion" /Applications/Xcode_12.4.app/Contents/Info.plist
```

> 本文由简悦 SimpRead 转码