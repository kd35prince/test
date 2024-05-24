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
