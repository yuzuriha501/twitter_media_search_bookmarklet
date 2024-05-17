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

# コード (省略なし)

適当。ID抽出して検索叩く。

```js
javascript:(() => {
    const path = location.href.split('/');

    // URLに反応して欲しくないページ階層
    const ignores = [
        'home',
        'explore',
        'notifications',
        'messages',
        'i',
        'communities',
        'search',
        'settings',
        'privacy',
        'tos',
        'compose',
    ];

    if (path[2].endsWith('twitter.com') || path[2].endsWith('x.com') && path[3]) {
        const id = path[3].split('?')[0];
        // 無視
        if (ignores.includes(id)) { return; }
        
        if (path[4]) {
            const sub = path[4].split('?')[0];
            if (ignores.includes(sub)) { return; }
        }

        // Twitter検索で "filter:media from:ユーザID" を実行してるだけ
        var url = 'https://x.com/search?f=live&q=filter:media%20from:' + id;
        window.open(url, '_blank');
    }
})();
```

# コード (省略あり)
ブックマークレットに登録するのはこれで
```js
javascript:(()=>{const path=location.href.split('/');const ignores=['home','explore','notifications','messages','i','communities','search','settings','privacy','tos','compose',];if(path[2].endsWith('twitter.com')||path[2].endsWith('x.com')&&path[3]){const id=path[3].split('?')[0];if(ignores.includes(id)){return} if(path[4]){const sub=path[4].split('?')[0];if(ignores.includes(sub)){return}} var url='https://x.com/search?f=live&q=filter:media%20from:'+id;window.open(url,'_blank')}})()
javascript:(()=>{let e=location.href.split("/"),i=["home","explore","notifications","messages","i","communities","search","settings","privacy","tos","compose",];if(e[2].endsWith("twitter.com")||e[2].endsWith("x.com")&&e[3]){let t=e[3].split("?")[0];if(i.includes(t))return;if(e[4]){let s=e[4].split("?")[0];if(i.includes(s))return}var o="https://x.com/search?f=live&q=filter:media%20from:"+t;window.open(o,"_blank")}})();
```

省略化に利用したサイト様: https://rakko.tools/tools/33/
他: https://www.toptal.com/developers/javascript-minifier

# 使い方

1. メディア欄を表示したいユーザを開く
2. 登録したブックマークレットを実行
3. 新しいタブが開き、メディアのみが検索結果に並ぶ
4. 満足

<br>
右クリックメニューにブックマークレットを自由に追加できるアドオンなどを利用すると便利になるかも <br>

FireFox ユーザの自分は以下で確認済み<br><br>
 Contextlets<br>
 https://addons.mozilla.org/en-US/firefox/addon/contextlets/

# おわりに
改変自由、ライセンス不要。

このソフトウェアには保証はついていません。<br>
このソフトウェアを利用したことで問題が起きた際に、ソフトウェアの製作者は一切の責任を負いません。<br>
