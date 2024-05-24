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
