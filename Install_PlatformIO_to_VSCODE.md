#Install_PlatformIO_to_VSCODE

・VSCODEインストール

・Extentionで

　Japanese Language Pack for Visual Studio Code

　platformio ide

　Serial Monitor

　teleplot

　をインストール

・Boardの準備

　・ターミナルでコマンド打つ。

　　　pio platform install nordicnrf52

　　　->ユーザフォルダ("thatt"）配下の".platformio/platforms"に"nordicnrf52"ができる

　・"nordicnrf52/boards"配下に"xiaoblesense.json"を新規作成。下記をコピーペースト


#
[xialblesense.json](./xiaoblesense.json)
#


・新規プロジェクトを作成。boardには"Arduino Nano 33 BLE"を指定。

　."platformio/packages"配下に"framework-arduino-mbed"と"tool*"ができていることを確認


・下記ファイルをダウンロードし、2.6.1配下のファイルを"framework-arduino-mbed"にコピー

　wget -c https://files.seeedstudio.com/arduino/core/nRF52840/Seeed_XIAO_BLE_nRF52840_Sense261.tar.bz2

　tar -xjf Seeed_XIAO_BLE_nRF52840_Sense261.tar.bz2

　cp -r 2.6.1/* $HOME/.platformio/packages/framework-arduino-mbed



・"nordicnrf52"配下の"platform.py"を追加加工

　　if board in ("nano33ble", "nicla_sense_me", "xiaoblesense"):

　　self.packages["tool-adafruit-nrfutil"]["optional"] = False

