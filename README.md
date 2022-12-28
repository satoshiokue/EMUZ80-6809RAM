# EMUZ80-6809RAM
6809 Single-Board Computer

![EMUZ80-6809RAM](https://github.com/satoshiokue/EMUZ80-6809RAM/blob/main/imgs/IMG_1821.jpeg)  
6809 Single-Board Computer    

![EMUZ80-6809RAM](https://github.com/satoshiokue/EMUZ80-6809RAM/blob/main/imgs/IMG_1822.jpeg)  
MEZ6809RAM  

電脳伝説さん(@vintagechips)のEMUZ80が出力するZ80 CPU制御信号をメザニンボードで組み替え、6809と64kB RAMを動作させることができます。  
RAMの制御信号とメモリマップドIOのMRDY信号をPICのCLC(Configurable Logic Cell)機能で作成しています。  
電源が入るとPICは6809を停止させ、ROMデータをRAMに転送します。データ転送完了後、バスの所有権を6809に渡してリセットを解除します。  

HD63C09PとPIC18F47Q43の組み合わせで動作確認しています。  

動作確認で使用したMPU  
HD63C09P 350kHz - 3.15MHz (1.4MHz - 12.6MHz)  
MC68B09P 2MHz  
HD68A09P  

このソースコードは電脳伝説さんのmain.cを元に改変してGPLライセンスに基づいて公開するものです。

## メザニンボード
https://github.com/satoshiokue/MEZ6809RAM  

## 回路図
https://github.com/satoshiokue/MEZ6809RAM/blob/main/MEZ6809RAM.pdf　　

## ファームウェア

EMUZ80で配布されているフォルダemuz80.X下のmain.cと置き換えて使用してください。
* emuz80_6809ram.c  

## クロック周波数

84行目のCLK_6809がクロック周波数です。初期値は8MHzになっています。  
6809内部で1/4されます。
```
#define CLK_6809 8000000UL
```

## アドレスマップ
```
Memory
RAM1  0x0000 - 0x9FFF 40kバイト
RAM2  0xB000 - 0xFFFF 20kバイト

I/O   0xA000 - 0xAFFF
通信レジスタ 0xA001
制御レジスタ 0xA000
```

## PICプログラムの書き込み
EMUZ80技術資料8ページにしたがってPICに適合するファイルを書き込んでください。  

PIC18F47Q43 emuz80_6809RAM_Q43.hex  

PIC18F47Q83 emuz80_6809RAM_Q8x.hex  
PIC18F47Q84 emuz80_6809RAM_Q8x.hexx  


Enhanced 6502 BASIC by Lee Davison  
https://philpem.me.uk/leeedavison/6502/ehbasic/  

## 6809プログラムの格納
インテルHEXデータを配列データ化して配列rom[]に格納すると0xC000に転送され6809で実行できます。

テキスト変換例  

Grant's 6-chip 6809 computer の "ROM dump and source code"公開されているGrantSearle BASIC ExBasROM.hexは次のように変換します。
http://searle.x10host.com/6809/Simple6809.html

```
hex2bin -p 00 ExBasROM.hex
xxd -i -c16 ExBasROM.bin > ExBasROM.txt
```

使用ツール例[E3V3A / hex2bin]  
https://github.com/E3V3A/hex2bin  

## 謝辞
思い入れのあるCPUを動かすことのできるシンプルで美しいEMUZ80を開発された電脳伝説さんに感謝いたします。

Z80 / 6502 に続き6809を仕様通りの速度で実行できる環境を達成することができました。  

## 参考）EMUZ80
EUMZ80はZ80CPUとPIC18F47Q43のDIP40ピンIC2つで構成されるシンプルなコンピュータです。

![EMUZ80](https://github.com/satoshiokue/EMUZ80-6502/blob/main/imgs/IMG_Z80.jpeg)

電脳伝説 - EMUZ80が完成  
https://vintagechips.wordpress.com/2022/03/05/emuz80_reference  
EMUZ80専用プリント基板 - オレンジピコショップ  
https://store.shopping.yahoo.co.jp/orangepicoshop/pico-a-051.html

## 参考）phemu6809
comonekoさん(@comoneko)さんがEMUZ80にMC6809を搭載できるようにする変換基板とファームウェアphemu6809を発表されました。

![phemu6809](https://github.com/satoshiokue/EMUZ80-6502/blob/main/imgs/IMG_6809.jpeg)

https://github.com/comoneko-nyaa/phemu6809conversionPCB  
phemu6809専用プリント基板 - オレンジピコショップ  
https://store.shopping.yahoo.co.jp/orangepicoshop/pico-a-056.html
