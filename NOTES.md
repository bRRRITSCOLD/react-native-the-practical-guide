# Notes

## Links
1. [https://academind.com/tutorials/react-native-vs-flutter-vs-ionic-vs-nativescript-vs-pwa/](https://academind.com/tutorials/react-native-vs-flutter-vs-ionic-vs-nativescript-vs-pwa/)
2. [https://reactnative.dev/docs/colors](https://reactnative.dev/docs/colors)
3. [https://reactnative.dev/docs/flexbox](https://reactnative.dev/docs/flexbox)
4. [https://academind.com/tutorials/react-hooks-introduction](https://academind.com/tutorials/react-hooks-introduction)
5. [https://reactjs.org/docs/hooks-intro.html](https://reactjs.org/docs/hooks-intro.html)
6. [https://developer.chrome.com/docs/devtools/](https://developer.chrome.com/docs/devtools/)
7. [https://docs.expo.io/versions/v34.0.0/workflow/debugging/](https://docs.expo.io/versions/v34.0.0/workflow/debugging/)
8. [https://reactnative.dev/docs/colors](https://reactnative.dev/docs/colors)

[ -d "$HOME/Library/Android/sdk" ] && ANDROID_SDK=$HOME/Library/Android/sdk || ANDROID_SDK=$HOME/Android/Sdk
echo "export ANDROID_SDK=$ANDROID_SDK" >> ~/`[[ $SHELL == *"zsh" ]] && echo '.zshenv' || echo '.bash_profile'`

echo "export PATH=$HOME/Library/Android/sdk/platform-tools:\$PATH" >> ~/`[[ $SHELL == *"zsh" ]] && echo '.zshenv' || echo '.bash_profile'`

React Native Styling vs CSS Styling
Styling in React Native is inspired by CSS - but it's not equivalent!

You must never forget that React Native in the end is all about translating React components (like <View> or <Text>) to native widgets (like UIView or widget.view - see section 1 of the course, I do dive into this there)!

These native widgets don't understand CSS. They have nothing to do with the web, HTML or anything like that!

What the React Native team does, is the following: They also provide "style translations" => CSS-inspired styling commands/ properties which also are translated to styling configurations those native widgets understand.

Hence backgroundColor: 'black' works - it simply targets the platform-specific configurations for the native widget that will result in a black background to be drawn. Even if these native instructions look nothing like CSS. React Native does the heavy lifting behind the scenes.

That's why many but absolutely not all CSS properties are supported in React Native. That's also why styling is done via JavaScript and not CSS. In addition, not all React Native components support all style properties.

`<Text>` doesn't support flexbox-related properties for example - but I'll dive into this later in the course.