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
9. [https://github.com/facebook/react-native/commit/a2a03bc68ba062a96a6971d3791d291f49794dfd](https://github.com/facebook/react-native/commit/a2a03bc68ba062a96a6971d3791d291f49794dfd)
10. [https://icons.expo.fyi/](https://icons.expo.fyi/)
11. [https://github.com/GeekyAnts/NativeBase](https://github.com/GeekyAnts/NativeBase)
12. [https://github.com/react-native-training/react-native-elements](https://github.com/react-native-training/react-native-elements)
13. [https://facebook.github.io/react-native/docs/dimensions#docsNav](https://facebook.github.io/react-native/docs/dimensions#docsNav)
14. [https://facebook.github.io/react-native/docs/platform-specific-code](https://facebook.github.io/react-native/docs/platform-specific-code)
15. [https://reactnavigation.org/docs/4.x/getting-started](https://reactnavigation.org/docs/4.x/getting-started)
16. [https://icons.expo.fyi/](https://icons.expo.fyi/)
17. [https://reactnavigation.org/docs/bottom-tab-navigator/](https://reactnavigation.org/docs/bottom-tab-navigator/)
18. [https://reactnavigation.org/docs/material-top-tab-navigator/](https://reactnavigation.org/docs/material-top-tab-navigator/)
19. [https://reactnavigation.org/docs/material-bottom-tab-navigator/](https://reactnavigation.org/docs/material-bottom-tab-navigator/)
20. [https://reactnavigation.org/docs/drawer-navigator/](https://reactnavigation.org/docs/drawer-navigator/)

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

<Text> doesn't support flexbox-related properties for example - but I'll dive into this later in the course.

<View> vs <Text> - A Summary
<Text> and <View> are probably THE most important/ most-used components built into React Native.

---

<View> is your #1 component if you need to group and structure content (= provide a layout) and/ or if you want to style something as a container (e.g. the <Card> look we built in our custom <Card> component).

<View> uses Flexbox to organize its children - have a look at the Flexbox deep dive earlier in this course (in module 2) to learn more about how that works.

A <View> can hold as many child components as you need and it also works with any kind of child component - it can hold <Text> components, other <View>s (for nested containers/ layouts), <Image>s, custom components etc.

If you need scrolling, you should consider using a <ScrollView> - you could wrap your <View> with it or replace your <View> (that depends on your layout and styling). Please note, that due to its scrollable nature, Flexbox works a bit differently on a <ScrollView>: https://stackoverflow.com/questions/46805135/scrollview-with-flex-1-makes-it-un-scrollable

---

<Text> is also super important. As its name suggests, you use it for outputting text (of any length). You can also nest other <Text> components into a <Text>. Actually, you can also have nested <View>s inside of a <Text> but that comes with certain caveats you should watch out for: https://github.com/facebook/react-native/commit/a2a03bc68ba062a96a6971d3791d291f49794dfd

Unlike <View>, <Text> does NOT use Flexbox for organizing its content (i.e. the text or nested components). Instead, text inside of <Text> automatically fills a line as you would expect it and wraps into a new line if the text is too long for the available <Text> width.

You can avoid wrapping by setting the numberOfLines prop, possibly combined with ellipsizeMode.

Example:

<Text numberOfLines={1} ellipsizeMode="tail">
  This text will never wrap into a new line, instead it will be cut off like this if it is too lon...
</Text>
Also important: When adding styles to a <Text> (no matter if that happens via inline styles or a StyleSheet object), the styles will actually be shared with any nested <Text> components.

This differs from the behavior of <View> (or actually any other component - <Text> is the exception): There, any styles are only applied to the component to which you add them. Styles are never shared with any child component!

Updating All Code to Update Dynamically
In the video lectures, I didn't change all the code to take advantage of addEventListener on Dimensions (simply to avoid unnecessary repetition).

In case you're interested, here's how you would change the code to always update your styles when the Dimensions change.

StartGameScreen.js

No changes required, all styles do update when Dimensions change.

GameScreen.js

The buttonContainer style uses Dimensions...height to change marginTop.

buttonContainer: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginTop: Dimensions.get('window').height > 600 ? 20 : 5,
    width: 400,
    maxWidth: '90%'
  },
Change this to:

buttonContainer: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    width: 400,
    maxWidth: '90%'
  },
and in your component function, use inline styles to update marginTop on the <Card> where you use styles.buttonContainer:

<Card style={[...styles.buttonContainer, {marginTop: availableHeight > 600 ? 20 : 5}]}>
    ...
</Card>
availableHeight is already some state we're managing, so you don't need to add this.

Side-note, totally unrelated to the Dimensions-listener thing: You could generally shorten the component code a little bit by only changing the NumberContainer + Button-Container part of your JSX code.

Like this:

let gameControls = (
    <React.Fragment>
        <NumberContainer>{currentGuess}</NumberContainer>
        <Card style={styles.buttonContainer}>
            <MainButton onPress={nextGuessHandler.bind(this, 'lower')}>
                <Ionicons name="md-remove" size={24} color="white" />
            </MainButton>
            <MainButton onPress={nextGuessHandler.bind(this, 'greater')}>
                <Ionicons name="md-add" size={24} color="white" />
            </MainButton>
        </Card>
    </React.Fragment>
);
 
if (availableDeviceHeight < 500) {
    gameControls =  (
        <View style={styles.controls}>
            <MainButton onPress={nextGuessHandler.bind(this, 'lower')}>
                <Ionicons name="md-remove" size={24} color="white" />
            </MainButton>
            <NumberContainer>{currentGuess}</NumberContainer>
            <MainButton onPress={nextGuessHandler.bind(this, 'greater')}>
                <Ionicons name="md-add" size={24} color="white" />
            </MainButton>
        </View>
    );
}
 
return (
    <View style={styles.screen}>
      <Text style={DefaultStyles.title}>Opponent's Guess</Text>
      {gameControls}
      <View style={listContainerStyle}>
        {/* <ScrollView contentContainerStyle={styles.list}>
          {pastGuesses.map((guess, index) => renderListItem(guess, pastGuesses.length - index))}
        </ScrollView> */}
        <FlatList
          keyExtractor={item => item}
          data={pastGuesses}
          renderItem={renderListItem.bind(this, pastGuesses.length)}
          contentContainerStyle={styles.list}
        />
      </View>
    </View>
);
This introduces a new gameControls variable that manages the part of the JSX code that does actually change. Using this code instead of the one shown in the video lectures is totally optional though!

GameOverScreen.js

This file doesn't use any listener, hence you need to add useState and useEffect.

import React, { useState, useEffect } from 'react;
... // other imports
 
const GameOverScreen = props => {
    const [availableDeviceWidth, setAvailableDeviceWidth] = useState(Dimensions.get('window').width);
    const [availableDeviceHeight, setAvailableDeviceHeight] = useState(Dimensions.get('window').height);
 
    useEffect(() => {
        const updateLayout = () => {
            setAvailableDeviceWidth(Dimensions.get('window').width);
            setAvailableDeviceHeight(Dimensions.get('window').height);
    };
 
    Dimensions.addEventListener('change', updateLayout);
 
    return () => {
            Dimensions.removeEventListener('change', updateLayout);
        };
    });
 
    return (
        <ScrollView>
            <View style={styles.screen}>
                <TitleText>The Game is Over!</TitleText>
                <View style={‌{...styles.imageContainer, ...{
                    width: availableDeviceWidth * 0.7,
                    height: availableDeviceWidth * 0.7,
                    borderRadius: (availableDeviceWidth * 0.7) / 2,
                    marginVertical: availableDeviceHeight / 30
                }}}>
                    <Image
                        source={require('../assets/success.png')}
                        style={styles.image}
                        resizeMode="cover"
                    />
                </View>
                <View style={‌{...styles.resultContainer, 
                        ...{marginVertical: availableDeviceHeight / 60}}}>
                    <BodyText style={‌{...styles.resultText, ...{
                            fontSize: availableDeviceHeight < 400 ? 16 : 20}}}>
                        Your phone needed{' '}
                        <Text style={styles.highlight}>{props.roundsNumber}</Text> rounds to
                            guess the number{' '}
                        <Text style={styles.highlight}>{props.userNumber}</Text>.
                    </BodyText>
                </View>
                <MainButton onPress={props.onRestart}>NEW GAME</MainButton>
            </View>
        </ScrollView>
    );
};
// ...
Also remove the styles you're now setting as inline styles from the StyleSheet at the bottom of the file.

Adding AppLoading
In the next lecture, we'll add the AppLoading component.

We will do this by importing it like this:

import { AppLoading } from 'expo';
This might fail for you - depending on the version of Expo you're using to follow along.

If it does fail, try this alternative way of adding it:

expo install expo-app-loading
import AppLoading from 'expo-app-loading';
Also add the following prop to the <AppLoading /> component (in your JSX code):

onError={(err) => console.log(err)}
In the end, you should have:

<AppLoading
    startAsync={fetchFonts}
    onFinish={() => setFontLoaded(true)}
    onError={(err) => console.log(err)}
/>

React Navigation Docs
In case you want to dive into the official docs as well (we'll go through the installation in the next lectures, together), you can find the official docs here: https://reactnavigation.org/docs/4.x/getting-started

MUST READ: Installing Different Navigators
DON'T SKIP THIS LECTURE - PLEASE READ TO BOTTOM!

---

If you're using React Navigation v4 or higher, everything works as shown in this module but there is one important difference: You need to install the different navigators which we'll use in this module (StackNavigator, DrawerNavigator, TabsNavigator) separately.

So when we use the StackNavigator (= next lecture), run

npm install --save react-navigation-stack
before you start using it (with v3 and lower, it was part of react-navigation itself).

Also add this import in the file where you are using createStackNavigator:

import { createStackNavigator } from 'react-navigation-stack';
Same for TabsNavigator (used a little bit later in this module):

npm install --save react-navigation-tabs
import { createBottomTabNavigator } from 'react-navigation-tabs';
And also for DrawerNavigator (also used later in this module):

npm install --save react-navigation-drawer
import { createDrawerNavigator } from 'react-navigation-drawer';

React Navigation & Code Attachments
You don't have to read this lecture - it's only relevant if you plan on running one of my code attachments!

Throughout the course, you find code attachments which you can use to compare your code to mine.

In case you want to run my attachments, make sure you follow these steps to use react-navigation v4 in them:

1) Run npm install and then expo upgrade

2) Install all extra navigators that are required for this specific code snapshot:

npm install --save react-navigation-stack

npm install --save react-navigation-tabs

npm install --save react-navigation-drawer

(of course you can combine that all into one npm install command if you need all of them)

3) Make sure you're using version 4 of react-navigation

npm install --save react-navigation@latest

4) Install all required dependencies

expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view

5) Update all "navigator" imports

import { createStackNavigator, createAppContainer } from 'react-navigation';

would become

import { createAppContainer } from 'react-navigation';
import { createStackNavigator } from 'react-navigation-stack';
for example. Do that for all navigators (e.g. tabs, drawer) you might be using in the specific snapshot.

And with that, the attachments should work.

I basically show all of that throughout the lectures - I'm just summing it up here so that you have a quick & easy go-to reference.

Alternative Navigation Syntax
The "navigate to new screen" syntax shown in the previous lecture (and throughout this module) is pretty explicit/ clear, that's why I chose it for this introduction to React Navigation.

But instead of

props.navigation.navigate({routeName: 'SomeIdentifier'});
you can also use

props.navigation.navigate('SomeIdentifier');
This alternative is of course a bit shorter, other than that, it has no advantage or disadvantages compared to the more explicit one.

Throughout the course, I'll use both alternatives.

Header Buttons: Using the Correct Version
In the next lecture, we'll add a package named "react-navigation-header-buttons".

In order to avoid errors, make sure you're using the correct version of that package => Version 6

You can install that via npm install --save react-navigation-header-buttons@6

(instead of just npm install --save react-navigation-header-buttons which I use in the next lecture)

navigationOptions inside of a Navigator
When defining a navigator, you can also add navigationOptions to it:

const SomeNavigator = createStackNavigator({
    ScreenIdentifier: SomeScreen
}, {
    navigationOptions: {
        // You can set options here!
        // Please note: This is NOT defaultNavigationOptions!
    }
});
Don't mistake this for the defaultNavigationOptions which you could also set there (i.e. in the second argument you pass to createWhateverNavigator()).

The navigationOptions you set on the navigator will NOT be used in its screens! That's the difference to defaultNavigationOptions - those option WILL be merged with the screens.

So what's the use of navigationOptions in that place then?

The options become important once you use the navigator itself as a screen in some other navigator - for example if you use some stack navigator (created via createStackNavigator()) in a tab navigator (e.g. created via createBottomTabNavigator()).

In such a case, the navigationOptions configure the "nested navigator" (which is used as a screen) for that "parent navigator". For example, you can use navigationOptions on the nested navigator that's used in a tab navigator to configure the tab icons.