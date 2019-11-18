---
layout: default
title: Document | dj.sugi studio
---

## Get Start
ベーシックなUIのライブラリです.  
インスペクタ上で簡単に設定できます.  
DOTWEENをラッピングしています.

[Releases - unitypackage download](https://github.com/sugichan0116/unity-ui-library/releases)



## Document

1. [Window.cs](#Windowcs)  
1. [UIAnimation.cs](#UIAnimationcs)  
1. [Tab.cs](#Tabcs)  
1. [ScrollList.cs](#ScrollListcs)  
1. [ContentContainer.cs](#ContentContainercs)  
1. [ContentUpdater.cs](#ContentUpdatercs)  


<br><br>

---

### Window.cs
基本的なウィンドウです.  
開閉のボタン操作やアニメーション、ポーズ機能を簡単に扱えます.

![window](img/window.gif)

#### Functions

|function|description|
|---|---|
|Open()|ウィンドウを開く|
|Close()|ウィンドウを閉じる|
|Toggle()|開いていたら閉じ, 閉じていたら開ける|

#### Property

![inspector](img/window_inspector.png)

<details>
<summary>Show detailed properties</summary><div>

|property|type|description|
|---|---|---|
|ShouldInactiveOnPlay|bool|アプリケーションを起動したとき<br>非アクティブにします|
|ShouldPauseOnOpen|bool|ウィンドウを開いたとき<br>時間を止めます(timeScale=0)|
|EnableEvents|bool|イベントを有効化します|
|OnOpen|UnityEvent|オープン時に呼び出されます|
|OnClose|UnityEvent|クローズ時に呼び出されます|
|Animations|UIAnimation[]|オープン・クローズ時に再生される<br>アニメーションを設定します|
|SearchAnimations|Function|自分や子供から`UIAnimation.cs`を検索し<br>Animationsに設定します|

</div></details>

<br><br>

---


### UIAnimation.cs
`window.cs`に設定するとアニメーションが再生されます.  
継承されたコンポーネントを利用すると簡単にアニメーションが設定できます.

#### Property

![inspector](img/animation_inspector.png)

<details>
<summary>Show detailed properties</summary>

|property|type|description|
|---|---|---|
|Development|bool|発展設定を有効にします|
|During|float|アニメーションの再生時間[sec]|
|SeparateDuring|bool|アニメーション時間をShowとHideそれぞれに設定します|
|ShowDuring|float|Show時の再生時間[sec]|
|HideDuring|float|Hide時の再生時間[sec]|
|InEase|Ease|Show時のイージングを設定します|
|OutEase|Ease|Hide時のイージングを設定します|
|CustomCurve|bool|イージングをアニメーションカーブで設定します|
|InCurve|AnimationCurve|Show時のイージングを設定します|
|OutCurve|AnimationCurve|Hide時のイージングを設定します|
|SetAnimation|Function|`UIAnimation.cs`を`Window.cs`に設定します|

</details>

#### Extention Class

|Component|description|
|---|---|
|UIAnimationCanvasGroup|CanvasGroupのAlpha値をアニメーションします<br>ウィンドウのフェード処理に用います|
|UIAnimationImage|ImageのColorをアニメーションします|
|UIAnimationSlide|Positionをアニメーションします<br>スライドイン処理が得意です|
|UIAnimationRotate|Rotateをアニメーションします|
|UIAnimationScale|Scaleをアニメーションします|


<br><br>

---

### Tab.cs
基本的なタブ.  
リンクされた`TabHeader.cs`から受けたインデックスを`ContentContainer.cs`に反映します.  
`ContentContainer.cs`は`ContentUpdater.cs`によって更新されます.  

![Tab](img/tab.gif)

#### property

![inspector](img/tab_inspector.png)

<details>
<summary>Show detailed properties</summary>

|property|type|description|
|---|---|---|
|HeaderContainer|ContentContainer|タブのヘッダーコンテナ<br>`TabHeader.cs`が子要素として認識される|
|ContentContainer|ContentContainer|タブのコンテントコンテナ<br>`UIContent.cs`が子要素として認識される|
|Selected|int|選択されているタブインデックス|
|NextTab|Function|次のタブへ移動|
|PreviousTab|Function|前のタブへ移動|
|LinkTabHeader|Function|ヘッダとコンテントをリンクします<br>実行前に必ずリンクしてください|

</details>

<br><br>

---

### TabHeader.cs
`UIContent.cs`に紐づけされた見出しです.  
`HeaderContainer`の子要素にしてください  
`SelectTab()`によって`Tab.cs`に更新を働きかけます.


#### Functions

|function|description|
|---|---|
|SelectTab()|ヘッダに紐づいたコンテントへ更新|

#### Property

<details>
<summary>Show detailed properties</summary>

|property|type|description|
|---|---|---|
|SelectTab|Function|ヘッダに紐づいたコンテントへ更新|

</details>


<br><br>

---


### ScrollList.cs
タブよりもたくさんの要素を管理します.  
ScrollBarによってリストをコントロールできます.

![Scroll](img/scroll.gif)

#### Property

![inspector](img/scroll_inspector.png)

<details>
<summary>Show detailed properties</summary>

|property|type|description|
|---|---|---|
|Bar|Scrollbar|リストのコントローラー|
|Container|ContentContainer|リストのコンテナ<br>`UIContent.cs`が子要素として認識される|
|Value|float|インスペクタ上でのスクロール位置|
|UpdateContent|Function|`Value`の位置にコンテントを更新する|
|NextContent|Function|次の要素へ移動する|
|PreviousContent|Function|前の要素へ移動する|

</details>


<br><br>

---


### ContentContainer.cs
たくさんのUI要素を格納するコンテナです.  
`Tab.cs`などの管理クラスに与えられた情報をもとに`ContentUpdater.cs`で要素の更新を行います.

#### Property

![inspector](img/container_inspector.png)

<details>
<summary>Show detailed properties</summary>

|property|type|description|
|---|---|---|
|Updaters|ContentUpdater[]|実行される`ContentUpdater.cs`のリスト|
|SetUpdater|Function|同オブジェクトの`ContentUpdater.cs`を検索して設定する|

</details>


<br><br>

---


### UIContent.cs
`ContentContainer.cs`の子要素に用いてください


<br><br>

---


### ContentUpdater.cs
与えられた情報からUI要素を更新します.  
継承されたコンポーネントを用いると自在なアニメーションが設定できます.


#### Extention Class

|Component|description|
|---|---|
|ContentBasicUpdater|選択された要素のみactiveにします|
|ContentHorizontalUpdater|水平方向に移動するアニメーション<br>`Spacing`を設定すると選択要素の前後に空白が挿入されます|
|ContentVerticalUpdater|垂直方向に移動するアニメーション<br>`Spacing`を設定すると選択要素の前後に空白が挿入されます|
|ContentPlaneUpdater|二次元の移動アニメーションを自由に設定できます<br>`IndexScale` 操作する要素の数<br>`Magnitude` 移動曲線の大きさ<br>`Movement Curve` 移動曲線(正規化)<br>`Curve Center` 選択要素の移動曲線上の位置|
|ContentImageColorUpdater|選択された要素をハイライトするImageのColorを設定します|
|ContentUnderlineUpdater|下線オブジェクトが選択要素の位置に伸びるように移動します|
|ContentHeroUpdater|選択要素のScaleを設定します|


<br><br>

---
