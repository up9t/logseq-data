- Open android studio, go to asset manager, click + button and select vector image, in there select clip art and click the android icon, a menu full of icons will appear, select what you want to use, if the icons you want to import doesn't appear on the menu because of some bugs (also happened to me) or maybe the icon you're looking for isn't available from the Material Symbol site.
  logseq.order-list-type:: number
- Go manually to the Material Symbol site or any other site that offers downloadable vector icon through web browser then search the icon, select the icon, on the right side bar select Android, you can  do two ways XML or Compose, both are valid. XML is a little bit easier to setup.
  logseq.order-list-type:: number
	- Use XML, click download, open Android Studio, select your project, select Asset Manager, then click import drawable, specify the path of the file you just downloaded.
	  logseq.order-list-type:: number
	- Use Compose, currently Asset Manager doesn't support importing Kotlin file automatically, so you need to do it manually. After you select Compose and click download on the Material Symbol site, Change the file name whatever you like, keep it simple, like Home.kt, PageInfo.kt. After that, go to your project in Android studio and drag and drop those downloaded files to the source directory, you could also create a directory first like org/myapp/myapp/ui.icons or whatever. After that, you still need to change the package name on top of each files to match with their directory, for example if you put them in the directory `org/myapp/myapp/ui/icons` then the package name should be `package org.myapp.myapp.ui.icons`. After done, just import it like any normal Kotlin package.
	  logseq.order-list-type:: number
- logseq.order-list-type:: number
- logseq.order-list-type:: number
-
- #android #icon #kotlin