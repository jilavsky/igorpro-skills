---
description: "このファイルは、Igor Pro 9 と比較した Igor Pro 10 の新機能について説明します。これは、他のヘルプファイルのトピックを参照します。."
slug: /igor-pro-10/what-s-new-in-igor-pro-10-ja_jp
---

# What's New in Igor Pro 10? {#what-s-new-in-igor-pro-10}

このファイルは、Igor Pro 9 と比較した Igor Pro 10 の新機能について説明します。これは、他のヘルプファイルのトピックを参照します。

新機能および変更点に関するよくある質問の一覧は、次のURLで公開しています： [https://www.wavemetrics.com/support/faq](https://www.wavemetrics.com/support/faq)

## Version Compatibility in Igor Pro 10 {#version-compatibility-in-igor-pro-10}

Igor Pro 10 は、Igor のすべての旧バージョンで作成されたファイルを読み取ることができます。

Igor Pro 10 で導入された機能を使わない場合、Igor Pro 10 で保存されたエクスペリメントファイルは以前のバージョンでも読み込めます。

Igor Pro 10で追加された機能を使用した後、エクスペリメントファイルを保存すると、そのファイルを以前のバージョンの Igor で読み込もうとする時には、エラーが発生する可能性があります。万一、以前のバージョンの Igor に戻す必要が生じた場合に備え、今すぐすべての Igor ファイルのバックアップコピーを作成しておくことをお勧めします。

Igor Pro 10 では、一部の動作がわずかに変更されています。これらの変更は、既存の Igor エクスペリメントの一部に影響を与える可能性があります。詳細は [Behavior Changes in Igor Pro 10](#behavior-changes-in-igor-pro-10) を参照してください。

### Igor Pro is a 64-bit Application {#igor-pro-is-a-64-bit-application}

Igor Pro バージョン 7～9 は32ビット版と64ビット版の両方で提供されていましたが、Igor Pro 10 は64ビット版のみとなります。これは、Igor Pro 10 で使用する XOP も64ビット対応である必要があることを意味します。

Igor Pro 10 はネイティブ x64 アプリケーションであり、WaveMetrics は Intel/AMD CPU を搭載したマシンでのみ Igor Pro 10 の実行をサポートしています。ただし、Igor Pro 10 インストーラーが、Windows ARM64 マシン（仮想マシンと実機の両方）への Igor のインストールも許可しているかもしれません。Igor 10 を実行するには、使用するマシン/OSが x64 エミュレーションをサポートしている必要があります（最適な結果を得るには Windows 11 24H2 以降を推奨します）。WaveMetrics は、Igor Pro 10 を ARM エミュレーション環境で実行することを明示的にサポートしていませんが、将来的にサポートする可能性があります。このような設定で使用している場合で、バグがあれば報告してください。ただし、修正できる範囲が限られる可能性があることをご了承ください。

### Igor Pro 10 Language Support {#igor-pro-10-language-support}

Igor Pro 10 は、ユーザーインターフェイスおよびドキュメントに使用される言語を決定するために、オペレーティングシステムの言語を自動的に使用します。以前のバージョンでは、WaveMetrics は英語版と日本語版のアプリケーションを別々に提供しており、それぞれに個別のライセンスが必要でした。これは、Igor を実行する時に OS の言語設定が日本語の場合、Igor も日本語を使うことを意味します。必要であれば、この動作を変更することができます。詳細は [Language Selection](/igorpro/igor-basics/using-igor.md) を参照してください。現在、すべてのドキュメントは英語です。これは将来的に変更される可能性があります。

## Features Removed From Igor Pro 10 {#features-removed-from-igor-pro-10}
- PDF マニュアルは廃止されました。

- コマンド [NewCamera](/igorpro/commands/newcamera.md), [ModifyCamera](/igorpro/commands/modifycamera.md), [GetCamera](/igorpro/commands/getcamera.md) がサポートされなくなりました。カメラのサポートは MMI XOP を使用して提供されます（下記参照）。

## XOP Changes in Igor Pro 10 {#xop-changes-in-igor-pro-10}
### New XOPs in Igor Pro 10: {#new-xops-in-igor-pro-10}
- 新しい MMI XOP は、広く普及している Micro-Manager プロジェクトを利用し、科学カメラ、光源、シャッター、フィルターホイール、XY軸ステージ、Z軸ステージなど、幅広いハードウェアの制御を可能にします。詳細は [MMI - Overview](/igorpro/extensions/data-acquisition/mmi/mmi-overview.md) を参照してください。

### XOPs Removed From Igor Pro 10 {#xops-removed-from-igor-pro-10}

- MultiClamp700xCommander XOP は削除されました。Igor Pro 9 ですでに古いものと見なされており、32ビット版のみでした。XOP の64ビット版フォーク（サードパーティによるメンテナンス）は次で入手可能です： [https://github.com/AllenInstitute/mcc-xop](https://github.com/AllenInstitute/mcc-xop)。 WaveMetrics はこのサードパーティ製 XOP を使用しておらず、サポートは提供できません。

- IgorGIS XOP は削除されました。XOP の維持管理、セキュリティ修正プログラム提供時のサードパーティ製ライブラリの更新、およびサポート問い合わせへの対応に必要な専門知識が当社に存在しなくなったため、Igor Pro 9 ですでに古いものとしてマークされました。Igor Pro 9 に同梱されていた64ビット版 IgorGIS64.xop を持っている場合、その XOP を Igor Pro 10 でも引き続き使用できる可能性があります。

### Packages Made Obsolete in Igor Pro 10 {#packages-made-obsolete-in-igor-pro-10}

パッケージを廃止する主な理由は、それを実現するより新しく優れた方法が利用可能になったためです。そのようなパッケージに依存する古いエクスペリメントファイルが残っている可能性があるため、実際にそれらを削除はしません。

- Percentile and Box Plot パッケージは廃止され、WaveMetrics Procedures\Obsolete フォルダーに移動されました。パッケージへの参照が Packages メニューから削除されました。このパッケージの使用は可能ですが、組み込みのボックスプロットの方が優れています（ [Box Plots and Violin Plots](/igorpro/graphing/graphs.md#box-plots-and-violin-plots) を参照）。このプロシージャパッケージをどうしても使いたい場合は：
    ```igor
    #include <Percentile and Box Plot>
    ```

## Guide To Igor Pro 10 Improvements {#guide-to-igor-pro-10-improvements}

このファイルで説明している Igor Pro 10 の改善点は以下の通りです。

[Python Integration in Igor Pro 10](#python-integration-in-igor-pro-10)<br>
[Performance Improvements in Igor Pro 10](#performance-improvements-in-igor-pro-10)<br>
[Display Improvements in Igor Pro 10](#display-improvements-in-igor-pro-10)<br>
[User-Interface Improvements in Igor Pro 10](#user-interface-improvements-in-igor-pro-10)<br>
[Behavior Changes in Igor Pro 10](#behavior-changes-in-igor-pro-10)<br>
[Programming Changes in Igor Pro 10](#programming-changes-in-igor-pro-10)<br>
[Programming Improvements in Igor Pro 10](#programming-improvements-in-igor-pro-10)<br>
[Function and Operation Improvements in Igor Pro 10](#function-and-operation-improvements-in-igor-pro-10)<br>
[Data Browser Improvements in Igor Pro 10](#data-browser-improvements-in-igor-pro-10)<br>
[Window Browser Improvements in Igor Pro 10](#window-browser-improvements-in-igor-pro-10)<br>
[Dialog Improvements in Igor Pro 10](#dialog-improvements-in-igor-pro-10)<br>
[Graphing Improvements in Igor Pro 10](#graphing-improvements-in-igor-pro-10)<br>
[Box and Violin Plot Improvements in Igor Pro 10](#box-and-violin-plot-improvements-in-igor-pro-10)<br>
[Table Improvements in Igor Pro 10](#table-improvements-in-igor-pro-10)<br>
[Page Layout Improvements in Igor Pro 10](#page-layout-improvements-in-igor-pro-10)<br>
[Notebook Improvements in Igor Pro 10](#notebook-improvements-in-igor-pro-10)<br>
[Help Improvements in Igor Pro 10](#help-improvements-in-igor-pro-10)<br>
[Graphics Export Improvements in Igor Pro 10](#graphics-export-improvements-in-igor-pro-10)<br>
[Procedure Window Improvements in Igor Pro 10](#procedure-window-improvements-in-igor-pro-10)<br>
[Gizmo Improvements in Igor Pro 10](#gizmo-improvements-in-igor-pro-10)<br>
[Drawing Improvements in Igor Pro 10](#drawing-improvements-in-igor-pro-10)<br>
[Annotation Improvements in Igor Pro 10](#annotation-improvements-in-igor-pro-10)<br>
[Control and Control Panel Improvements in Igor Pro 10](#control-and-control-panel-improvements-in-igor-pro-10)<br>
[Analysis Improvements in Igor Pro 10](#analysis-improvements-in-igor-pro-10)<br>
[Statistics Improvements in Igor Pro 10](#statistics-improvements-in-igor-pro-10)<br>
[Matrix Improvements in Igor Pro 10](#matrix-improvements-in-igor-pro-10)<br>
[Multipeak Fitting Improvements in Igor Pro 10](#multipeak-fitting-improvements-in-igor-pro-10)<br>
[Image Processing Improvements in Igor Pro 10](#image-processing-improvements-in-igor-pro-10)<br> 
[Data Import And Export Improvements in Igor Pro 10](#data-import-and-export-improvements-in-igor-pro-10)<br>
[Miscellaneous Improvements in Igor Pro 10](#miscellaneous-improvements-in-igor-pro-10)<br>
[New And Improved Packages in Igor Pro 10](#new-and-improved-packages-in-igor-pro-10)<br>
[New And Improved Example Experiments in Igor Pro 10](#new-and-improved-example-experiments-in-igor-pro-10)<br>

## Python Integration in Igor Pro 10 {#python-integration-in-igor-pro-10}

Igor Pro は、Python プログラミング言語との直接的な双方向通信が可能になりました（ [Python Overview](/igorpro/python/python-overview.md) を参照）。

[Python](/igorpro/commands/python.md) および [PythonFile](/igorpro/commands/pythonfile.md) マンドを使って、Igor プロシージャコードからお気に入りの Python ライブラリを呼び出したり、専用の [Python Console](/igorpro/python/python-overview.md#python-console)（Python🠖Open Console）で Python コードを1行ずつ実行したりできます。

<img src="MD_images/Whats_New_In_Igor_Pro_10/python_console.png" alt="Python Console" width="75%"/>

Igor Pro 10 に同梱されている igorpro Python モジュールは、Python と Igor 間でデータをやり取りするための直感的な API を提供します（ [Python Module Reference](/igorpro/python/python-module-reference.md) を参照）。NumPy ライブラリ（[https://numpy.org/](https://numpy.org/)）との変換機能が組み込まれているため、ウェーブを NumPy 配列を必要とする分析関数に渡す作業は比較的簡単です：

```python
import igorpro
import numpy as np

# Get a list of Igor waves inside a data folder
dataset = igorpro.folder('root:analysis').waves()
for wave in dataset:
    # Convert each wave into a numpy array and run the analysis
    results = runCalculations(wave.asarray())
```

Python オブジェクトを Igor に渡し戻すと、それらは自動的に適切な Igor 型に変換されます：
```igor
// Run a Python function that returns a numpy array, and return it to an existing Igor wave
Make/FREE arrayFromPython
Python execute = "arr : ndarray = waveAnalysis()", array = {"arr", arrayFromPython}
```

## Performance Improvements in Igor Pro 10 {#performance-improvements-in-igor-pro-10}

- [NewPath](/igorpro/commands/newpath.md) と [IndexedFile](/igorpro/commands/indexedfile.md) のパフォーマンスが向上しました。特に、[IndexedDir](/igorpro/commands/indexeddir.md) ヘルプトピックの `PrintFoldersAndFiles` サンプルの関数に類似したコードにおいて顕著です。

- Windows 11 上で実行する場合、[MultiThread](/igorpro/programming/keywords/other-programming-keywords.md#multithread) と [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md) は、ハードウェアがサポートする限り、論理プロセッサ（スレッド）を最大限に活用できるようになりました。これまでは、利用可能な論理プロセッサが100個以上あっても、Igor は最大100個までしか使用しませんでした。オペレーティングシステムの制限により、Windows 10 上で実行する場合、64個の論理プロセッサしか使用できません。

## Display Improvements in Igor Pro 10 {#display-improvements-in-igor-pro-10}

Qt と WaveMetrics は、Windows ディスプレイ設定のスケーリング係数が異なる画面の処理を改善しました：

- 小数点以下の表示倍率（つまり、表示倍率が 100% の整数倍ではないパーセンテージ）でモニターに表示する場合、様々なアプリケーションにおけるグラフィックの品質が向上しました。この作業は段階的に進めています。該当するモニターを使用中で、125%、150%、175% の表示時に不自然な点が見つかった場合はお知らせください。

- 複数モニター時の解像度の処理を改善しました。Igor の MDI ウィンドウ（グラフや表などをすべて含む大きなウィンドウ）を、表示スケーリング係数が異なる別のモニターに移動すると、新しい解像度に合わせてグラフなどが再描画されるのが確認できます。

とはいえ、100% の倍数ではないスケーリング係数を使う場合に時々発生する既知の問題がいくつか存在します：

- ウィンドウ枠周辺のグラフィックスの不具合：

    <img src="MD_images/Whats_New_In_Igor_Pro_10/window_scaling_glitches.png" alt="Window scaling glitches" width="75%"/>

    これらの不具合は、Igor のメインウィンドウのサイズを少し変更するか、メインウィンドウを最小化してから元に戻すことで一時的に解消できます。

- テキストの不具合（左軸の回転した`0`文字で確認可能）：

    <img src="MD_images/Whats_New_In_Igor_Pro_10/text_scaling_glitches.png" alt="Text scaling glitches"/>

    これらの不具合は、グラフィックスのエクスポート時やクリップボードへのコピー時には発生しないことが確認されています。

- サイズ調整／位置合わせの不具合

    ウィンドウの一部が移動またはサイズ変更された時に、そのサイズや位置がわずかに（通常1～2ピクセル程度）変化する問題が発生しています。下の例では、タイトルバーのボタンがわずかに異なるサイズになっており、軸や目盛ラベルなどのウィンドウ内のオブジェクトの描画でも同様の現象が確認できます。

   <img src="MD_images/Whats_New_In_Igor_Pro_10/titlebar_scaling_glitches.png" alt="Title bar scaling glitches"/>

- ウィンドウのタイトルバーのボタンが時々動作しない

    場合によっては、ウィンドウのツールバーにある最小化、最大化、および／または標準化ボタンをクリックしても何も起こらないことがあります。表示の拡大率を変更する以外に、この問題の回避策として別のスタイルを使う方法があります。「その他」🠖「その他の設定」メニュー項目を選択して「その他設定」ダイアログを開き、「その他」カテゴリを選択し、「フュージョンスタイルを使用」チェックボックスをオンにします。

    一時的な回避策として、タイトルバーを右クリックし、ボタンをクリックする代わりにコンテキストメニューを使ってウィンドウを操作してください。

Windows の設定で表示スケーリング係数を 100% または 200% に設定すると、通常これらの問題はすべて解消されます。このような問題への対応は継続して行いますが、一部は Qt 側の問題であると考えられるため、修正や回避策の実施には限界がある可能性があります。

複数の構成や状況をテストすることは困難なため、上記以外の明らかなスケーリング問題に遭遇した場合は、問題を support@wavemetrics.com まで報告してください。「ヘルプ」🠖「システム情報」ダイアログ内の情報を必ず含めてください。

## User-Interface Improvements in Igor Pro 10 {#user-interface-improvements-in-igor-pro-10}

- [Control Panel Expansion](/igorpro/user-interface/controls.md#control-panel-expansion) は、 「その他」🠖「その他の設定」ダイアログで無効にできます。

- エクスペリメントの起動コマンドと再現マクロは、「ファイル」🠖「エクスペリメントの情報」ダイアログで確認できます。

- 「グラフ」🠖「コントロールを選択」のサブメニューでは、選択されるコントロールを赤い四角形で囲んでプレビュー表示します。

- 描画ツールのコンテキストメニューにグリッドサブメニューを追加しました。描画モード中にコントロールまたはグラフ上で右クリックし、Grid を選択して使います（ [Modes of Operation](/igorpro/user-interface/controls.md#modes-of-operation) を参照）。

## Behavior Changes in Igor Pro 10 {#behavior-changes-in-igor-pro-10}

- Gizmo ウィンドウ内でのマウスホイールスクロールのデフォルト動作が、回転からズームに変更されました。この設定は、Misc🠖Miscellaneous Settings ダイアログの Gizmo カテゴリで変更できます。

- 特殊なモード 1 および 2 を使う [Listbox](/igorpro/user-interface/controls.md#listbox) コントロール（Listbox *special* キーワードを参照）は、各リストボックスセルの画像上にタイトルを描画する時、コントロールのフォント設定を反映するようになりました。 以前はテキストが定義が不十分なデフォルトフォントで描画されていたため、フォント、フォントサイズ、フォントスタイルを設定していないリストボックスコントロールではわずかな変化が生じていました。当社のテストでは、修正前のフォントサイズは 10 でしたが、デフォルトは 12 になりました。フォント、フォントサイズ、またはフォントスタイルを設定している場合、それらの設定が反映されるため、外観が大きく変わる可能性があります。

- [PopupMenu](/igorpro/commands/popupmenu.md) アクションプロシージャに送信されるメニュー項目テキストは、（ほとんど使用されない）メニューアクセラレーターの '&' 文字が削除されるため、表示されるメニュー項目と同じように見えます。これは、メニュー項目のテキストが、例えば [ControlInfo](/igorpro/commands/controlinfo.md), [GetLastUserMenuInfo](/igorpro/commands/getlastusermenuinfo.md),  [DoIgorMenu](/igorpro/commands/doigormenu.md) に対して ``S_value`` 経由で、または [PopupContextualMenu](/igorpro/commands/popupcontextualmenu.md) に対して ``S_selection`` 経由で返される他のケースにも適用されます。[PopupMenu](/igorpro/commands/popupmenu.md) ``popMatch`` は、後方互換性のために、アクセラレーター '&' 文字の有無にかかわらず文字列を受け入れます。これは主に、１つの "&" を表示する意図で "&&" を含むメニュー項目に適用されますが、Igor 10 以前の PopupMenus では正しく表示されませんでした。

- **スレッドからの出力：** Igor Pro 10 では、Igor プリエンプティブスレッド（ [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking) 参照）から出力可能な履歴行数の制限が撤廃されました。また Igor 10 では、メインスレッドとプリエンプティブスレッド間の出力行の順序付けが改善されています。これらの変更は、履歴ウィンドウにテキストを入力するあらゆる操作に影響します。これには、[Print](/igorpro/commands/print.md) および [printf](/igorpro/commands/printf.md) コマンド、そして [CurveFit](/igorpro/commands/curvefit.md) など、結果を履歴に印刷するあらゆる操作が含まれます。スレッド化されたコードにおける Print および printf コマンドの使用は、主にデバッグ目的であり、出力結果をすべて確認したい場合を想定しています。ただし、制限を解除すると、履歴に膨大な量のテキストが出力される可能性があり、パフォーマンスに深刻な影響を及ぼす恐れがあります。

- スレッドからの暴走した出力による有害な影響の可能性を考慮し、制限を再設定できる新しい [SetIgorOption](/igorpro/commands/setigoroption.md) キーワードを追加しました。詳細については、[Print](/igorpro/commands/print.md) コマンドのドキュメント内の `Printing from Threads` サブセクションを参照してください。

- 描画オブジェクトをドラッグしてサイズ変更、位置変更、または回転させる時、ドラッグ操作がリアルタイムで反映されるようになりました。つまり、ドラッグするとオブジェクトが変化します。以前は、アウトラインが結果を表示し、マウスを離すまでオブジェクトは変更されませんでした。

- 「グラフ」🠖「トレース情報タグを表示」と「テーブル」🠖「列情報タグを表示」の表示は、ツールチップフック機能によって制御されるツールチップの表示に影響しなくなりました。プログラマーは、ツールチップフック機能によって制御されるツールチップをユーザーが簡単にオン/オフできる方法を UI に追加することが推奨されます。

- スレッドセーフなユーザー定義関数から [CleanupName](/igorpro/commands/cleanupname.md) が呼ばれたときに、*maxBytes* パラメーターを無視しなくなりました。

## Programming Changes in Igor Pro 10 {#programming-changes-in-igor-pro-10}

- Igor 10 では、注釈上にマウスが移動した時、マウスが押下された時、およびマウスが離された時に、グラフウィンドウフック関数が呼び出されるようになりました。Igor 9 およびそれ以前のバージョンでは、このイベントは Igor によって取得され、ウィンドウフック関数には到達しませんでした。

- Igor 10 では、グローバル変数または文字列が既に持っていた値と同じ値に代入された場合、そのエクスペリメントを保存する必要があるものとしてマークしなくなりました。この変更がコードに問題を引き起こす場合は、[ExperimentModified](/igorpro/commands/experimentmodified.md) コマンドを呼び出して、エクスペリメントの保存が必要であるとマークしてください。

- Igor 10 以降、メインのプロシージャウィンドウで、次の方法で通常のモジュール名を定義できるようになりました：

    ```igor
    #pragma moduleName = name
    ```

    [The ModuleName Pragma](/igorpro/programming/programming.md#the-modulename-pragma) を参照してください。

- Igor 10 のコンパイラは、以下のコード内の２つの print 文のような、switch 文および strswitch 文内の「到達不能」なコードのコンパイルを拒否します：
    ```igor
    switch(val)
        print "001" // Igor 10 will stop compiling here because this code will never be executed
        case 1:
        ...
        break
        print "002" // same thing: a compile error because of unreachable code
        break
        default:
        ...
        break
    endswitch
    ```

- プログラムによる [Abort](/igorpro/commands/abort.md),  [AbortOnRTE](/igorpro/programming/keywords/flow-control.md#abortonrte) または [AbortOnRTE](/igorpro/programming/keywords/flow-control.md#abortonrte) コマンドが呼び出された場合、Debug On User Abort はデバッガーを起動しなくなりました；デバッガーは、ステータスバーが「デバッグ」と再ラベル付けされた時に、ユーザーがステータスバーの Abort ボタンをクリックして実行を中止した場合にのみ起動されます。[Debugging on Error](/igorpro/programming/debugging.md#debugging-on-error) を参照してください。

- [AnnotationInfo](/igorpro/commands/annotationinfo.md) 関数は、ウィンドウに注釈が存在しない場合、または指定された注釈が存在しない場合に "" を返すようになりました。Igor 10 以前では、これらの場合はランタイムエラーを引き起こしていました。

- [PauseForUser](/igorpro/commands/pauseforuser.md) コマンドは、メインウィンドウまたはターゲットウィンドウが存在しない場合、またはタイプが正しくない場合にエラーを発行するようになりました。

## Programming Improvements in Igor Pro 10 {#programming-improvements-in-igor-pro-10}

- 他の独立モジュールや通常モジュール内の定数は、関数と同様に二重または三重の名前を使って参照できます。

- 通常のモジュール内のスタティックな定数は、二重の名前でアクセスできます。

    例えば：
    ```igor
    switch(val)
        case OtherIM#regularModuleInOtherIM#staticConstantName:
        ...
        break
        case OtherRegularModule#staticConstantName:
        ...
        break
    endswitch
    ```

- プリエンプティブスレッドのエラーは、メインスレッドのエラーと同等の情報をほぼ返すようになりました。

- [The Debugger](/igorpro/programming/debugging.md#the-debugger) オブジェクトリストと構造体の内容は、名前またはタイプでソートできます。

- デバッガーのツールチップおよび式インスペクタは、パスのリテラルなシンボリック名を与えられた時に、そのシンボリックパスの値を表示します。新しいシンボリックパスインスペクタも追加されました。

- [Waveform Arithmetic and Assignment](/igorpro/igor-basics/waves.md#waveform-arithmetic-and-assignment)（ウェーブフォーム演算および代入）による自動インデックス付けで関数を呼び出す時、デバッガーは呼び出し元の関数において、呼び出された関数で使われる [p](/igorpro/commands/p.md), [q](/igorpro/commands/q.md), [r](/igorpro/commands/r.md), [s](/igorpro/commands/s.md) の現在の値を表示するようになりました。

- デバッガーは、メインスレッドから呼び出された [Threadsafe Functions](/igorpro/programming/programming.md#threadsafe-functions) に対して、ステップイン／ステップスルーを実行できます。

- 文字列と変数を最初の2つのパラメーターとして取るグラフスタイルマクロは、追加スタイルマクロとして使用できます：

    - グラフ名と、そのグラフ内に既に存在するトレースの数が渡され、残りのパラメーターは設定されません（[Missing Parameter Dialog](/igorpro/user-interface/dialog-help.md#missing-parameter-dialog) が表示される可能性があります）。
    - これらのパラメーターを持つグラフスタイルマクロをアペンドダイアログでどのように使用できるかについては、[Dialog Improvements in Igor Pro 10](#dialog-improvements-in-igor-pro-10) を参照してください。

- 関数とマクロの両方で、エスケープされた [Line Continuation](/igorpro/programming/programming.md#line-continuation)（行末記号）が単純な名前を２行に分割しない限り、ほぼどこでも行の継続がサポートされるようになりました。ただし、複合名の構成要素は連続する行に記述しても構いません。 

    ```igor
    // Compound name components can be on successive lines:
    Macro CallStaticFunction()
        Variable v1= MyModule#functionInMyModule() // usual syntax to call Static Functions
        // demonstrate a compound name with line continuation
        Variable v2 = MyModule \
                      #        \
                      functionInMyModule()
        Print v1,v2
    EndMacro
    
    // Line continuation can also be applied to a line-ending comment:
    Function [WAVE w] // output wave \
        Example4(String name,       // input: created wave's name \
                Variable length,    // input: # of points \
                Variable avg,       // input: mean value  \
                Variable noise)     // input: gnoise value
        Make/O/N=(length) $name \
                            = avg + gnoise(noise)
        WAVE w= $name
    End
    ```

- 出力リストにおいて、DFREF を [Multiple Return Syntax](/igorpro/programming/programming.md#multiple-return-syntax)（複数戻り値構文）と一緒に使用できるようになりました：

    ```igor
    [DFREF dfr] = MRSFunctionReturningDFREF()

    Function [DFREF df] MRSFunctionReturningDFREF()
        DFREF currentDF = GetDataFolderDFR()
        NewDataFolder/O currentDF:subfolder     // create a subfolder
        DFREF df = currentDF:subfolder          // and return a reference to it
    End
    ```

- [WaveHash](/igorpro/commands/wavehash.md) と [Hash](/igorpro/commands/hash.md) は、４つの xxHash アルゴリズムに加え、４つの SHA3 バリアントをサポートするようになりました。xxHash アルゴリズムは非暗号学的ハッシュアルゴリズムであり、サポートされている他のほとんどのアルゴリズムよりも大幅に高速で、その他の望ましい特性も備えています。これらのアルゴリズムに関する詳細は [xxHash](https://github.com/Cyan4973/xxHash/) を参照してください。

## Function and Operation Improvements in Igor Pro 10 {#function-and-operation-improvements-in-igor-pro-10}

- [GetFileFolderInfo](/igorpro/commands/getfilefolderinfo.md) は、S_languageAndCharsetList および S_versionInfo で Windows 専用のファイルバージョン情報を返すようになり、/LANG=languageCode /CSET=charSetCode フラグを受け付けるようになりました。

- [ListToTextWave](/igorpro/commands/listtotextwave.md) コマンド：新しいオプションの *keySepStr* が指定された場合（かつ "" ではない場合）、列 0 にキー、列 1 に値を格納した "key" および "value" の列の次元ラベルを持つ２列のテキストウェーブを返します。

- [IgorInfo](/igorpro/commands/igorinfo.md)(0) は各画面に対して SCALE=1 または 2 および RESOLUTION=*dpi* を返します。SCALE はディスプレイの拡大率を整数値で表したものです；Display Settings コントロールパネルで "Scale and layout" を 200% に設定すると、表示サイズは２倍になります。*dpi* は論理的な画面解像度（DPIとも呼ばれる）であり、Windows では通常 96 です。

- [IgorInfo](/igorpro/commands/igorinfo.md)(17) は、現在のエクスペリメントの起動コマンドと再実行マクロを返します。

- [IgorInfo](/igorpro/commands/igorinfo.md)(18) は、既存のエクスペリメントが終了しているという事実を返します。

- [FunctionInfo](/igorpro/commands/functioninfo.md)("") は、現在実行中の関数の情報を返すようになりました。

- [DoAlert](/igorpro/commands/doalert.md) および [Abort](/igorpro/commands/abort.md) で HTML を許可することでカラーサポートを追加しました。例えば：

    ```igor
    DoAlert 0, "<p style=\"color:red;\">This is red text.</p><p>Click <a href=\"https://www.wavemetrics.com/\">here to buy Igor</a>.</p>"
    ```

- [Printf](/igorpro/commands/printf.md), [sprintf](/igorpro/commands/sprintf.md) などの関数に、精度パラメーターを、%W0P や %W1P のように小数点以下の桁数ではなく、有効桁数の合計として解釈する新しい %W2P および %W3P オプションが追加されました。

    - フラグ桁 0 と 1 は、"%.\<precision\>W..." における精度値を、出力される数値の**小数部**の桁数として解釈します。フラグ桁 0 と 1 は Igor 10 以前からありました。

    - フラグ桁 2 と 3 は、"%.\<precision\>W..." における精度値を、出力される数値の**小数部と整数部**を出力するために使われる桁数の**合計**として解釈します。出力値は、%g が \<precision\> を解釈するのと同様にその桁数に丸められます。フラグ桁 2 と 3 は Igor 10 で追加されました。

    - **%W の例**
        ```igor
        printf "%.2W0PHz", 12.342E6     // prints 12.34MHz
        printf "%.2W1PHz", 12.342E6     // prints 12.34 MHz
        printf "%.0W0Ps", 12.342E-6     // prints 12µs
        printf "%.0W1Ps", 12.342E-9     // prints 12 ns
        printf "%.2W2PHz", 12.342E3     // prints 12KHz
        printf "%.4W3PHz", 12.342E3     // prints 12.34 KHz
        printf "%.2W2PV", -12.342E-3    // prints -12mV
        printf "%.4W3Ps", -12.342E-12   // prints 12.34 ps
        ```

- [Say](/igorpro/commands/say.md) テキスト読み上げコマンドを追加しました。

- [SplitWave](/igorpro/commands/splitwave.md) は、ソースウェーブからターゲットウェーブへスケーリングと次元ラベルをコピーするために /SCL=1 を受け付けるようになりました。

- [ImageTransform](/igorpro/commands/imagetransform.md) が /DEST フラグの使用をサポートするようになったため、ユーザーはコマンドの出力ウェーブを指定できます。/FREE も、ユーザー関数内で自由な出力ウェーブを生成するためにサポートされています。

- [ModifyImage](/igorpro/commands/modifyimage.md) に、画像の表示/非表示を切り替えるための *hide* キーワードが含まれました。

- [Display](/igorpro/commands/display.md), [Edit](/igorpro/commands/edit.md), [NewPanel](/igorpro/commands/newpanel.md), [NewGizmo](/igorpro/commands/newgizmo.md), [NewLayout](/igorpro/commands/newlayout.md), [NewNotebook](/igorpro/commands/newnotebook.md), [NewWaterfall](/igorpro/commands/newwaterfall.md), [NewImage](/igorpro/commands/newimage.md), [OpenNotebook](/igorpro/commands/opennotebook.md) コマンドは、ダイアログを表示せずにそれらのウィンドウを終了させ、エクスペリメントデータに保存されない、新しい /K=4 オプションをサポートします。

- [NewImage](/igorpro/commands/newimage.md) と [AppendImage](/igorpro/commands/appendimage.md) は、/PACK フラグを介したダイレクトカラー画像向けに 10 種類の新しいパッキングモードをサポートします。

- [SpecialDirPath](/igorpro/commands/specialdirpath.md) は、新しい "Igor Diagnostics" *dirIDStr* 文字列を使うことで、クラッシュのミニダンプやその他の診断情報を含むフォルダーの場所を返すことができます。

- [SoundLoadWave](/igorpro/commands/soundloadwave.md) は、μ-law、A-Law、AIFF および AIFC、WAVE、.mp3、.mpeg4 を含む、より多くの種類のオーディオファイルを読み込むことができます。

- [PlaySound](/igorpro/commands/playsound.md) は符号なし 8 ビットのサウンドウェーブを正しく再生します。

- [ImageLoad](/igorpro/commands/imageload.md) は、JPEG 圧縮を使用した TIFF ファイルの読み込みが可能になりました。このためには、ファイルを読み込む時に LibTIFF ライブラリを使う必要があります。詳細については、ImageLoad のドキュメントの /BIGT フラグおよび ***Loading TIFF Files*** セクションを参照してください。

- [PauseForUser](/igorpro/commands/pauseforuser.md) は、メインウィンドウまたはターゲットウィンドウの名前が正しくない場合のエラーメッセージを改善しました。現在、どのウィンドウが不正または欠落しているかを通知します。

- [TraceInfo](/igorpro/commands/traceinfo.md) は、CONTOURZWAVE キーワードの値として、トレースのコンター Z ウェーブの完全なパスを返すようになりました。トレースがコンタープロットに関連付けられていない場合、このパスは空になります。

## Data Browser Improvements in Igor Pro 10 {#data-browser-improvements-in-igor-pro-10}

- エクスペリメントをブラウズする時、ポイント列と次元列をオブジェクトリストに追加できるようになりました。これらのフィールドはオブジェクトリストに表示されていなくても、ソートすることができます。

- オブジェクトリスト内の区切り線をドラッグして列のサイズを変更すると、より良い結果が得られるようになりました。

## Window Browser Improvements in Igor Pro 10 {#window-browser-improvements-in-igor-pro-10}

- Window Browser は、設定されている場合、ウィンドウの名前のない、および名前の付いたウィンドウフックとツールチップフックを表示します。

## Dialog Improvements in Igor Pro 10 {#dialog-improvements-in-igor-pro-10}

- 「トレースを追加」および「カテゴリトレースを追加」ダイアログにグラフスタイルマクロのサポートを追加しました（Igor 10 以前では「表示」および「新規カテゴリプロット」ダイアログのみがグラフスタイルマクロをサポートしていました）。

- ユーザーが選択したスタイルマクロの個別の記憶を追加し、起動している Igor 間でも保持されるようにしました。これにより、ユーザーは希望する Display スタイルマクロと希望する Append スタイルマクロを一度だけ設定し、常にそれらを使用できるようになります。

- 選択されたスタイルマクロ（通常はパラメーターを持ちません）が２つ以上のパラメーターを持つ場合、**グラフ名とそのグラフ内の既存のトレース数が渡され、残りのパラメーターは設定されません**（これにより [Missing Parameter Dialog](/igorpro/user-interface/dialog-help.md#missing-parameter-dialog) が表示される可能性があります）。

- 「イメージの順序変更」ダイアログ（「イメージ」🠖「イメージの順序設定」）が複数の画像レイヤーに対応しました。[ReorderImages](/igorpro/commands/reorderimages.md) を参照してください。

## Graphing Improvements in Igor Pro 10 {#graphing-improvements-in-igor-pro-10}

- 画像プロットを表示するための第二レイヤーを追加しました。新しいレイヤーは、トレースと軸の上に画像を表示します。[Creating an Image Plot](/igorpro/graphing/image-plots.md#creating-an-image-plot), [AppendImage](/igorpro/commands/appendimage.md), [NewImage](/igorpro/commands/newimage.md), [ReorderImages](/igorpro/commands/reorderimages.md), [ImageInfo](/igorpro/commands/imageinfo.md) を参照してください。

- [NewImage](/igorpro/commands/newimage.md), [AppendImage](/igorpro/commands/appendimage.md), [ModifyImage](/igorpro/commands/modifyimage.md) コマンドにおいて、10 種類の新しい画像カラーパッキングモードのサポートを追加しました。

- ２つのカラーテーブルを追加しました：RedYellowGreen (256 colors) と RedYellowGreen10 (10 colors)。

- テキストマーカーのマーカースタンドオフを改善（[ModifyGraph](/igorpro/commands/modifygraph.md) mstandoff）しました。以前は、指定された非テキストマーカーに対してスタンドオフが計算されていました。スタンドオフはテキストの境界ボックスから計算されるようになりました。

- マーカーのスタンドオフは、マーカーのストロークの太さを考慮するようになりました。以前は、マーカーのストロークの太さ（[ModifyGraph](/igorpro/commands/modifygraph.md) mrkThick）の値が大きすぎると、マーカーのスタンドオフ用に確保されたスペースを圧迫していました。これにより、既存のグラフの外観にわずかな変化が生じる可能性がありました。

- マーカーのスタンドオフをポイント単位で適用できるようになりました（ [Customize at Point](/igorpro/graphing/graphs.md#customize-at-point) を参照してください）。

- グラフプレファレンスの useComma, useDotForX, useLongMinus は、グラフウィンドウの Capture Prefs ダイアログでキャプチャできるようになりました。

- [RemoveContour](/igorpro/commands/removecontour.md) が、新しい /Z（エラーを無視）フラグを持つようになりました。

## Box and Violin Plot Improvements in Igor Pro 10 {#box-and-violin-plot-improvements-in-igor-pro-10}

- [Box Plots and Violin Plots](/igorpro/graphing/graphs.md#box-plots-and-violin-plots) が、対数Y軸上にプロットできるようになりました。

## Table Improvements in Igor Pro 10 {#table-improvements-in-igor-pro-10}

- テーブルのコンテキストメニューに、Cut、Copy、Paste、Insert Paste、Clear のメニュー項目が追加されました。テーブル内で右クリックして使います。

## Page Layout Improvements in Igor Pro 10 {#page-layout-improvements-in-igor-pro-10}

- ページレイアウト内でガイドをドラッグすると、ウィンドウ下部のステータス表示にその位置が表示されます。印刷可能ページ幅または高さの分数が表示されます。Shift キーを押しながらドラッグすると、ガイドが印刷可能ページ幅または高さの整数倍に制限されます（ [Guides Mode for Laying Out Subwindows](/igorpro/graphing/making-figures/subwindows.md#guides-mode-for-laying-out-subwindows) を参照）。

- Ctrl キーを押しながらスクロールホイールを使うと、レイアウトの拡大率が変更されます。

- Shift キーを押しながら矢印キーでレイアウトオブジェクトを移動すると、移動速度が10倍になります。

## Notebook Improvements in Igor Pro 10 {#notebook-improvements-in-igor-pro-10}

- Ctrl キーを押しながらスクロールホイールを使うと、ノートブックの拡大率が変更されます。

- `Note`, `Warning`, `Caution` の記号に特殊文字を使用できるようになりました。Notebook🠖Special メニュー項目、またはルーラーツールバーの `Insert` ポップアップを使ってください。

## Help Improvements in Igor Pro 10 {#help-improvements-in-igor-pro-10}

- Ctrl キーを押しながらスクロールホイールを使うと、ヘルプ文書の拡大率が変更されます。

- Igor Pro 9 以降、Igor は起動後に XOP のヘルプファイルを開いたままにすることがありました。これはさほど重要ではありませんでしたが、追加のヘルプウィンドウが開き、「ヘルプ」→「ヘルプウィンドウ」のリストに余分な項目が追加されることを意味していました。これは Igor Pro 10 で修正されました。注意：XOP のヘルプファイルを意図的に開いた場合、ウィンドウは期待通り開いたままになります。

- Help Browser の "Help Topics" タブにあるトピック一覧で、 "Sort topics" がオフの場合、ヘルプトピックのリストが正しく順序付けされるようになりました。これは Igor Pro 7 以降、破損した状態でした。

## Graphics Export Improvements in Igor Pro 10 {#graphics-export-improvements-in-igor-pro-10}

- エラーバーが SVG 形式で正しくエクスポートされるようになりました。以前は、SVG 形式へのエクスポート時にエラーバーのクリッピングが正しく行われていませんでした。プロット領域の外側に描画されるべきエラーバーおよびエラーボックスが、生成された SVG 画像内に描画されていました。クリッピング処理が SVGエ クスポート時に正しく行われるようになり、Igor Pro でプロット領域外にあるエラーバーはエクスポートされた SVG 画像に表示されなくなりました。エラーシェーディングも SVG へのエクスポートは正しく行われ、この問題が発生しなくなりました。

:::note
エラーの省略記号は、SVG へのエクスポート時にも正しくクリッピングされません。必要な結果を得るには、プロット領域を拡大または縮小してください。
:::

## Procedure Window Improvements in Igor Pro 10 {#procedure-window-improvements-in-igor-pro-10}

#### Code Folding {#code-folding}
Procedure ウィンドウでコードの折り畳みがサポートされるようになりました。左マージンのコード折りたたみ矢印をクリックすると、コードブロックの表示/非表示を切り替えます。折りたたまれたコードブロックの右側にある省略記号インジケーターにマウスを合わせると、一時的に非表示のコードが表示されます：

<img src="MD_images/Whats_New_In_Igor_Pro_10/codeFolding_hoverIndicator.png" alt="Code Folding Hover Margin" width="40%"/>

複数のコードブロックを一度に折りたたんだり、展開したりできる右クリックメニュー項目があります。コードの折り畳みは、Misc🠖Miscellaneous Settings の Text Editing セクションでオン/オフを切り替えることができます。

#### Statement Completion {#statement-completion}
コマンドキーワードおよび特殊関数（例：MatrixOP や APMath）に対して補完候補が表示されるようになりました。様々なコンテキストにおけるコード補完の全般的な改善が行われました。

#### Syntax Highlighting {#syntax-highlighting}
コマンドキーワードに構文の強調表示が追加されました。設定は Misc🠖Miscellaneous Settings の Text Editing セクションで変更可能です。

#### Go to User Function {#go-to-user-function}
Ctrl キーを押しながらユーザー定義関数をクリックすると、その関数の定義の先頭に移動します。 

#### Scroll Magnification {#scroll-magnification}
Ctrl キーを押しながらスクロールホイールを使うと、Procedure ウィンドウの拡大率が変更されます。

#### Persistent Function Hints {#persistent-function-hints}
Procedure ウィンドウ下部のステータスバーに表示される関数のヒントは、関数やコマンド呼び出しの引数を入力している間も消えなくなりました。

#### External Editors {#external-editors}
Procedure ウィンドウのステータスバーに追加された新しいツールアイコンにより、プロシージャファイルに関連付けられたファイルを外部のテキストエディターで簡単に開くことができるようになりました。これは、スタンドアロンのファイルを表示している Procedure ウィンドウでのみ機能します。

## Gizmo Improvements in Igor Pro 10 {#gizmo-improvements-in-igor-pro-10}

- Gizmo シーンのマウスによる回転およびパン操作において、Shift キーを押したままにすることで回転軸/パン軸を固定できるようになりました。Ctrl キーを押すと、一時的に回転モードとパンモードを切り替えます。 

- 3D 散布図は、3D データを1つ以上の 2D 平面に「投影」する機能をサポートするようになりました。この投影は、Gizmo 散布図ダイアログで制御されます。この機能により、ModifyGizmo コマンドに projection、projectRGBA、projectMarkerSize プロパティが追加されました。

- 3D 散布図のマーカーの品質を、ModifyGizmo コマンドの quadricFacets プロパティを使って、ユーザーが直接カスタマイズできるようになりました。マーカーの描画に使われるファセット数は、'Shape and Size' タブの Gizmo 散布図ダイアログからアクセスできます。

- Gizmo ボックスオブジェクトは、立方体の各面に対して色プロパティ（faceColor）をサポートするようになりました。

- Windows ディスプレイ設定のスケーリング係数が 100% の非整数倍の場合の Gizmo 上の注釈の描画が改善されました。

## Drawing Improvements in Igor Pro 10 {#drawing-improvements-in-igor-pro-10}

- [DrawArc](/igorpro/commands/drawarc.md) コマンドに新しい /ORIG フラグが追加され、原点まで線を引いて円弧を完成させることができるようになりました。（弧に矢印がある場合、それらは依然として弧の曲線の最初または最後の点を指し、原点を指すわけではありません。）

- グラフに、注釈の上（前面）に描画する2つの新しい描画レイヤーが追加されました。2つのレイヤーは ProgTop と UserTop です。[Drawing Layers](/igorpro/graphing/drawing.md#drawing-layers) を参照してください。

- 各種描画コマンド（ [DrawLine](/igorpro/commands/drawline.md), [DrawRect](/igorpro/commands/drawrect.md) など）は、座標が Inf または NaN となる描画オブジェクトを作成しなくなりました。以前はそれがチェックされておらず、そのようなオブジェクトのコピーがクラッシュを引き起こしていました。

- [DrawPoly](/igorpro/commands/drawpoly.md) と [DrawBezier](/igorpro/commands/drawbezier.md) オブジェクトの編集時には、クリック位置の編集ヒントと、アンカーポイントやコントロールポイントの制約および形状の完成時に押下する修飾キーが表示されます。

- コントロールハンドルをクリックまたはドラッグするときに、Alt キーを押しながら、対応するコントロールハンドルとは独立して  [DrawBezier](/igorpro/commands/drawbezier.md) オブジェクトのコントロールハンドルをドラッグするとより簡単になります。このモードでは、マウスカーソルが特徴的な "convert control point" カーソルに変わります。

- [DrawPoly](/igorpro/commands/drawpoly.md) と [DrawBezier](/igorpro/commands/drawbezier.md) オブジェクトを「閉じる」（両端を結合する）ことはより簡単です；マウスカーソルが、十字カーソルに小さな円が追加された "close" カーソルに変化するようになりました。

- [DrawPoly](/igorpro/commands/drawpoly.md) と [DrawBezier](/igorpro/commands/drawbezier.md) オブジェクトの編集用に、コンテキストメニューをさらに追加しました。これには新しい "Complete Polygon" および "Complete Bezier" 項目が含まれます。編集モードでは、アンカー、コントロールポイント、またはセグメントを右クリックすると、これらのコンテキストメニューが表示されます。

- *commands* キーワードを持つ [DrawAction](/igorpro/commands/drawaction.md) は、描画オブジェクトが存在しない場合、*S_recreation* 文字列をヌル文字列ではなく、空文字列に初期化するようになりました。 また、*V_flag* を *S_recreation* 内のリストにある描画オブジェクトの数に設定します。

- [DrawPoly](/igorpro/commands/drawpoly.md) と [DrawBezier](/igorpro/commands/drawbezier.md) オブジェクトの再作成マクロは、NaN 座標が検出された場合に新しい行を開始するようになりました。これにより、ポリゴンやベジエ曲線のセグメントを識別しやすくなります。

- 同じ理由で、[DrawBezier](/igorpro/commands/drawbezier.md) オブジェクト再作成マクロは、最初のセグメントの4つのxy座標ポイント（開始アンカー、コントロールポイント１、コントロールポイント２、最初のセグメントの終了アンカー、次のセグメントの開始アンカー）を最初の行に配置し、続く各セグメントの3つの xy 座標ポイント（コントロールポイント１、コントロールポイント２、終了アンカー）を後続の行に配置します。

## Annotation Improvements in Igor Pro 10 {#annotation-improvements-in-igor-pro-10}

- 注釈、ラベル、およびコントロール内の [Annotation Text Escape Codes](/igorpro/graphing/annotations.md#annotation-text-escape-codes)（注釈テキストのエスケープコード）の解析中に、追加のエラーチェックを追加しました。

## Control and Control Panel Improvements in Igor Pro 10 {#control-and-control-panel-improvements-in-igor-pro-10}

- 可能な限り、制御用マクロでは coordinate.00 ではなく整数を使用してください；非整数座標は引き続き %.2f 形式を使います。

- コントロールパネル内で、レイアウトガイドを使用してコントロールを配置することが可能になりました。コントロールを使ったレイアウトガイドの使用方法については、[Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) を参照してください。以前はこれらのガイドラインを "subwindow guides" と呼んでいましたが、これらのガイドラインの適用範囲を拡大したため、現在は "layout guides" と呼んでいます。各コントロールには、レイアウトガイドに接続可能な６つのアンカーがあります。
これらのアンカーは、左、水平中央、右、上、垂直中央、下です。アンカーを１つ接続すると、移動するコントロールができ、接続されたレイアウトガイドが作成されます。
２つのアンカーを接続すると、許可されている場合、サイズ変更のコントロールが作成されます。

- 描画ツールパレットに "Guides Mode" の新しいボタンが追加されました。これによりレイアウトガイドを編集し、サブウィンドウやコントロールのレイアウトを制御するためにレイアウトガイドを使用できます。レイアウトガイド、ガイドモード、サブウィンドウに関する基本情報については、[Subwindow User-Interface Concepts](/igorpro/graphing/making-figures/subwindows.md#subwindow-user-interface-concepts) を参照してください。

- サブウィンドウのレイアウトガイドの使用方法については、[Guides Mode for Laying Out Subwindows](/igorpro/graphing/making-figures/subwindows.md#guides-mode-for-laying-out-subwindows) を参照してください。このヘルプトピックは以前、"Subwindow Layout Mode and Guides" という名前で存在していました。トピックタイトルの変更に伴い、明確化と新機能の反映のため、そのセクションを大幅に書き直しました。

- レイアウトガイドを使用してコントロールを配置すると、コントロールを適切に移動、サイズ変更したコントロールパネルの作成が格段に容易になります。例えば、ウィンドウのサイズ変更時に、コントロールパネルウィンドウの一定割合を占める [ListBox](/igorpro/user-interface/controls.md#listbox) コントロールを作成するのは非常に簡単です。

- Shift キーを押しながらガイドをドラッグすると、ドラッグしたガイドはパネルの幅または高さの最も近い有理数倍に制限されます。選択された分数はオーバーレイされたグラフィックで示されます。

- アクティブなサブウィンドウを作成する必要なく、レイアウトガイドの作成と編集が可能になりました。これは、コントロールのレイアウトガイドを編集できるようにするために必要です。

- コントロールのレイアウトガイドへのアタッチメントをサポートするため、各種コントロールコマンドに、コントロール上のレイアウトアンカーをレイアウトガイドにアタッチする指定のための "guides" キーワードが追加されました。例えば、[Button](/igorpro/commands/button.md) を参照してください。

- [ListBox](/igorpro/user-interface/controls.md#listbox) コントロールのセル内のチェックボックスと開示コントロールは、コントロールパネルの展開に正しく反応するようになりました。

- Igor Pro 9 に存在していたバグを修正しました：無効化されたセルを持つ ListBox コントロールは、マウスのクリックに応答しないため、マウスクリックで選択することはできません。ただし、無効化されたセル上でマウスをドラッグすると、そのセルが選択される可能性がありました。この抜け穴は現在修正されました。


## Analysis Improvements in Igor Pro 10 {#analysis-improvements-in-igor-pro-10}

- [IntegrateODE](/igorpro/commands/integrateode.md) コマンドにおいて導関数関数に静的関数を使用することが可能になりました。このプロシージャでは、Procedure ウィンドウは `ModuleName` の指定が必要で、関数名は完全な `ModuleName#FunctionName` で命名しなければなりません。[Procedure Modules](/igorpro/advanced-topics.md#procedure-modules) を参照してください。

- k>n の時に 0 を返すように [binomial](/igorpro/commands/binomial.md)(n,k) を変更しました。

- [Interp4D](/igorpro/commands/interp4d.md) と [Interp4DPath](/igorpro/commands/interp4dpath.md) 関数を追加しました。

## Statistics Improvements in Igor Pro 10 {#statistics-improvements-in-igor-pro-10}
- [WaveStats](/igorpro/commands/wavestats.md) のオプションパラメーターに、各種 V_ variables の生成および初期化を完全にバイパスする  /W フラグを追加しました。

## Matrix Improvements in Igor Pro 10 {#matrix-improvements-in-igor-pro-10}

- [MatrixOP](/igorpro/commands/matrixop.md) に以下の関数を追加しました：subtractMin(), indexMatch(), removeCol(), removeCols(), scaleLayers(), scaleChunks(), subtractRows(), subtractCols(), quatFromSpherical(), quatInverse(), median(), zapZeros(), replaceInfs(), enoise(), setType(), rowDiff(),
binMean(), binVar(), limit(), not()

- MatrixOP の整数変換関数を変更しました：uint8()、int8()、uint16()、int16()、uint32()、int32() は、NaN 入力に対して 0 を返し、+-INF に対して最大値/最小値を返します。

- MatrixOP コンパイルは、これまで実行時のみに報告されていたエラーをテストするようになりました。

## Multipeak Fitting Improvements in Igor Pro 10 {#multipeak-fitting-improvements-in-igor-pro-10}

Igorのパワーユーザーである Stephan Thürmer 氏（Igorフォーラムでのハンドルネーム「chozo」）の献身的な努力と寛大な貢献により、Multipeak Fittingパッケージは更新と改良を続けています。

- エラー処理の改善により、特に範囲外データ、空のウェーブ、NaN に関して、多くの領域で堅牢性が向上しました。

- ホールドストリングウェーブへの対応を追加しました。

- 100% および 200% の表示スケーリングが両方ともサポートされるようになりました。

- コピー/貼り付けのショートカットが、テーブル UI 内で直接使用可能になりました。

- 自動位置特定は、ゼロ幅ピークを返さなくなりました。

- 複数のアラートおよびエラーメッセージを改善しました。

## Image Processing Improvements in Igor Pro 10 {#image-processing-improvements-in-igor-pro-10}

- 2D ソース画像処理時に ROI ウェーブを無視していた [ImageSeedFill](/igorpro/commands/imageseedfill.md) を修正しました。

- /LTMD フラグを持つ [ImageLoad](/igorpro/commands/imageload.md) を変更し、タグテキストのウェーブが各行に１つ、タグの正式名称から始まるタグで構成されるようにしました。可能な限り、タグは昇順でリストされています。

## Data Import And Export Improvements in Igor Pro 10 {#data-import-and-export-improvements-in-igor-pro-10}

- [HDF5SaveData](/igorpro/commands/hdf5savedata.md) は多次元データの転置をより細かく制御するため、/TRAN=2 および /TRAN=3 をサポートするようになりました。特に、/TRAN=3 は自動マルチスレッディングを使用して実行を高速化します。

- HDF5 ライブラリが 1.14.6 に更新されました。BLOSC2 および ZSTD ダイナミックフィルタープラグインが追加されました。[HDF5 Dynamically Loaded Filters](/igorpro/data/igor-hdf5-guide.md#hdf5-dynamically-loaded-filters) を参照してください。

- [XLLoadWave](/igorpro/commands/xlloadwave.md) は、Excel 97-2003 ファイル形式（BIFF8）を使用する Excel ファイルから、非 ASCII のワークシート名を読み込むようになりました。

## Miscellaneous Improvements in Igor Pro 10 {#miscellaneous-improvements-in-igor-pro-10}

- UTF-8 テキストを含む文字列の解析と操作を支援するため、新しい [graphemeLength](/igorpro/commands/graphemelength.md) 関数と [UTF8CharLength](/igorpro/commands/utf8charlength.md) 関数を追加しました。[Characters Versus Bytes](/igorpro/igor-basics/text-encodings.md#characters-versus-bytes) も参照してください。

## New And Improved Packages in Igor Pro 10 {#new-and-improved-packages-in-igor-pro-10}
ヒートマップおよびデンドログラムパッケージ

- サブウィンドウ内でデンドログラムプロットを作成できるようになりました。

- アクセサー関数が提供されており、自身のコードからデンドログラムプロットを利用したいプログラマーを支援します。
これには、デンドログラム構造を保持する設定が含まれており、それらの構造を再利用して新しいデンドログラムを作成できるようになっています。

## New And Improved Example Experiments in Igor Pro 10 {#new-and-improved-example-experiments-in-igor-pro-10}

### Modified Example Experiments in Igor Pro 10 {#modified-example-experiments-in-igor-pro-10}

- 「ファイル」🠖「サンプルエクスペリメント」🠖Analysis🠖Spherical Triangulation Demo<br>
[SphericalTriangulationDemo.pxp](#igor-pxp/Examples/Analysis/SphericalTriangulationDemo.pxp)

### New Example Experiments in Igor Pro 10 {#new-example-experiments-in-igor-pro-10}

- 「ファイル」🠖「サンプルエクスペリメント」🠖Tutorials🠖Wave Scaling Tutorial<br>
[Wave Scaling Tutorial.pxp](<IgorPXP:Learning Aids:Tutorials:Wave Scaling Tutorial.pxp>)

- 「ファイル」🠖「サンプルエクスペリメント」🠖Python🠖Machine Learning  は、TensorFlow Python ライブラリを用いたシンプルな機械学習タスクを実演します<br>
[MachineLearningDemo.pxp](#igor-pxp/Examples/Python/MachineLearningDemo.pxp)