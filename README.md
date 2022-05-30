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
nanoエディタを使用します。`"ssid"`と`"pwd"`には接続先のそれぞれの値を入力しましょう。
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
RaspberryPiを起動してから設定したWi-Fiに接続されるまで5分ほどかかる場合がある

# ブートローダーのバージョンを確認する
```
vcgencmd bootloader_version
```
USBから起動できるように設定を変更する。
```
sudo raspi-config
```
「6　Advanced Options...」を選択 → 「A6 Boot Order...」を選択 → 「B2 USB Boot...」を選択 → 「USB is default boot device」と出たらEnterを押す → 「Finish」を選択しラズパイを再起動させる。



# シャットダウンする場合
入力後、緑色のランプが消えるまでじっと待つ
```
sudo shutdown -h now
```



# LLVMインストール
```
sudo apt install llvm-13 libnuma-dev
```
/usr/bin/opt-9 のシンボリックリンク /usr/bin/opt を作成する
```
sudo ln -s /usr/bin/opt-13 /usr/bin/opt
ls -al /usr/bin/opt
sudo ln -s /usr/bin/llc-13 /usr/bin/llc
ls -al /usr/bin/llc
```
戻り値：/usr/bin/opt -> /usr/bin/opt-13　　/usr/bin/llc -> /usr/bin/llc-13



# DBを圧縮して転送する
`.tar.gz`という拡張子はアーカイブファイルである`.tar`を`gzip`形式で圧縮したファイルを示す。
ファイルを圧縮する場合は以下のコマンド
```
tar -zcvf <圧縮後の任意のファイル名.tar.gz> <圧縮したいファイル>
```
`.tar.gz`ファイルを解凍する場合は以下のコマンド
```
tar -zxvf <xxxx.tar.gz>
```
オプションの意味`Z`zgip形式を指定`C`新しいtarファイルを作る`x`解凍`v`圧縮・解凍状況を表示`f`圧縮ファイル名指定。
```
# rm <ファイル名>　ファイルを指定して削除するコマンド

```



