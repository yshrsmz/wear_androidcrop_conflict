Attribute conflict with Android Crop & Support Android Wear library
===

When I tried to use [android-crop](https://github.com/jdamcd/android-crop) and `com.google.android.support:wearable:2.0.4` in same project(actually I was trying to upgrade wearable project to v2), I faced following error.
 
```
AGPBI: {"kind":"error","text":"Attribute \"highlightColor\" already defined with incompatible format.","sources":[{"file":"/home/myname/repos/wear_androidcrop_conflict/app/build/intermediates/res/merged/debug/values/values.xml","position":{"startLine":328}}],"original":"","tool":"AAPT"}
AGPBI: {"kind":"error","text":"Original attribute defined here.","sources":[{"file":"/home/myname/repos/wear_androidcrop_conflict/app/build/intermediates/res/merged/debug/values/values.xml","position":{"startLine":313}}],"original":"","tool":"AAPT"}
/home/myname/repos/wear_androidcrop_conflict/app/build/intermediates/res/merged/debug/values/values.xml:329: error: Attribute "highlightColor" already defined with incompatible format.
/home/myname/repos/wear_androidcrop_conflict/app/build/intermediates/res/merged/debug/values/values.xml:314: Original attribute defined here.
```

After some investigation, I found that 

`com.google.android.support:wearable` has following styleable from `2.0.2`

```
<declare-styleable name="ComplicationDrawable">
  <attr format="color" name="backgroundColor"/>
  <attr format="reference" name="backgroundDrawable"/>
  <attr format="color" name="textColor"/>
  <attr format="color" name="titleColor"/>
  <attr format="string" name="textTypeface"/>
  <attr format="string" name="titleTypeface"/>
  <attr format="dimension" name="textSize"/>
  <attr format="dimension" name="titleSize"/>
  <attr format="dimension" name="iconColor"/>
  <attr format="color" name="borderColor"/>
  <attr format="dimension" name="borderRadius"/>
  <attr name="borderStyle">
    <enum name="none" value="0"/>
    <enum name="solid" value="1"/>
    <enum name="dashed" value="2"/>
  </attr>
  <attr format="dimension" name="borderDashWidth"/>
  <attr format="dimension" name="borderDashGap"/>
  <attr format="dimension" name="borderWidth"/>
  <attr format="dimension" name="rangedValueRingWidth"/>
  <attr format="dimension" name="rangedValuePrimaryColor"/>
  <attr format="dimension" name="rangedValueSecondaryColor"/>
  <attr format="color" name="highlightColor"/>
</declare-styleable>
```

and android-crop has following styleable.

```
<declare-styleable name="CropImageView">
  <attr format="reference|color" name="highlightColor"/>
  <attr format="boolean" name="showThirds"/>
  <attr format="boolean" name="showCircle"/>
  <attr name="showHandles">
    <enum name="changing" value="0"/>
    <enum name="always" value="1"/>
    <enum name="never" value="2"/>
    </attr>
</declare-styleable>
```

Both styleables have same attribute `highlightColor`, so this is the problem.
