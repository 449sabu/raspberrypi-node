# RaspberryPiでのRTSオプションについて
以下のコマンドを実行すると、コンパイルで使用されたデフォルトオプションを確認できる。
```
cardano-node +RTS --info
```
>以下が現在のノードで指定されているデフォルトオプション
```
"-T -I0 -A16m -N2 --disable-delayed-os-memory-return"
```
RTSオプションをデフォルトから変更することはIOGは推奨しておらず、自己責任。
***
# GHC/RTSオプション詳細
`-A<size>m`=nursery blocksのサイズを指定します<br>
`-Iw⟨seconds⟩`=アイドル状態のGC間の最小待機時間をこのフラグで指定できます。たとえば、-Iw60は、アイドル状態のGCが最大で1分に1回実行されることを保証します。<br>
`-H<size>M`=RTSが起動時に指定したサイズのRAMを強制的に割り当て、この最低割り当て量を維持します。
`-n<size>m`
`-T`<br>
`-S`<br>
>参考文献
[GHC/Memory_Management](https://downloads.haskell.org/~ghc/latest/docs/html/users_guide/runtime_control.html#miscellaneous-rts-options)<br>
***
```
--disable-delayed-os-memory-return -I0.3 -Iw600 -A64m -n4m -F1.2 -qg1
```
[参考：ELMPI Poolさん](https://discord.com/channels/747675500297584720/792575220719943720/981941307771588689)<br>
***
更新履歴
>22/06/06 -Relay
```
+RTS -N2 --disable-delayed-os-memory-return -I0.3 -Iw600 -A64m -n4m -F1.5 -qg1 -RTS
```
>22/6/14 -BP
```
# 更新前
+RTS -N --disable-delayed-os-memory-return -I0.1 -Iw300 -A32m -n4m -F1.5 -H2500M -T -S -RTS
#更新後
+RTS -N2 --disable-delayed-os-memory-return -I0.3 -Iw600 -A64m -n4m -F1.5 -qg1 -RTS
```
