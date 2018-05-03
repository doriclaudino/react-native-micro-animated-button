# react-native-micro-animated-button

[![npm version](https://badge.fury.io/js/react-native-micro-animated-button.svg)](https://badge.fury.io/js/react-native-micro-animated-button)

<img src="https://raw.githubusercontent.com/sonaye/react-native-micro-animated-button/master/demo.gif" width="400">

# Installation

`yarn add react-native-vector-icons react-native-micro-animated-button`

`react-native-vector-icons` may require native linking, see package [repository](https://github.com/oblador/react-native-vector-icons) for more details (not needed if using Expo).

# Definition

```javascript
type button = {
  activeOpacity?: number,
  backgroundColor?: string,         // default = white
  bounce?: boolean,                 // default = false
  disabled?: boolean,               // default = false
  disabledBackgroundColor: string,  // default = gray
  disabledForegroundColor: string,  // default = white
  errorBackgroundColor: string,     // default = red
  errorForegroundColor?: string,    // default = white
  errorIcon: string,
  errorLabel: string,
  expandOnFinish?: boolean,         // default = false
  foregroundColor?: string,         // default = blue
  icon?: string,                    // default = icons names from FontAwesome
  iconSet? any,                     // default = FontAwesome
  iconSize?: number,                // default = 17
  iconStyle?: Object,
  initialState?: string,            // default = null, can have values ['success', 'error', 'loading']
  label: string,
  labelStyle?: Object,              // default = defaultLabelStyle
  maxWidth?: number,                // default = 240
  minWidth?: number,                // default = 40
  width?: number,                   // default = 240, overwrites maxWidth and minWidth, use for fixed length
  noFill?: boolean,                 // default = false
  noRadius?: boolean,               // default = false
  onError?: Function,               // default = () => null
  onLoad?: Function,                // default = () => null
  onPress?: Function,               // default = () => null
  onReset?: Function,               // default = () => null
  onSecondaryPress?: Function,      // default = () => null
  onSuccess?: Function,             // default = () => null
  renderErrorIcon?: any,            // default = <FontAwesome />
  renderIndicator?: any,            // default = <ActivityIndicator />
  renderLabel?: any,                // default = <Text />
  renderSuccessIcon?: any,          // default = <FontAwesome />
  scaleFactor?: number,             // default = 1.1
  scaleOnSuccess?: boolean,         // default = false
  shakeOnError?: boolean,           // default = false
  static?: boolean,                 // default = false
  style?: Object,                   // default = defaultStyle
  successBackgroundColor?: string,  // default = green
  successForegroundColor?: string   // default = white
  successIcon: string,
  successLabel: string,
};

const defaultStyle = {
  alignItems: 'center',
  borderRadius: 40 / 2,
  borderWidth: 1,
  height: 40,
  justifyContent: 'center',
  marginVertical: 10
};

const defaultLabelStyle = {
  backgroundColor: 'transparent',
  padding: 10
};

// methods
button.error();   // Animates button to error state
button.load();    // Animates button to loading state
button.reset();   // Animates button to initial/default state
button.success(); // Animates button to success state
```

## Examples

```javascript
import React, { PureComponent } from 'react';
import { Platform, ScrollView, StatusBar, Text, View } from 'react-native';

import Btn from 'react-native-micro-animated-button';

StatusBar.setHidden(true, 'fade');

const colors =
  Platform.OS === 'ios'
    ? {
        blue: '#007aff',
        gray: '#d8d8d8',
        green: '#4cd964',
        red: '#ff3b30',
        white: '#ffffff'
      }
    : {
        blue: '#4285f4',
        gray: '#d8d8d8',
        green: '#0f9d58',
        red: '#db4437',
        white: '#ffffff'
      };

const Example1 = () => (
  <View style={styles.center}>
    <Btn
      foregroundColor={colors.green}
      label="Submit"
      onPress={() => this.b1.success()}
      ref={ref => (this.b1 = ref)}
      successIcon="check"
    />

    <Btn
      foregroundColor={colors.blue}
      label="Retweet"
      onPress={() => this.b2.success()}
      ref={ref => (this.b2 = ref)}
      successIcon="retweet"
    />

    <Btn
      foregroundColor={colors.red}
      label="Favorite"
      onPress={() => this.b3.success()}
      ref={ref => (this.b3 = ref)}
      successIcon="heart"
    />
  </View>
);

const Example2 = () => (
  <View style={styles.center}>
    <Btn
      errorBackgroundColor={colors.red}
      errorIcon="thumbs-down"
      expandOnFinish
      foregroundColor={colors.blue}
      label="Am I even?"
      onPress={() =>
        new Date().getSeconds() % 2 === 0 ? this.b4.success() : this.b4.error()
      }
      ref={ref => (this.b4 = ref)}
      successBackgroundColor={colors.green}
      successIcon="thumbs-up"
      width={240}
    />

    <Btn
      errorBackgroundColor={colors.red}
      errorIcon="thumbs-down"
      expandOnFinish
      foregroundColor={colors.blue}
      label="Am I even?"
      onPress={() =>
        new Date().getSeconds() % 2 === 0 ? this.b5.success() : this.b5.error()
      }
      ref={ref => (this.b5 = ref)}
      successBackgroundColor={colors.green}
      successIcon="thumbs-up"
      width={240}
    />
  </View>
);

const Example3 = () => (
  <View style={styles.center}>
    <Btn
      backgroundColor={colors.blue}
      errorBackgroundColor={colors.red}
      errorForegroundColor={colors.white}
      errorIcon="warning"
      foregroundColor={colors.white}
      label="Simulate an error"
      onPress={() => this.b6.error()}
      ref={ref => (this.b6 = ref)}
      shakeOnError
      width={240}
    />

    <Btn
      backgroundColor={colors.blue}
      foregroundColor={colors.white}
      label="Smile at me"
      onPress={() => this.b7.success()}
      ref={ref => (this.b7 = ref)}
      scaleOnSuccess
      successBackgroundColor={colors.green}
      successForegroundColor={colors.white}
      successIcon="smile-o"
      width={240}
    />
  </View>
);

class Example4 extends PureComponent {
  state = { disabled: true };

  onPress = () => this.setState({ disabled: !this.state.disabled });

  render() {
    return (
      <View style={styles.center}>
        <Btn
          backgroundColor={colors.blue}
          foregroundColor={colors.white}
          label="Static Button"
          noRadius
          onPress={this.onPress}
          static
        />

        <Btn
          disabled={this.state.disabled}
          label="Disabled Button"
          noRadius
          static
        />
      </View>
    );
  }
}

class Example5 extends PureComponent {
  state = { clicked: false };

  onPress = () => this.setState({ clicked: true }, () => this.b8.success());

  onSecondaryPress = () =>
    this.setState({ clicked: false }, () => this.b8.reset());

  render() {
    return (
      <View style={styles.row}>
        <Btn
          foregroundColor={colors.blue}
          icon="cloud-download"
          noFill
          onPress={this.onPress}
          onSecondaryPress={this.onSecondaryPress}
          ref={ref => (this.b8 = ref)}
          successBackgroundColor={colors.blue}
          successIcon="remove"
        />

        {this.state.clicked && (
          <Text style={styles.rightText}>I just got downloaded</Text>
        )}
      </View>
    );
  }
}

const Examples = () => (
  <ScrollView contentContainerStyle={styles.full}>
    <Example1 />
    <Example2 />
    <Example3 />
    <Example4 />
    <Example5 />
  </ScrollView>
);

const styles = {
  center: { alignItems: 'center' },
  full: { flex: 1 },
  rightText: { color: colors.blue, marginLeft: 10 },
  row: { alignItems: 'center', flexDirection: 'row', justifyContent: 'center' }
};

export default Examples;
```
