# React Native Panorama

> The react-native-panorama library is a direct continuation of the [@lightbase/react-native-panorama-view module](https://github.com/lightbasenl/react-native-panorama-view). It's a way of continue the panoramic view integration in React Native since @lightbase/react-native-panorama-view has no more updates. 

<img src="./github/preview.gif" />

## Mostly automatic installation (RN >= 0.60)

`$ yarn add @dsdev/react-native-panorama`

`$ cd ios && pod install`


## Usage

You can size your panorama anyway you'd like using the regular `View` styles.

NOTE: On android, you need to make sure the View renders at least a few pixels (not invisible / display:
none). Otherwise, the VR viewer won't fire events. You may use `onImageDownloaded` to lazy load the VR
renderer instead.

Here are some examples:

### Embed a panorama as a part of your screen

```tsx
import PanoramaView from "@dsdev/react-native-panorama";

const PanoramaDetails = () => (
  <View style={styles.container}>
    <PanoramaView
      style={styles.viewer}
      dimensions={{ height: 230, width: Dimensions.get("window").width }}
      inputType="mono"
      imageUrl="https://raw.githubusercontent.com/googlevr/gvr-android-sdk/master/assets/panoramas/testRoom1_2kMono.jpg"
    />
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  viewer: {
    height: 230,
  },
});
```

### Fullscreen panorama

```tsx
import PanoramaView from "@dsdev/react-native-panorama";

const FullScreenPanorama = () => (
  <PanoramaView
    style={{ flex: 1 }}
    dimensions={{
      height: Dimensions.get("window").height,
      width: Dimensions.get("window").width,
    }}
    inputType="mono"
    imageUrl="https://raw.githubusercontent.com/googlevr/gvr-android-sdk/master/assets/panoramas/testRoom1_2kMono.jpg"
  />
);
```

## Props

| Name                 | Type                                | Description                                                                                               |
| -------------------- | ----------------------------------- | --------------------------------------------------------------------------------------------------------- |
| imageUrl             | string                              | Remote or local URI for fetching the panorama image.                                                      |
| enableTouchTracking  | boolean                             | Enables dragging the panorama by touch when `true`.                                                       |
| onImageLoadingFailed | callback                            | Fired when something goes wrong while trying to load the panorama.                                        |
| onImageDownloaded    | callback                            | Fired when the image was successfully downloaded. This will fire before onImageLoaded                     |
| onImageLoaded        | callback                            | Fired when the image was successfully loaded.                                                             |
| style                | ViewStyle                           | Allows to style the `PanoramaView` like a regular `View`.                                                 |
| inputType            | 'mono' or 'stereo'                  | Specify the type of panorama source image. **Android only**                                               |
| dimensions           | `{ height: number, width: number }` | Is used to prevent loading unnecessarily large files into memory. **Currently required for Android only** |
