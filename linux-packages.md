####Entertainment:
* Vlc
* ubuntu-restricted-extras
* sudo /usr/share/doc/libdvdread4/install-css.sh
* gnash
* MusicBrainz Picard   __ppa:musicbrainz-developers/stable__
  * Settings:
```
$if($ne(%albumartist%,),%albumartist%/)$if($ne(%album%,),%album%/)$if($gt(%totaldiscs%,1),%discnumber%-,)$if($ne(%tracknumber%,),$num(%tracknumber%,2) ,)%title%$if($ne(%album%,), - %album%)
```
* Puddletag, EasyTAG, Cowbell, Beets
  * Settings:
```
$num(%track%,2) %title% - %album%
remove tags other than Tags: title;album;composer;albumartist;artist;genre;track;discnumber;date;year;lyricist;unsyncedlyrics; comment;__image;Acoustid Id;
remove comments
remove lyricist
remove unsyncedlyrics
export artwork
remove __image
Clean up - title, album, composer, albumartist,   artist, genre, __filename
Standard Conversion
Fill empty
Fill Up
```
* SMPlayer

####Video Editor:
* Lightworks
* PiTiVi
* HandBrake

####Management:
* Keepassx
* Bleachbit
* gnome-contacts
* fslint, fdupes, dupeguru (PE, ME)

####Development:
* Git                  __ppa:git-core/ppa__
* Pencil Project
* Meld
* Diffuse
* Eclipse
* Brackets
  * libgcrypt11 dependency issue
  * Beautify - Format JavaScript, HTML, and CSS files.
  * Interactive Linter - Integration with linters such as JSHint, JSLint, ESLint, JSCS, CoffeeLint, and more!
  * Emmet - High-speed HTML and CSS workflow.
  * Brackets Bower - Manage your application's front-end dependencies using the bower.json file.
  * AngularJS for Brackets & AngularJS Code Hints
* OpenJDK/JDK
* java-decompiler
* build-essential	_contains make gcc etc._
* Cola git
* Gitg
* Giggle
* Apache Maven
* MongoDB
* Curl
* NodeJS              __curl --silent --location https://deb.nodesource.com/setup_4.x | sudo bash -__
* npm - live-server
* npm - angular2
* npm - systemjs
* npm - typescript
* npm - grunt
* Dart SDK            __add to PATH /usr/lib/dart/bin/ to access dart tools; use ~/.profile__
* jq - a lightweight and flexible command-line JSON processor.

####Server:
* Jetty
* Nginx
* Tomcat
* Samba

####Internet:
* Aria2
* Uget
* FlashGot
* youtube-dl
* Net Activity Viewer
* WireShark
  * dumpcap -D
  * dumpcap -i <capture interface> -w <outfile>
  * dumpcap -i 1 -w /tmp/mycap.pcap
* Fiddler
* Deluge         __ppa:deluge-team/ppa__
* Transmission
* Firefox
  * Flashgot
  * purge + Delete /etc/firefox/:/usr/lib/firefox/:/usr/lib/firefox-addons/:/usr/lib/mozilla/:~/.adobe:~/.macromedia:~/.mozilla:~/.cache/mozilla
  * JVM plugin - icedtea
* Chromium browser
 * chromium-codecs-ffmpeg - Free ffmpeg codecs for the Chromium Browser
 * chromium-codecs-ffmpeg-extra - Extra ffmpeg codecs for the Chromium Browser
 * purge + Delete /etc/chromium-browser:/usr/lib/chromium-browser/:~/.cache/chromium:~/.config/chromium:/usr/share/chromium-browser
 * How to get latest Chromium?
   * sudo add-apt-repository ppa:canonical-chromium-builds/stage
 * Disable hardware acceleration
* Chrome, Vivaldi, Brave, Midori, Qupzilla
* flashplugin-installer
* Empathy (empathy-skype) | Ekiga | Skype
* No Machine
* ICA client (full package)
  * sudo cp /usr/share/ca-certificates/mozilla/AddTrust_External_Root.crt /opt/Citrix/ICAClient/keystore/cacerts/
* Samba
* Webex

####System:
* Intel Linux Graphics(remember to add key signatures)
* iucode-tool _processor microcode update_
* Compizconfig Settings Manager
* Virtual Box	__add the debian repository to source list and add the public key__
  * Install Extension Pack
  * Check whether _dkms_ package is also installed
  * Setup Guest OS -> run VBoxGuestAdditions.iso
  * grep 'vboxusers' /etc/group
    * sudo usermod -G vboxusers -a $USER
* HPLIP
* ClamAV
* ClamTK
* ntopng
* p7zip
* hplip
* gdebi     __debian installer__
* dpkg-deb  __manipulating .deb files__
* Mono      __makes CLR .exe applications run__
* Wine      __makes Win32 .exe applications run__
* tree
* gnome-disk-utility
* gparted
* Foremost, TestDisk, Photorec, extundelete, scalpel
* gscan2pdf
* ubuntu-mate-desktop : mate-desktop-environment
* hardinfo
* Monitorix
* python3-pip
* virtualenv
  * source v-env/bin/activate
  * deactivate
* csvkit
  * in2csv -f json -k fundamentals ~/Desktop/parsehub/club.json > output/club.csv
  * jq .fundamentals < ~/Desktop/parsehub/club.json | in2csv -f json > output/club2.csv
  * csvcut output/club.csv -n
  * csvstat output/club.csv
  * csvjoin -c Symbol,Equities --outer output/club.csv output/table.csv > output/output.csv
  * csvcut -c column\ 1,column2\(yrs\) output.csv > reorder.csv
  * join -1 2 -2 2 --check-order -t , -i club.csv club.csv

####Editor:
* Vim
* Retext
* Remarkable
* Atom
  * atom-beautify
  * emmet
  * linter
  * atom-typescript
* tesseract-ocr
* ocrfeeder

####Learning:
* Artha
