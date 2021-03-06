
# ios_snippets

## Bamboo setting to build and test

### Prerequisites
- Install [Fastlane](https://github.com/fastlane/fastlane)
  ```
  sudo gem install fastlane --verbose  
  sudo gem install scan
  ```
  
### Plan configuration:

- variables:
  - clean = yes
  - configuration = debug
  - project =
  - release = 1
  - scheme = C24Hhv-Example
  - workspace = Example/c24hhv.xcworkspace

### Define steps for plan

- Checkout source code into ```src``` directory

- pod install task
  ```
  export PATH=/usr/local/opt/ruby/bin:/usr/local/bin:$PATH
  
  export LANG=en_US.UTF-8
  export LANGUAGE=en_US.UTF-8
  export LC_ALL=en_US.UTF-8
  
  pod install
  ```
- Erase simulator data
  ```
  instruments -s devices \
  | grep iPhone \
  | grep -o "[0-9A-F]\{8\}-[0-9A-F]\{4\}-[0-9A-F]\{4\}-[0-9A-F]\{4\}-[0-9A-F]\{12\}" \
  | while read -r line ; do
  echo "Reseting Simulator with UDID: $line"
  xcrun simctl erase $line
  done
  ```
- Build and test with fastlane
  ```
  #set -o errexit
  set -o nounset
  set -o xtrace
  
  PATH="$PATH:/usr/local/bin"
  
  PROJECT=""
  if [ -n "${bamboo_project}" ]; then
      PROJECT="--project ${bamboo_project}"
  fi
  
  WORKSPACE=""
  if [ -n "${bamboo_workspace}" ]; then
      WORKSPACE="--workspace ./${bamboo_workspace}"
  fi
  
  SCHEME=""
  if [ -n "${bamboo_scheme}" ]; then
      SCHEME="--scheme ${bamboo_scheme}"
  fi
  
  TARGET=""
  if [ -z "${bamboo_scheme}" ]; then
      # SCHEME
      #-alltargets
      #-target TARGET
      #TARGET="-target ${bamboo_target}"
      TARGET=""
  fi
  
  CONFIGURATION=""
  if [ -n "${bamboo_configuration}" ]; then
      CONFIGURATION="--configuration ${bamboo_configuration}"
  fi
  
  # kill any running simulator
  osascript -e 'tell app "Simulator" to quit'
  
  rm -rf ../test-reports > /dev/null 2>&1
  rm -rf ../logs/scan > /dev/null 2>&1
  
  open -a /Applications/Xcode.app/Contents/Developer/Applications/Simulator.app/
  
  scan \
      $WORKSPACE \
      $SCHEME \
      --buildlog_path ../logs/scan \
      --output_directory ../test-reports \
      --device "iPhone 6"\
      --xcargs "-derivedDataPath ../build" \
      --clean 
  # xcodebuild $WORKSPACE $SCHEME -destination 'platform=iOS Simulator,name=iPhone 6' test | xcpretty
  
  mv ../test-reports/report.junit ../test-reports/report.xml
  ```

- JUnit Parser
- Kill simulator after build
  ```
  set -o errexit
  set -o nounset
  set -o xtrace

  osascript -e 'tell app "Simulator" to quit'
  ```

### Calabash integration with bamboo
- Add device uuid variable to plan: ```device_uuid = your device id```
- Add 'Run tests step' with following script:
  ```
  export PATH=/usr/local/opt/ruby/bin:/usr/local/bin:$PATH

  export LANG=en_US.UTF-8
  export LANGUAGE=en_US.UTF-8
  export LC_ALL=en_US.UTF-8

  DEVICE_TARGET=$bamboo_device_uuid cucumber --tags @landing
  ```
