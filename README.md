# Flutter Emoji Picker

Yet another Emoji Picker for Flutter 🤩

## Key features

1. Lightweight Package

2. Faster Loading

3. Null-safety

4. Completely customizable

5. Material Design and Cupertino mode

6. Emojis that cannot be displayed are filtered out (Android Only)

7. Optional recently used emoji tab

8. Skin Tone Support

9. Custom-Font Support

## Getting Started

   ```
   import 'package:flutter/foundation.dart' as foundation;
EmojiPicker(
    onEmojiSelected: (Category category, Emoji emoji) {
        // Do something when emoji is tapped (optional)
    },
    onBackspacePressed: () {
        // Do something when the user taps the backspace button (optional)
        // Set it to null to hide the Backspace-Button
    },
    textEditingController: textEditionController, // pass here the same [TextEditingController] that is connected to your input field, usually a [TextFormField]
    config: Config(
        columns: 7,
        emojiSizeMax: 32 * (foundation.defaultTargetPlatform == TargetPlatform.iOS ? 1.30 : 1.0), // Issue: https://github.com/flutter/flutter/issues/28894
        verticalSpacing: 0,
        horizontalSpacing: 0,
        gridPadding: EdgeInsets.zero,
        initCategory: Category.RECENT,
        bgColor: Color(0xFFF2F2F2),
        indicatorColor: Colors.blue,
        iconColor: Colors.grey,
        iconColorSelected: Colors.blue,
        backspaceColor: Colors.blue,
        skinToneDialogBgColor: Colors.white,
        skinToneIndicatorColor: Colors.grey,
        enableSkinTones: true,
        showRecentsTab: true,
        recentsLimit: 28,
        noRecents: const Text(
          'No Recents',
          style: TextStyle(fontSize: 20, color: Colors.black26),
          textAlign: TextAlign.center,
        ), // Needs to be const Widget
        loadingIndicator: const SizedBox.shrink(), // Needs to be const Widget
        tabIndicatorAnimDuration: kTabScrollDuration,    
        categoryIcons: const CategoryIcons(),
        buttonMode: ButtonMode.MATERIAL,
    ),
)
```

## Backspace-Button

You can add a Backspace-Button to the end category list by adding the callback method onBackspacePressed: () { } to the EmojiPicker-Widget. This will make it easier for your user to remove an added Emoji without showing the keyboard. Check out the example for more details about usage. Set it to null to hide the Backspace-Button.

## Custom view

The appearance is completely customizable by setting customWidget property. If properties in Config are not enough you can inherit from EmojiPickerBuilder (recommended but not necessary) to make further adjustments.

   ```
   class CustomView extends EmojiPickerBuilder {
    CustomView(Config config, EmojiViewState state) : super(config, state);

    @override
    _CustomViewState createState() => _CustomViewState();
}

class _CustomViewState extends State<CustomView> {
    @override
    Widget build(BuildContext context) {
        // TODO: implement build
        // Access widget.config and widget.state
        return Container();
    }
}

EmojiPicker(
    onEmojiSelected: (Category category, Emoji emoji) { /* ...*/ },
    config: Config( /* ...*/ ),
    customWidget: (config, state) => CustomView(config, state),
)
```

## Extended usage with EmojiPickerUtils

```
// Get recently used emoji
final recentEmojis = await EmojiPickerUtils().getRecentEmojis();

// Search for related emoticons based on keywords
final filterEmojiEntities = await EmojiPickerUtils().searchEmoji("face", defaultEmojiSet);

// Add an emoji to recently used list or increase its counter
final newRecentEmojis = await EmojiPickerUtils().addEmojiToRecentlyUsed(key: key, emoji: emoji);
// Important: Needs same key instance of type GlobalKey<EmojiPickerState> here and for the EmojiPicker-Widget in order to work properly

// Highlight emojis with custom style spans
final textSpans = EmojiPickerUtils().setEmojiTextStyle('text', emojiStyle: style);

// Clear list of recent Emojis
EmojiPickerUtils().clearRecentEmojis(key: key);
```