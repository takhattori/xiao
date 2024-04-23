#Install_PlatformIO_to_VSCODE

・VSCODEインストール

・Extentionで

　Japanese Language Pack for Visual Studio Code

　platformio ide

　Serial Monitor

　teleplot

　をインストール

・Boardの準備(1)（mbedの場合：SPIが異常に遅い）

　・ターミナルでコマンド打つ。

　　　pio platform install nordicnrf52

　　　->ユーザフォルダ("thatt"）配下の".platformio/platforms"に"nordicnrf52"ができる

　・"nordicnrf52/boards"配下に"xiaoblesense.json"を新規作成。下記をコピーペースト


#
[xialblesense.json](./xiaoblesense.json)
```json
{
    "build": {
      "arduino":{
        "ldscript": "linker_script.ld"
      },
      "core": "arduino",
      "cpu": "cortex-m4",
      "extra_flags": "-DSEEED_XIAO_NRF52840_SENSE -DARDUINO_ARCH_NRF52840",
      "f_cpu": "64000000L",
      "hwids": [
        [
          "0x2886",
          "0x0045"
        ],
        [
          "0x2886",
          "0x8045"
        ]
      ],
      "mcu": "nrf52840",
      "variant": "SEEED_XIAO_NRF52840_SENSE",
      "softdevice": {
        "sd_flags": "-DS140",
        "sd_name": "s140",
        "sd_version": "7.3.0",
        "sd_fwid": "0x0123"
      }
    },
    "connectivity": [
      "bluetooth"
    ],
    "debug": {
      "jlink_device": "nRF52840_xxAA",
      "openocd_target": "nrf52.cfg",
      "svd_path": "nrf52840.svd"
    },
    "frameworks": [
      "arduino"
    ],
    "name": "Seeed XIAO BLE Sense",
    "upload": {
      "maximum_ram_size": 237568,
      "maximum_size": 811008,
      "protocol": "nrfutil",
      "speed": 115200,
      "protocols": [
        "jlink",
        "nrfjprog",
        "nrfutil",
        "cmsis-dap",
        "sam-ba",
        "blackmagic"
      ],
      "use_1200bps_touch": true,
      "require_upload_port": true,
      "wait_for_upload_port": true
    },
    "url": "https://wiki.seeedstudio.com/XIAO_BLE",
    "vendor": "Seeed Studio"
}
```
#


　・ひな形を作るため最初、新規プロジェクトを作成。boardには"Arduino Nano 33 BLE"を指定。

　　　."platformio/packages"配下に"framework-arduino-mbed"と"tool*"ができていることを確認


　・下記ファイルをダウンロードし、2.6.1配下のファイルを"framework-arduino-mbed"にコピー

　　　wget -c https://files.seeedstudio.com/arduino/core/nRF52840/Seeed_XIAO_BLE_nRF52840_Sense261.tar.bz2

　　　tar -xjf Seeed_XIAO_BLE_nRF52840_Sense261.tar.bz2

　　　cp -r 2.6.1/* $HOME/.platformio/packages/framework-arduino-mbed



　・"nordicnrf52"配下の"platform.py"を追加加工

　　if board in ("nano33ble", "nicla_sense_me", "xiaoblesense"):

　　self.packages["tool-adafruit-nrfutil"]["optional"] = False



・Boardの準備(2)（Non-mbedの場合、不具合は不明。SPIは正常）

  - Adafruit nrf52840 based board（例えば nrf52840 feather express）で空プロジェクトを作る
  
  - 一度ビルドすると必要ファイルをもってくる

  - 必要ファイルコピーする

  - "name": "Seeed Xiao BLE Sense" + "vendor": "Seeed Studio"　を選択


------

curl https://files.seeedstudio.com/arduino/core/nRF52840/Arduino_core_nRF52840.tar.bz2 -o arduino.core.1.0.0.tar.bz2

tar -xjf arduino.core.1.0.0.tar.bz2

rm arduino.core.1.0.0.tar.bz2 

# download the board from GitHub

curl https://gist.githubusercontent.com/turing-complete-labs/0763b9d89913a4647c9fa1b988a5bdb6/raw/2100fb176d73a431080cc7f688d7ac8b603e03a3/xiao_ble_sense.json -o ~/.platformio/platforms/nordicnrf52/boards/xiao_ble_sense.json

# copy the needed files

cp 1.0.0/cores/nRF5/linker/nrf52840_s140_v7.ld ~/.platformio/packages/framework-arduinoadafruitnrf52/cores/nRF5/linker

cp -r 1.0.0/cores/nRF5/nordic/softdevice/s140_nrf52_7.3.0_API ~/.platformio/packages/framework-arduinoadafruitnrf52/cores/nRF5/nordic/softdevice

cp -r 1.0.0/variants/Seeed_XIAO_nRF52840_Sense ~/.platformio/packages/framework-arduinoadafruitnrf52/variants

------



