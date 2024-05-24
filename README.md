# test
just for study


import React from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  View,
  Text
} from 'react-native';
import * as exampleByName from './examples';
import ProcessExample from './examples/entries/ProgressViewDemo'
import ProcessAndroidExample from './examples/ProgressBarAndroidDemo'
import GeolocationDemo from './examples/GeolocationTest';
import ScrollableTabviewDemo from './examples/ScrollableTabview'
// import SnapCarouselExample from './examples/SnapCarouselExample'
import { NavigationContainer, Page } from './components';
import { Benchmarker, DeepTree, SierpinskiTriangle } from './benchmarks';
import { PortalHost, PortalProvider } from '@gorhom/portal';
import ReactNativeAnimatableDemo from './examples/reactNativeAnimatable/App'

function App() {
  return (
    <View style={{ backgroundColor: '#F0FFF0' }}>
      <StatusBar barStyle="light-content" />
      <SafeAreaView>
        <NavigationContainer>
          <PortalProvider>
            <Page name='ProcessAndroidExample'><ProcessAndroidExample></ProcessAndroidExample></Page>
            <Page name='ProcessExample'><ProcessExample></ProcessExample></Page>
            <Page name='GeolocationDemo'><GeolocationDemo></GeolocationDemo></Page>
            <Page name='ScrollableTabviewDemo'><ScrollableTabviewDemo></ScrollableTabviewDemo></Page>
            <Page name = 'ReactNativeAnimatableDemo'><ReactNativeAnimatableDemo></ReactNativeAnimatableDemo></Page>
            {/* <Page name = 'RnFastImgDemo'><RnFastImgDemo></RnFastImgDemo></Page> */}
            {/* <Page name='SnapCarouselExample'><SnapCarouselExample></SnapCarouselExample></Page> */}
          </PortalProvider>
        </NavigationContainer>
      </SafeAreaView>
    </View>

  );
}

export default App;


import { useState, useRef, useCallback } from 'react';
import { TouchableOpacity, ScrollView } from 'react-native';
import * as Animatable from 'react-native-animatable';
import { Tester, Filter, TestCase, TestSuite } from '@rnoh/testerino';

export default function ExampleView() {
    const [textFontSize, setTextFontSize] = useState(10);

    return (
        <Tester style={{
            display: 'flex',
            flexDirection: 'column'
        }}>
            <ScrollView>
                <TestCase itShould="SimpleMask">
                    <Animatable.View style={{ padding: 50, backgroundColor: '#333333' }}>
                        <Animatable.Text
                            animation="slideInDown"
                            iterationCount={5}
                            direction="reverse"
                            style={{ color: 'white', textAlign: 'center' }}
                            duration={2000}
                            onAnimationBegin={() => { console.log('test onAnimationBegin') }}
                            onAnimationEnd={() => { console.log('test onAnimationEnd') }}
                        >Up and down you go</Animatable.Text>
                        <Animatable.Text animation="bounce" easing="ease-out" iterationCount="infinite" iterationDelay={1500} style={{ textAlign: 'center' }} useNativeDriver={true} isInteraction={true}>❤️</Animatable.Text>
                        <Animatable.Text animation="fadeIn" delay={2000} style={{ textAlign: 'center', marginTop: 50, color: 'white' }}>(*^▽^*)</Animatable.Text>
                        <TouchableOpacity onPress={() => setTextFontSize(textFontSize + 5)}>
                            <Animatable.Text
                                transition="fontSize"
                                style={{ textAlign: 'center', marginTop: 50, color: 'white', fontSize: textFontSize || 10 }}
                                onTransitionBegin={() => { console.log('test onTransitionBegin') }}
                                onTransitionEnd={() => { console.log('test onTransitionEnd') }}
                            >O(∩_∩)O哈哈~</Animatable.Text>
                        </TouchableOpacity>
                    </Animatable.View>
                </TestCase>

            </ScrollView>
        </Tester>


    )
}   

app.tsx
import React, { useCallback } from 'react';
import {
  Button,
  TextInput,
  SafeAreaView,
  SectionList,
  StyleSheet,
  TouchableWithoutFeedback,
  ScrollView
} from 'react-native';
import { View, Text, Animation } from 'react-native-animatable';
import Slider from '@react-native-community/slider';
import AnimationCell from './AnimationCell';
import { animationTypes } from './groupedAnimationTypes';
import { Tester, Filter, TestCase, TestSuite } from '@rnoh/testerino';

