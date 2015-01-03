Material Navigation Drawer
==========================

Navigation Drawer according to Material Design spec.

How it works
------------

 - Icon color defaults to `android:textColorSecondary` when not selected. See `NavigationItemDescriptor`.
 - Text color and selected icon color defaults to `android:textColorPrimary`. See `NavigationItemDescriptor`.
 - Activated background is set to 12% of `android:colorForeground`. This currently limits the use to white drawer on white theme or black on black.
 - List background is set to `android:colorForegroundInverse`. (*)
 - Divider color is 12% of `android:colorForeground`. You cannot change this currently.

(*) You can modify this by accessing one of `NavigationDrawerFragment.setBackground()` methods.

Please note that this is not a drawer per se, the fragment can be used as a pinned side bar (e.g. on 10" tablets). For usage example see the `sample `directory.

Minimum API is 11, because activated selector is introduced just then. As recommended minimum is API 14, lowering the requirements is not planned.

To use this library add the following to your module's `build.gradle`:
```groovy
dependencies {
    compile 'net.xpece.material:navigation-drawer:0.2.1@aar'
}
```

The project depends on support-v4 library version 21.0.3.

Customization
-------------

As of support-v4 library 21.0.3 there is a hardocded margin of 64dp in a `DrawerLayout`. Use `NavigationDrawerUtils.fixMinDrawerMargin(DrawerLayout)` to remove this limitation. Use this right after you obtain a drawer layout instance typically in `Activity.onCreate(Bundle)`. Why is this an issue? Specs say the margin should be only 56dp on phones.

To set proper drawer width according to specs call `NavigationDrawerUtils.setProperNavigationDrawerWidth(View)` on your instance of `NavigationDrawerFragment.getView()`. This is not handled automatically to allow developers to reuse the fragment outside of `DrawerLayout` with custom width.

`NavigationSectionDescriptor`

 - Use `heading(String)` to set optional section heading.
 - Use `addItem(NavigationItemDescriptor)` or `addItems(List<NavigationItemDescriptor>)`. These allow you to chain calls as opposed to standard `List` methods.
 
`NavigationItemDescriptor`

- Use `sticky()` and `notSticky()` to specify whether the item should stay selected on click or not.
- Use `icon(int)` to specify a drawable resource. Typically this would be a 24dp by 24dp icon. This gets colored automatically.
- Use `text(String)` or `text(int)` to set item label.
- Use `badge(String)` or `badge(int)` to set badge text. Badge will be hidden when supplied value is `null`;
- Use `activeColor(int)` and its derivatives to specify color of selected icon and text.
- Use `passiveColor(int)` and its derivatives to specify color of unselected icon. Note that unselected text always takes color of `android:textColorPrimary`.
- Use `badgeColor(int)` and its derivatives to specify background color of the badge. Text color is calculated automatically.
 
Work TBD
--------

 - Better API, factories, copying element prototypes.
 - ~~Lower API requirement preferrably to level 4 and ditch dependencies.~~
 - ~~Code resources and deploy as jar instead of aar.~~