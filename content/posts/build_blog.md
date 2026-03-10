---
title: "Build Blog" # 標題
date: 2026-03-10T20:26:00+08:00 # 發布時間
draft: false # 草稿
description: "我怎麼拼出這個網站的" # ani 摘要
summary: "A article about how I build my blog" # sim 摘要
author: "Linuk" # 作者

# can put many in
tags: ["blog"] # 標籤
categories: ["Daily", "Notes"] # 分類

math: true            # Latex 支援
toc: true             # 是否顯示目錄 (Anatole 支援)

# picture put in static/
# thumbnail: "icon.png" # Anatole
cover: "chisato.jpg"     # Reimu
---

> Warn: 沒意外會是流水帳

## Start
前天早上起來先問 Gemini 要用什麼模板去做，\
然後就跑去找 Hugo Themes 了\
挑超久、、、\
第一眼愛上(?) 的是 reimu\
宅味都流出來了ww 爽 這超我的\
還有像是 Terminal, Github Style 看起來也不錯但就是不想用 Github XD\
還看到了 Stack, 但可惜授權是 GPL-3.0-only 所以不是很想用\
順便發現 [Blameazu](https://blameazu.github.io/) 用的 Theme\
最後是選了 reimu 跟 anatole 的主題\
至於為什麼要兩個 因為第一個宅味真的太重了www\
沒想到要搞兩個 style 的 blog 居然這麼麻煩

### 建 anatole style
再來就真的是 AI 局\
前後大概問了快 100 次 Gemini 吧\
但 Claude 還是權威很多 orzorz\
簡單的使用 `hugo server --config hugo-sim.toml` 看了一下之後發現沒有 icon\
???wtf 我不是有寫進設定檔裡面了嗎\
問 Gemini 超多次的 還叫他去看 anatole 的 source code 結果好像根本沒看\
改去問 Claude 一下下就解決了 怎麼會有人欄位順序寫反阿...\
後來就一直用 Sonnet 了 幸好額度沒有用很快 ~~(是不是該買 pro 了阿)~~\
傳了第一篇測試文之後馬上發現問題了\
Table of Content 在混 放在最上面根本沒什麼用處\
因為怕 Claude 額度用完就先問 Gemini 結果變成浮動的\
位置也不是我想要的 真的頗浪費時間 ~~再不學網頁設計阿~~\
最後就決定直接跟 AI 說使用 Hackmd 的方式了 ~~幸好有範例可以抄~~\
再稍微手動調一下就完成了 耶\
最後加上 style change 的按鈕之後就跑去休息了\
這裡倒是沒有什麼大問題 ~~原來架網站也是簡簡單單分分鐘鐘阿~~

btw, anatole style 是 /sim/ 是取 simple\
reimu style 是 /ani/ 是取 anime

## 建 reimu style
這裡花了最多時間\
因為還要處理兩個 theme 之間的衝突\
像是不能用 config/ 要另外用開一個 config-ani/ 不然 anatole 會吃到 config 的設定\
reimu 本身的設定也很繁雜\
不能只用 hugo.toml 設定 還要再複製一個 params.yml 去改\
但是有打字效果很爽 放了中二的東西\
以及 anatole 是用 posts 彙整(這裡是 toml 設定的) 但是 reimu 是用 archives 有夠麻煩\
圖標也用了很久 因為預設不是採用 awesomefont 而是其他的\
且改成純 awesomefont 好像也有程式上的問題\
前後又叫 ai 改了很久 中間還一度想翻桌 (╯°Д°)╯( ┻━┻\
以及引導列的文字也是找了一些檔案才知道要怎麼改 ~~這設定方式也太躁了吧~~\
因為在 sample 上有看到可以播歌的功能 所以決定來試試看\
但因為設計這個 theme 的是中國人~~(毫不意外)~~ 所以用的是他們那裡的\
我想說要改成 youtube, 意識到有廣告問題就想要直接 hardcode 進去\
推上 github 之後才赫然想起有版權這回事 太晚想到了啦\
於是趕快撤銷之後想想其他辦法\
原本想直接用他預設的 結果沒有我要的歌 真可惜\
最後的解法是放到 cloudflare 上面用 public link 存取\
這裡又花了不少時間 (註冊 cloudflare R2 空間的部份w)\
我還是有注明歌曲出處ㄉ\

不得不說 千束好好看 ~~愛了愛了~~\
特別感謝 mkomko2022(雖然我不認識你) 的千束

貌似還有文章留言功能但是暫時不想處理了 :D


## End
### 404NotFound
在欣賞做好的頁面時 發現了 404 error page 好醜 用的是 github 預設的\
所以就決定自己寫(叫 AI 寫) 一個
就覺得既然都 404 應該不會又那麼多人遇到
所以就中二一點了 XD
因為想到中二就會想到闇影大人
所以就www 自己去看
特別爽 芙莉蓮也好棒
### 我是懶人
每次用 git add, git commit, git push 都好累
所以就使喚 AI 寫一個自動 push 腳本了
後來又覺得 article 的模板要複製好麻煩
又用 AI 寫一個自動初始化的出來了
我怎麼這麼強(懶)大(惰)

-# cover from: [うーたん＠FANBOX開始](https://www.pixiv.net/en/artworks/101490315)
