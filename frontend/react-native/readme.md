## Run instructions for iOS:
    change working directory to ios folder

    ### Install Cocoapods
      bundle install # you need to run this only once in your project.
      bundle exec pod install
      cd ..
    
    ### npx react-native run-ios
        Open kitchenChamberMobile/ios/kitchenChamberMobile.xcodeproj in Xcode or run "xed -b ios"
        Hit the Run button

### Check available simulator names:
    Open terminal and execute below command will list all available devices name
    xcrun simctl list devices

    Then you can run the simulator with specific device name:
    npm run ios -- --simulator="iPhone 14 Pro (16.0)"

