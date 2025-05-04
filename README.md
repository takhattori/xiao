# xiao

[まずは開発環境](./Install_PlatformIO_to_VSCODE.md)

[XIAO expansion board]
Wire定義の修正 (Raspberry Pi Pico/RP2040ボード(Arduino-Pico) バージョン4.4.4以降)
Raspberry Pi Pico/RP2040ボード(Arduino-Pico) バージョン4.4.4でWire1が定義されましたが、背面パッドのI2CがWireで定義されたため、I2CのデフォルトピンがWire1に定義された状態になっています。

I2CデフォルトピンをWire、背面パッドのI2CをWire1と定義するには、pins_arduino.hのWire定義を以下のように修正してください。
なお、I2CデフォルトピンをWire1で使用する場合は、修正は不要です。

// Wire
#define __WIRE0_DEVICE (i2c1)
#define PIN_WIRE0_SDA  (6u)
#define PIN_WIRE0_SCL  (7u)
#define SDA            PIN_WIRE0_SDA
#define SCL            PIN_WIRE0_SCL
#define I2C_SDA        (SDA)
#define I2C_SCL        (SCL)

#define __WIRE1_DEVICE (i2c0)
#define PIN_WIRE1_SDA  (16u)
#define PIN_WIRE1_SCL  (17u)

pins_arduino.hの場所

場所
C:¥Users¥ユーザ名¥AppData¥Local¥Arduino15¥packages¥rp2040¥hardware¥rp2040¥バージョン¥variants¥seeed_xiao_rp2350¥pins_arduino.h
