#!/bin/bash
echo "-- building new app --"
gradle assembleDebug

apk=$(find -iname "*debug.apk")
pkg=$(aapt dump badging $apk|awk -F" " '/package/ {print $2}'|awk -F"'" '/name=/ {print $2}')
act=$(aapt dump badging $apk|awk -F" " '/launchable-activity/ {print $2}'|awk -F"'" '/name=/ {print $2}')

echo "-- uninstalling old app --"
adb shell pm uninstall $pkg

echo "-- installing new app --"
adb install $apk

echo "-- starting app --"
adb shell am start -n $pkg/$act


