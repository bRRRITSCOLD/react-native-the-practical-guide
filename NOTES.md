# Notes

## Links
1. [https://academind.com/tutorials/react-native-vs-flutter-vs-ionic-vs-nativescript-vs-pwa/](https://academind.com/tutorials/react-native-vs-flutter-vs-ionic-vs-nativescript-vs-pwa/)
2. [https://reactnative.dev/docs/colors](https://reactnative.dev/docs/colors)
3. [https://reactnative.dev/docs/flexbox](https://reactnative.dev/docs/flexbox)
4. [https://academind.com/tutorials/react-hooks-introduction](https://academind.com/tutorials/react-hooks-introduction)
5. [https://reactjs.org/docs/hooks-intro.html](https://reactjs.org/docs/hooks-intro.html)

[ -d "$HOME/Library/Android/sdk" ] && ANDROID_SDK=$HOME/Library/Android/sdk || ANDROID_SDK=$HOME/Android/Sdk
echo "export ANDROID_SDK=$ANDROID_SDK" >> ~/`[[ $SHELL == *"zsh" ]] && echo '.zshenv' || echo '.bash_profile'`

echo "export PATH=$HOME/Library/Android/sdk/platform-tools:\$PATH" >> ~/`[[ $SHELL == *"zsh" ]] && echo '.zshenv' || echo '.bash_profile'`