const COLORS = [
  '#65b237', // green
  '#346ca5', // blue
  '#a0a0a0', // light grey
  '#ffc508', // yellow
  '#217983', // cobolt
  '#435056', // grey
  '#b23751', // red
  '#333333', // dark
  '#ff6821', // orange
  '#e3a09e', // pink
  '#1abc9c', // turquoise
  '#302614', // brown
];

const NATIVE_INCOMPATIBLE_ANIMATIONS = [
  'jello',
  'lightSpeedIn',
  'lightSpeedOut',
];

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5FCFF',
  },
  title: {
    fontSize: 28,
    fontWeight: '300',
    textAlign: 'center',
    margin: 20,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 20,
    backgroundColor: 'transparent',
  },
  slider: {
    height: 30,
    margin: 10,
  },
  toggle: {
    width: 120,
    backgroundColor: '#333',
    borderRadius: 3,
    padding: 5,
    fontSize: 14,
    alignSelf: 'center',
    textAlign: 'center',
    margin: 10,
    color: 'rgba(255, 255, 255, 1)',
  },
  toggledOn: {
    color: 'rgba(255, 33, 33, 1)',
    fontSize: 16,
    transform: [
      {
        rotate: '8deg',
      },
      {
        translateY: -20,
      },
    ],
  },
  sectionHeader: {
    backgroundColor: '#F5FCFF',
    padding: 15,
  },
  sectionHeaderText: {
    textAlign: 'center',
    fontSize: 18,
  },
});

export default function App() {
  const [duration, setDuration] = React.useState(1000);
  console.log(duration)
  const [toggledOn, setToggledOn] = React.useState(false);
  const textRef = React.useRef<Text>(null);

  const handleRowPressed = useCallback(
    (componentRef: typeof View, animationType: Animation) => {
      componentRef.animate(animationType, duration);
      textRef.current?.animate(animationType, duration);
    },
    [duration],
  );

  return (
    <View style={styles.container}>
      <View style={styles.slider}>
        <Button title='点我一下' onPress={() => { setDuration(Math.round(Math.floor(Math.random() * 1000) + 1)) }}></Button>
      </View>

      <TouchableWithoutFeedback onPress={() => setToggledOn(prev => !prev)}>
        <Text
          style={[styles.toggle, toggledOn && styles.toggledOn]}
          transition={['color', 'rotate', 'fontSize']}>
          Toggle me!
        </Text>
      </TouchableWithoutFeedback>
      <Text animation="zoomInDown" delay={700} style={styles.instructions}>
        Tap one of the following to animate for {duration} ms
      </Text>
      <Tester style={{
        display: 'flex',
        flexDirection: 'column'
      }}>
        <ScrollView>
          <TestCase itShould="SimpleMask">
            <View
              animation="bounceInUp"
              duration={1100}
              delay={1400}
              style={styles.container}>
              <SectionList
                contentInsetAdjustmentBehavior="automatic"
                keyExtractor={item => item}
                sections={animationTypes}
                removeClippedSubviews={false}
                renderSectionHeader={({ section }) => (
                  <View style={styles.sectionHeader}>
                    <Text style={styles.sectionHeaderText}>{section.title}</Text>
                  </View>
                )}
                renderItem={({ item, index }) => (
                  <AnimationCell
                    animationType={item}
                    color={COLORS[index % COLORS.length]}
                    onPress={handleRowPressed}
                    useNativeDriver={
                      NATIVE_INCOMPATIBLE_ANIMATIONS.indexOf(item) === -1
                    }
                  />
                )}
              />
            </View>
          </TestCase>
        </ScrollView>
      </Tester>

    </View>
  );
}

app.json

{
  "name": "AnimatableExplorer",
  "displayName": "AnimatableExplorer"
}

react-native-animatable.d.ts

export type Animation =
  | 'bounce'
  | 'flash'
  | 'jello'
  | 'pulse'
  | 'rotate'
  | 'rubberBand'
  | 'shake'
  | 'swing'
  | 'tada'
  | 'wobble'
  | 'bounceIn'
  | 'bounceInDown'
  | 'bounceInUp'
  | 'bounceInLeft'
  | 'bounceInRight'
  | 'bounceOut'
  | 'bounceOutDown'
  | 'bounceOutUp'
  | 'bounceOutLeft'
  | 'bounceOutRight'
  | 'fadeIn'
  | 'fadeInDown'
  | 'fadeInDownBig'
  | 'fadeInUp'
  | 'fadeInUpBig'
  | 'fadeInLeft'
  | 'fadeInLeftBig'
  | 'fadeInRight'
  | 'fadeInRightBig'
  | 'fadeOut'
  | 'fadeOutDown'
  | 'fadeOutDownBig'
  | 'fadeOutUp'
  | 'fadeOutUpBig'
  | 'fadeOutLeft'
  | 'fadeOutLeftBig'
  | 'fadeOutRight'
  | 'fadeOutRightBig'
  | 'flipInX'
  | 'flipInY'
  | 'flipOutX'
  | 'flipOutY'
  | 'lightSpeedIn'
  | 'lightSpeedOut'
  | 'slideInDown'
  | 'slideInUp'
  | 'slideInLeft'
  | 'slideInRight'
  | 'slideOutDown'
  | 'slideOutUp'
  | 'slideOutLeft'
  | 'slideOutRight'
  | 'zoomIn'
  | 'zoomInDown'
  | 'zoomInUp'
  | 'zoomInLeft'
  | 'zoomInRight'
  | 'zoomOut'
  | 'zoomOutDown'
  | 'zoomOutUp'
  | 'zoomOutLeft'
  | 'zoomOutRight';

