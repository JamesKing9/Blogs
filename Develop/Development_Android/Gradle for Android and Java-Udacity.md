

# 3.  Why Gradle 

For example, for Gradle users, the process that executes the modern IDs, like Android Studio, or CI front end products like Jenkins, is all defining Gradle. In this day and age, an app store Android developer unable to ship changes into production faster and faster will fail behind the competition, in the end automation is the key to making this happen. 

So why Gradle?

<img src=".\img\2017729-134401.jpg"/ style="height:260px">       

The biggest reason is that Google has selected Gradle as the build system for Android Studio. In fact, Android Studio delegates the entire process of building Android Apps to Gradle. When I hit the run button, Android Studio just sets Gradle in motion and sits back to watch. By learning about Gradle, we can extend this default behavior to build even more and more capable and well tested Android apps.

Obviously, Google is full of very smart engineers. And one measure of their smarts is that they 



# 39  Android Studio, Gradle, and Build Varain

Android Studio work together to build and deploy your apps. We'll also talk about how Gradle makes it easy to create variance of your apps,  like debug and release builds, and paid versus free versions. 



# 40  Android Studio and Gradle

Android Studio is an incredibly powerful piece of software. It has an editor with sophisticated code completion, and static analysis features. It also has a suite of tools for integrating with Android devices and emulators. The one thing it doesn't have, however, is an integrated build system. Android Studio delegates the entire build process to Gradle.

<img src=".\img\2017729-141239.jpg" style="height:260px"/>

That's everything that happens to turn your sources and resources into an APK that you can install on your device. Gradle itself doesn't inherently know anything about Android. That capability's provided by Google in the form of an Android Gradle plugin. Android Studio is actually happy to import and work with any Gradle project. We can use it to do all sorts of interesting things, like build Java libraries or deploy a backend service to Google App Engine. Even though Android Studio isn't building your project, it still needs a deep model of your project, so it can provide features like code completion, and auto importing. It maintains its own internal model of your project, and when a project is loaded or a Gradle  build script changes, Android Studio needs to synchronize its internal model with Gradle's model. When you get a "failed to sync" message, it usually means you've just got an error in one of your build scripts. 







































