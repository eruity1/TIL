# Unknown ruby interpreter version
When you create a new React Native app you will have the following option:
`Do you want to install CocoaPods now?`
Now I will admit despite working with Ruby on Rails in my job, I don't know what this is, maybe I will have a md explianing that at some point, but probably not. 

Okay I did some research and found this
* React Native’s iOS dependencies use CocoaPods for managing native libraries
* Without CocoaPods, the native modules won’t link correctly on iOS
* Most React Native libraries with native code require CocoaPods to work on iOS

Anyways after creating my new react-native project and opening it up in a terminal I see this:
```bash
RVM used your Gemfile for selecting Ruby, it is all fine - Heroku does that too,
you can ignore these warnings with 'rvm rvmrc warning ignore /Users/ethanruitenberg/Documents/projects/BarCrawlApp/Gemfile'.
To ignore the warning for all files run 'rvm rvmrc warning ignore allGemfiles'.

Unknown ruby interpreter version (do not know how to handle): >=2.6.10.
```

Great another error when trying to start a project. But not to worry this isn't going to affect your development it is just a warning. But it is a very easy fix, you just need to update your Ruby version manager or Ruby interpreter to one that understands this version syntax.
```bash
rvm get stable
```