groupedAnimationTypes.ts

import {Animation} from 'react-native-animatable';

interface GroupedAnimationType {
  title: string;
  data: Animation[];
}
export const animationTypes: GroupedAnimationType[] = [
  {
    title: 'Attention Seekers',
    data: [
      'bounce',
      'flash',
      'jello',
      'pulse',
      'rotate',
      'rubberBand',
      'shake',
      'swing',
      'tada',
      'wobble',
    ],
  },
  {
    title: 'Bouncing Entrances',
    data: [
      'bounceIn',
      'bounceInDown',
      'bounceInUp',
      'bounceInLeft',
      'bounceInRight',
    ],
  },
  {
    title: 'Bouncing Exits',
    data: [
      'bounceOut',
      'bounceOutDown',
      'bounceOutUp',
      'bounceOutLeft',
      'bounceOutRight',
    ],
  },
  {
    title: 'Fading Entrances',
    data: [
      'fadeIn',
      'fadeInDown',
      'fadeInDownBig',
      'fadeInUp',
      'fadeInUpBig',
      'fadeInLeft',
      'fadeInLeftBig',
      'fadeInRight',
      'fadeInRightBig',
    ],
  },
  {
    title: 'Fading Exits',
    data: [
      'fadeOut',
      'fadeOutDown',
      'fadeOutDownBig',
      'fadeOutUp',
      'fadeOutUpBig',
      'fadeOutLeft',
      'fadeOutLeftBig',
      'fadeOutRight',
      'fadeOutRightBig',
    ],
  },
  {
    title: 'Flippers',
    data: ['flipInX', 'flipInY', 'flipOutX', 'flipOutY'],
  },
  {
    title: 'Lightspeed',
    data: ['lightSpeedIn', 'lightSpeedOut'],
  },
  {
    title: 'Sliding Entrances',
    data: ['slideInDown', 'slideInUp', 'slideInLeft', 'slideInRight'],
  },
  {
    title: 'Sliding Exits',
    data: ['slideOutDown', 'slideOutUp', 'slideOutLeft', 'slideOutRight'],
  },
  {
    title: 'Zooming Entrances',
    data: ['zoomIn', 'zoomInDown', 'zoomInUp', 'zoomInLeft', 'zoomInRight'],
  },
  {
    title: 'Zooming Exits',
    data: [
      'zoomOut',
      'zoomOutDown',
      'zoomOutUp',
      'zoomOutLeft',
      'zoomOutRight',
    ],
  },
];

AnimationCell.tsx

import React, {memo, useCallback, useRef} from 'react';
import {StyleSheet, Text, TouchableWithoutFeedback} from 'react-native';
import {Animation, View} from 'react-native-animatable';

const styles = StyleSheet.create({
  cell: {
    padding: 16,
    marginBottom: 10,
    marginHorizontal: 10,
  },
  name: {
    color: 'white',
    fontSize: 16,
    textAlign: 'center',
  },
});

interface AnimationCellProps {
  animationType: Animation;
  color: string;
  onPress: (view: View, animationType: Animation) => void;
  useNativeDriver: boolean;
}

export default memo(function AnimationCell({
  useNativeDriver,
  color,
  onPress,
  animationType,
}: AnimationCellProps) {
  const ref = useRef<View>(null);
  const handlePress = useCallback(() => {
    if (ref.current && onPress) {
      onPress(ref.current, animationType);
    }
  }, [ref, onPress, animationType]);

  return (
    <TouchableWithoutFeedback onPress={handlePress}>
      <View
        ref={ref}
        style={[{backgroundColor: color}, styles.cell]}
        useNativeDriver={useNativeDriver}>
        <Text style={styles.name}>{animationType}</Text>
      </View>
    </TouchableWithoutFeedback>
  );
});


