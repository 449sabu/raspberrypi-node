# raspberrypi-node
自分及び、Raspberry Pi 4 を初めて触る方に向けて、コマンドをまとめたもの
Raspberry Pi 4 でCardanoのステーキングプールを構築することを最終目的とする。

# 用意するもの
・RaspberryPI ４B ×２（リレー用、ブロックプロデューサ用）
・Micro SDカード　３２GB
・SSD
・SSDケース（SATA接続をUSB3.0に変換する互換性のあるもの）

# 1. MicroSDに RaspberryPiOS を書き込む

# 2. SSH接続できるようにする
OSを書き込んだMicroSDのboot直下に空のsshと名のついたファイル(拡張子なし)を作成する
```
cd /Volumes/boot 
touch ssh /Volumes/boot 
```

```
ssh pi@raspberrypi.local
```

# 3. インターネットに接続できるようにする
起動する前に`boot`直下にある`wpa_supplicant.conh`にWi-Fiを記述することで初回起動時から無線LANにアクセスできるようになる。

```
cd /Volumes/boot
nano /Volumes/boot/wpa_supplicant.conf
```

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
country=JP
update_config=1

network={
    ssid="ssid"
    psk="pwd"
}
```
参照：https://www.raspberrypi.com/documentation/computers/configuration.html#configuring-networking-2



