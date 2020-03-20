# SF2和訳について(未完成版)
* 和訳はSoundFont2.04(最新)に従っている. (sf2と略す) SoundFont2.04は2006年に更新されたものであり現在までこの仕様のままである. 現在(2020年3月時点)仕様がすぐに変わるとは考えにくい. 
* sfspec24_japanese.mdが和訳. 原文はsfspec24.pdfにある.
* 完全な和訳は完成していないが, ただ単に和訳するだけでは不十分でシンセの前提知識がないと理解できないため時間がかかっている.
* SoundFont自体があまり良い規格ではないだろうと最近は考えており, sfzの方がいいかもしれない.
* モジュレーターについては全く使われていない機能なので無視していい.
* 図は原文からそのまま切り取ったものを使っている. 
* 原文ではSoundFontだったりSoundFont2だったりSoundFont2.01だったりとバージョンが変にまちまちなところがあるが気にしないこと. 
* 29n2603t8sa.pdfというSoundFontの仕様を元に何かの規格を提案する資料がある. 訳では例の謎の資料と呼んでいる.

## 仕様書を読むときに推奨していること
* MIDI仕様についてある程度の基礎知識を身につけてから読むこと. CCやプリセットやバンクの概念などがsf2仕様書にも出てくる. 
* シンセ音の知識としてASDRやLPFなどについても知っておくこと. https://info.shimamura.co.jp/digital/knowledge/2014/10/34247 がわかりやすい. 
* Section7まではジェネレーターやモジュレーターの機能について簡潔な説明しかしていない. その簡潔な説明だけでは意味不明なのでSection8以降を同時に読むこと. プリセットとインストラメントの役割の違いやジェネレーターの説明などはSF2_Intro.txtが一番わかりやすい. 先にそれを読んでおくと良いかも.

## モジュレーターについて
この機能は深刻な欠陥があると思われる. SoundFont2は音源の効果を演奏データで統一的に扱えるようコントロールに対するバラメーターの変化具合の調整ができる, という目的があったと思うがモジュレーターがあることでかえってジェネレーターの値の制御が煩雑になっている. そういうのはSF2側ではなくて演奏データ側でコントロールを細かくできるようにした方が良かったと思う. 音源と演奏データは分離できない部分があり, 音源と演奏データとの親和性が高いフォーマットが音楽の編集の理想のフォーマットである. モジュレーターは親和性がとても低く, この機能を使ったsf2ファイルは無いのではないか. あってもそれをちゃんと読み込めるソフトはほとんどないだろうとも. ジェネレーターの値を直接変化させる形式を取っていればまだましだったかもしれない. モジュレーターの問題点はモジュレーターが定義されていないとジェネレーターの値の変化具合を任意に変えることができないので(演奏途中で変化具合を変えるべきシチュエーションがそもそもよくわからない), いちいちsf2ファイルにモジュレーターを定義しなくてはならなくなるという点である. もしかしたら記述に誤りがあるかもしれないが.

## サンプルリンクについて
下のリンクは私がfluid-devのMLに質問したスレッド.
https://www.mail-archive.com/fluid-dev@nongnu.org/msg05051.html
この機能は定義が曖昧で実装例は皆無.


## TO DO
* 図の解像度をあげてより見やすくする.
* 原文54pageの部分の和訳は特に意味不明なので修正したい.
* SF2_Intro.txtの説明は非常に重要なため和訳したい.
* モジュレーターの具体例や実装例についてのわかりやすい説明を書く.
* Section7までの完全な和訳をする.

<a name="hutashika"></a>
## 和訳で不確かな部分(自分用のメモ)
* page32の15:chorusEffectsSendの"dry" or unprocessedの訳は英語のままにしている. また, 12dB低いの部分は6dB低いのが正しいのではと思うが
* 61pageのData Entry values have zero-offset at 0x2000. について
* perceptually-additive-real-world unitsについて
知覚的に加法的な単位と訳している. ある単位系では乗法的なものに対し対数をとることで加法的な単位にすることができる. 
* conductive(9.7)
* modLfoToPitchのexcursionを変位と訳している. 波動の波の高さの変位のこと. 
* impediments include the order of(9.7) 順番ではなさそう
* optimum audible equivalent 最適な音と訳した.
* page 54のThe ranges that modulators are active areの部分
* page 54の"added"
* page 54のA modulator in a local preset zone which is not identical to 
* page 54のA modulator in a global preset zone in an presetはanがおかしいしinstrumentのつもりかもしれない
* page 40の8.2.2のinputとoutputが謎
* page 40の8.2.3のThe polarity ifは誤植
* 127/128
* 8.4.22のbetween127/128 and 1は間違っている可能性が高い

* 8.4.4と8.4.3の違い(特に最後)があるのか不明
* Modulatorのtypeとtransform enumrationを混同している可能性がある(bit11からbit15は使われないと言っていたのが怪しい)

## SoundFont2の仕様について参考になるサイト
うつぽかずら さん(@vstcpp)のサイト
http://vstcpp.wpblog.jp/?page_id=2076
@gocha さんの記事 https://qiita.com/gocha/items/f3e7f216a071808e9e2d sf2のファイルフォーマットについて詳しい. 終端条件などの表が見やすい.
