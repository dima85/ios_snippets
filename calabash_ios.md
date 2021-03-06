# Calabash
### [Setup calabash for IOS](https://github.com/calabash/calabash-ios/wiki/calabash-ios-setup#setup-fast-track) 


If it doesn't work in your project, see one of the tutorials mentioned on the Tutorial: [How to add Calabash to Xcode page](https://github.com/calabash/calabash-ios/wiki/Tutorial%3A-How-to-add-Calabash-to-Xcode).

- In a terminal, go to your iOS project
  
  ```cd path-to-my-ios-project``` (i.e. directory containing .xcodeproj file)

- Install calabash-cucumber gem (this make take some time because of dependencies)
  
  ```gem install calabash-cucumber```

- **Setup your project for Calabash-iOS.**
  
  ```calabash-ios setup``` -  Answer the questions and read the output :)
  
- Generate a skeleton features folder for your tests
  
  ```calabash-ios gen```

- In Xcode, build your project using the ```-cal``` scheme

- To run all tests, in terminal run:  ```cucumber```
 
- To run tests with specific device and tags: ```DEVICE_TARGET=device_uuid cucumber --tags @tag_name``` (```--tags ~@tag_name``` to exclude tests with tag)

If all goes well, you are now ready to write your first test. Start by editing the file features/my_first.feature.

# Calabash usage
- [Geting started](https://github.com/calabash/calabash-ios/wiki/Getting-Started)
  - run debug console for calabash: ```calabash-ios console```

  - If doesn't run your application, run this command in calabash console: ```start_test_server_in_background```

- [Query language](https://github.com/calabash/calabash-ios/wiki/Query-Language):

  - ```query("button")``` - get all button in screen
  
  - ```query("button index:0 label")``` - get labels that is child of firt button 
  
  - ```query("view marked:'switch'")``` - get views that has accessibility label 'switch'
   
  - To wait for element to apear, use: ```wait_for_element_exists("webView marked:'hello'")```
  
  - There are a lot of [predefined steps](https://github.com/calabash/calabash-ios/wiki/02-Predefined-steps) 

- [WebView support](https://github.com/calabash/calabash-ios/wiki/06-WebView-Support#marked-api)
 
  - prefix query with ```webView```
  - you can use css, xpath or text selectors
  
    - ```query("webView css:'input[placeholder=hello]'")``` - css
    
    - ```query("webView marked:'some text'")``` - text
