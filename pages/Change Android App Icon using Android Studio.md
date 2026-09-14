- First thing you need to setup your icon file, you can use bitmap image like png, jpeg, or vector image like svg, it's up to you.
- We usually have 1 icon right? for example icon.png, but android uses 2, one is for the foreground and one for the background, they do this to achieve adaptive icon. Make sure you separate your icon into 2. For example foreground.svg and background.svg (jpeg/png also works too)
  id:: 6a3a3163-497d-4e7e-8c8f-74a0fb6228c0
- Open Android Studio like usual, and open your project.
  logseq.order-list-type:: number
- In the right sidebar, click the asset studio
  logseq.order-list-type:: number
- In there, click the plus button, and click Vector Image if you have svg icon, and Image if you have png, jpeg, or similar.
  logseq.order-list-type:: number
- In here you would have two different path, let's see if you select the Vector Image option. You're going to do next is to specify the path of your foreground.svg and then click finish, do it again with background.svg. If you use png/jpeg you can just go to step 6
  logseq.order-list-type:: number
- And now you have 2 added image in your drawable tab, next thing is to make it as the icon. See below step.
  logseq.order-list-type:: number
- For you using jpeg/png or if you have svg and finished the step 4-5, next is select Image option, select adaptive layer, and see the option below it, select foreground layer and select your foreground image, adjust some parameter if needed, if done click finish, do the same with the background  icon.
  logseq.order-list-type:: number
- Done, enjoy the new icon for your app.
  logseq.order-list-type:: number
-
-
- Source https://developer.android.com/studio/write/create-app-icons
- #android #icon