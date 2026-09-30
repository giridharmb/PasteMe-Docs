# Why Paste Me asks for Accessibility access

When you choose an item in Paste Me, it does two things:

1. puts the item on the clipboard
2. presses **⌘V** in the app you were using, so the item is pasted right where your cursor is

macOS only lets an app press keys in another app if you've allowed it under **Accessibility**. Paste Me uses this permission for exactly two things:

- sending **⌘V** when you paste
- sending **⌘C** when you use the optional "Copy selection & pin it" shortcut

It doesn't read your screen, record your keystrokes, or control other apps in any other way.

**Without the permission,** Paste Me still copies your chosen item to the clipboard, and you press ⌘V yourself.

## Grant access

1. Open **System Settings ▸ Privacy & Security ▸ Accessibility**. Paste Me's Settings ▸ General ▸ **Grant Access…** button opens this page for you.
2. Turn on **Paste Me**. If it isn't listed, click **+** and choose Paste Me from Applications.
3. That's it. You don't need to restart.

## Fixing a stuck permission

After an update, macOS sometimes keeps an old entry that no longer matches the app:

1. In the Accessibility list, select **Paste Me** and click **–** to remove it.
2. Click **+** and add Paste Me again. You can also run this in Terminal: `tccutil reset Accessibility com.guy.PasteMe`.
3. Try pasting again.
