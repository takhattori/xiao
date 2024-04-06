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
