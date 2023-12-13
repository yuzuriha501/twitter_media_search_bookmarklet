# なにこれ？

X (旧Twitter) のメディア欄が、ある日突然イン○タみたいにタイル表示になってしまい <br>
前のように メディア と ツイート内容 がセットで確認できなくなり困ったのでその対策

# 対象
PC ブラウザ を想定<br>
スマホでも頑張れるブラウザならワンチャン

公式アプリは無理、諦めて

# 解決方法
「検索でそのユーザのメディアだけを表示すればいい」と気づいたのでそれを実行する<br>
呼び出し方法は ブックマークレット

※ブックマークレットとは？：便利なURLリンク (詳細は自分で調べて)

# コード (省略なし)

適当。ID抽出して検索叩く。

```js
javascript:(() => {
    const path = location.href.split('/');

    // ID
    if (path[2].endsWith('twitter.com') && path[3]) {
        const id = path[3].split('?')[0];
        var url = 'https://twitter.com/search?f=live&q=filter:media%20from:' + id;
        window.open(url, '_blank');
    }
})();
```

# コード (省略あり)
ブックマークレットに登録するのはこれで
```js
javascript:(()=>{const path=location.href.split('/');if(path[2].endsWith('twitter.com')&&path[3]){const id=path[3].split('?')[0];var url='https://twitter.com/search?f=live&q=filter:media%20from:'+id;window.open(url,'_blank')}})()
```

省略化に利用したサイト様: https://rakko.tools/tools/33/

# 使い方

1. メディア欄を表示したいユーザを開く
2. 登録したブックマークレットを実行
3. 新しいタブが開き、メディアのみが検索結果に並ぶ
4. 満足

# おわりに
改変自由、ライセンス不要。

このソフトウェアには保証はついていません。<br>
このソフトウェアを利用したことで問題が起きた際に、ソフトウェアの製作者は一切の責任を負いません。<br>
