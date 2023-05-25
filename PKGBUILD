#!/bin/bash

STR=$'[Desktop Entry]\nEncoding=UTF-8\nName=OutFox\nGenericName=Rhythm and dance game\nTryExec=OutFox\nExec=OutFox\nTerminal=false\nIcon=OutFox\nType=Application\nCategories=Application;Game;ArcadeGame\nComment=A cross-platform rhythm video game.'
#echo -e $STR > OutFox.desktop

mkdir OutFox.AppDir
mkdir OutFox.AppDir/usr
mkdir OutFox.AppDir/usr/bin
mkdir OutFox.AppDir/usr/lib

wget -O appimagetoolx64.AppImage https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage
chmod +x appimagetoolx64.AppImage

#extracts the outfox tar.gz in the working directory
ls OutFox*.tar.gz | xargs -I{} tar -xf {} --strip-components=1 --directory OutFox.AppDir/usr/bin
cp OutFox.png OutFox.AppDir/OutFox.png
cp OutFox.desktop OutFox.AppDir/OutFox.desktop
wget https://raw.githubusercontent.com/AppImage/AppImageKit/master/resources/AppRun
chmod a+x AppRun
mv AppRun OutFox.AppDir/AppRun
sed -i -e 's#/usr#././#g' OutFox.AppDir/usr/bin/OutFox
ldd OutFox.AppDir/usr/bin/OutFox | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -v '{}' OutFox.AppDir/usr/lib
sed -i -r 's+/usr/share/OutFox/OutFox+OutFox+g' OutFox.AppDir/OutFox.desktop
ARCH=x86_64 ./appimagetoolx64.AppImage OutFox.AppDir
