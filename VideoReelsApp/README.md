# VideoGram - Instagram Reels Style Android App

A full-featured Android application built in Java that mimics Instagram Reels/YouTube Shorts style video playback with an integrated reward system.

## Features

### 🎥 Video Playback
- **Fullscreen vertical video feed** with smooth scrolling
- **ExoPlayer integration** for optimized video playback
- **Infinite scroll** using ViewPager2 for seamless user experience
- **Auto-play and loop** functionality
- **Dynamic video loading** from REST API

### 🏆 Reward System
- **Points accumulation** - Earn 10 points for each completed video
- **Local storage** using SharedPreferences for data persistence
- **Reward tracking** - Total points and videos watched statistics
- **Reward history screen** with detailed statistics
- **Reset/Redeem functionality** with confirmation dialogs

### 🎨 Modern UI/UX
- **Material Design 3** components and styling
- **Immersive fullscreen mode** for distraction-free viewing
- **Smooth animations** and transitions between screens
- **Responsive design** optimized for all screen sizes
- **Clean, minimalist interface** focusing on content

### 🔧 Technical Features
- **MVVM Architecture** with clean separation of concerns
- **Retrofit integration** for REST API calls with fallback support
- **Error handling** and network connectivity management
- **Memory optimization** for smooth video playback
- **Lifecycle-aware components** for proper resource management

## Project Structure

```
VideoReelsApp/
├── app/
│   ├── src/main/
│   │   ├── java/com/example/videoreels/
│   │   │   ├── activities/          # UI Activities
│   │   │   │   ├── SplashActivity.java
│   │   │   │   ├── MainActivity.java
│   │   │   │   └── RewardHistoryActivity.java
│   │   │   ├── adapters/            # RecyclerView Adapters
│   │   │   │   └── VideoAdapter.java
│   │   │   ├── models/              # Data Models
│   │   │   │   └── VideoModel.java
│   │   │   ├── network/             # API Handling
│   │   │   │   └── APIHandler.java
│   │   │   ├── utilities/           # Utility Classes
│   │   │   │   └── RewardManager.java
│   │   │   └── viewmodel/           # MVVM ViewModels (Optional)
│   │   ├── res/
│   │   │   ├── layout/              # XML Layouts
│   │   │   ├── values/              # Colors, Strings, Themes
│   │   │   ├── anim/                # Animation Resources
│   │   │   └── xml/                 # Configuration Files
│   │   └── AndroidManifest.xml
│   ├── build.gradle                 # App-level Gradle config
│   └── proguard-rules.pro          # ProGuard configuration
├── gradle/wrapper/                  # Gradle Wrapper
├── build.gradle                     # Project-level Gradle config
├── settings.gradle                  # Gradle settings
├── gradle.properties               # Gradle properties
└── README.md                       # This file
```

## API Integration

The app fetches video data from: `https://videogram.ipoupdates.com/getdata.php`

### Expected API Response Format:
```json
[
  {
    "id": 1,
    "videoUrl": "https://example.com/video1.mp4"
  },
  {
    "id": 2,
    "videoUrl": "https://example.com/video2.mp4"
  }
]
```

### Fallback Support
If the API is unavailable, the app includes mock video data with sample MP4 URLs for testing purposes.

## Requirements

- **Minimum SDK**: 21 (Android 5.0)
- **Target SDK**: 34 (Android 14)
- **Language**: Java
- **Architecture**: MVVM with clean modular code

## Dependencies

### Core Android Libraries
- AndroidX AppCompat
- Material Design Components
- ConstraintLayout
- RecyclerView
- ViewPager2

### Video Playback
- ExoPlayer 2.19.1

### Networking
- Retrofit 2.9.0
- Gson Converter

### Lifecycle Management
- AndroidX Lifecycle Extensions

## Installation & Setup

1. **Clone or download** the project
2. **Open in Android Studio**
3. **Sync Gradle** files
4. **Build and run** on device or emulator

### Build Commands
```bash
# Debug build
./gradlew assembleDebug

# Release build
./gradlew assembleRelease

# Install on connected device
./gradlew installDebug
```

## Usage

### Main Features

1. **Video Feed**
   - Swipe up/down to navigate between videos
   - Videos auto-play and loop
   - Reward points displayed in top-right corner

2. **Reward System**
   - Watch videos completely to earn points
   - Tap floating action button to view reward history
   - Reset/redeem points from reward history screen

3. **Navigation**
   - Splash screen on app launch
   - Smooth transitions between screens
   - Back button confirmation on main screen

## Code Highlights

### Video Playback Management
```java
// ExoPlayer setup with lifecycle management
private void setupExoPlayer(VideoModel video, int position) {
    exoPlayer = new ExoPlayer.Builder(context).build();
    playerView.setPlayer(exoPlayer);
    MediaItem mediaItem = MediaItem.fromUri(Uri.parse(video.getVideoUrl()));
    exoPlayer.setMediaItem(mediaItem);
    exoPlayer.prepare();
    exoPlayer.setRepeatMode(Player.REPEAT_MODE_ONE);
}
```

### Reward Management
```java
// Award points for video completion
public void awardVideoCompletionPoints() {
    addPoints(DEFAULT_POINTS_PER_VIDEO);
    incrementVideosWatched();
}
```

### API Integration
```java
// Retrofit API call with fallback
apiHandler.getVideosWithFallback(new APIHandler.ApiCallback<List<VideoModel>>() {
    @Override
    public void onSuccess(List<VideoModel> videos) {
        // Update UI with video data
    }
    
    @Override
    public void onError(String errorMessage) {
        // Handle error or use mock data
    }
}, true);
```

## Performance Optimizations

- **Memory Management**: Proper ExoPlayer release in ViewHolder recycling
- **Network Efficiency**: Retrofit with OkHttp for optimized API calls
- **UI Responsiveness**: Background threading for API calls and data processing
- **Battery Optimization**: Pause video playback when app is not in focus

## Testing

The app includes comprehensive error handling and fallback mechanisms:

- **Network connectivity** checks
- **API failure** handling with mock data
- **Video loading** error management
- **Memory leak** prevention
- **Lifecycle** state management

## Future Enhancements

- [ ] Video caching for offline playback
- [ ] Social features (likes, comments, sharing)
- [ ] User profiles and authentication
- [ ] Advanced reward system with different point values
- [ ] Video upload functionality
- [ ] Push notifications for new content

## License

This project is created for educational and demonstration purposes.

## Support

For issues or questions, please refer to the code comments and documentation within the source files.

---

**Built with ❤️ using Android Studio and Java**
