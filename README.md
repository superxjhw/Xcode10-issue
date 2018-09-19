
---
升级到Xcode10，由于iOS12移除了libstdc++.6.0.9，所以好的办法就是把这个库用libc++替换掉。但是项目中有的第三方的静态库里面使用到了，并且还没来得及修复这个问题，实在是没得什么好办法，所以就暂时把Xcode9中的libstdc++移动到了Xcode10对应目录下，之后再处理了。具体路径-->

```
cp /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/usr/lib/libstdc++.* /Applications/Xcode-beta.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/usr/lib/

cp /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/libstdc++.* /Applications/Xcode-beta.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/

```
这边有libstdc++.6.0.9.tbd两个平台的文件，自己复制到对应路径，运行即可。不过，模拟器会在运行时报以下错误，暂时没有找到解决办法。如果想适配iPhone XS Max，看下效果，可以通过移除掉libstdc++.6.0.9，然后看哪些三方库报错，暂时移除这些三方库，就可以了。

```
dyld: Library not loaded: /usr/lib/libstdc++.6.dylib
Referenced from: /Users/super/Library/Developer/CoreSimulator/Devices/022CC0A8-9B76-4F93-8D15-11241AA790E4/data/Containers/Bundle/Application/AD967BC3-4396-4C9A-97C6-18683C9739ED/yjtim.app/yjtim
Reason: no suitable image found.  Did find:
/usr/lib/libstdc++.6.dylib: mach-o, but not built for iOS simulator
```
