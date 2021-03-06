
<img src="https://i.imgur.com/tZybQsU.gif"/>

# Pywalfox

Pywalfox is an addon used to theme Firefox using your pywal colors.
- Customizable colors
- Uses the Firefox Theme API
- Automatic theming for DuckDuckGo (Optional)
- Custom CSS with bold text, styled dropdowns, etc. (Optional)
- Update the browser theme using the addon and/or your terminal

You can download the Firefox Addon here: https://addons.mozilla.org/en-US/firefox/addon/pywalfox/

### Warning
To use this addon, you must install a script on your computer. The script will be ran by Firefox upon launch and will handle fetching your pywal colors. As of now, Pywalfox supports only Linux.

### Requirements
**There currently seems to be an issue in `daemon/pywalfox.py` for those running python 2.7.x and I will fix it as soon as possible.**
- Python (both ~~2.7.x~~ and 3.x versions are supported) 
- Linux 

### Installation
1. `git clone git@github.com:Frewacom/Pywalfox.git`
2. `cd Pywalfox`
3. `bash setup.sh`

The setup script will prompt you for your password since the path in which we need to place the native messaging manifest is protected by default. Firefox requires the manifest to allow communication between the addon and the script running on your computer.

If the setup is successfull, it should look something like this:
```
Creating 'native-messaging-hosts' folder in ~/.mozilla
Copying native messaging manifest to /home/<username>/.mozilla/native-messaging-hosts/pywalfox.json
Setting path to daemon/pywalfox.py in the manifest
Setting execution permissions on daemon/pywalfox.py
Finished.
```

Restart Firefox and you should be able to fetch the colors using the Settings page. If not, take a look in the Troubleshooting section below. 

### Updating the theme using the terminal
If you are using some script for theming your system and do not want to manually refetch your pywal colors using the settings page, you can trigger an update of the browser theme by running `./daemon/pywalfox.py update` in your terminal (the script is not in your `PATH` by default).

### Custom CSS
If you want to use the custom CSS, you must do the following:
1. Navigate to `about:config` in Firefox
2. Set `toolkit.legacyUserProfileCustomizations.stylesheets` to `true`

### Troubleshooting
* Take a look at the Debugging output in the Settings page of the addon
* Make sure that `path` in `~/.mozilla/native-messaging-hosts/pywalfox.json` points to the location of `daemon/pywalfox.py`
* Make sure that `pywalfox.py` is executable (`chmod +x pywalfox.py`)
* Make sure that the file `~/.cache/wal/colors` exists and contains the colors generated by pywal
* Take a look at the Browser console (`Tools > Web developer > Browser console`) for errors

#### Errors in browser console
- `ExtensionError: No such native application pywalfox`

   The manifest is not installed properly. Follow the instructions here: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests. The manifest is located at `daemon/assets/pywalfox-manifest.json`.

- `Unchecked lastError value: Error: Could not establish connection. Receiving end does not exist.`

   The path to the script in the manifest is invalid or the script crashed on execution (try running it manually). 
   
   The script runs in an infinite loop, so as long as the script does not crash when running it, we know that the issues lies somewhere else. 

If you encounter any other errors: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_messaging#Troubleshooting

