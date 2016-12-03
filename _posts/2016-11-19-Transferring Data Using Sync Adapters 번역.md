---
layout: post
title:  "Transferring Data Using Sync Adapters 번역"
date:   2016-11-19 11:57:00 +0700
categories: [번역]
---
## 목차

* toc
{: toc}

## 개요
지금 진행하고 있는 안드로이드 프로젝트에서 RSS를 읽고 데이터를 다뤄야하는 기능이있다. 그래서 RSS를 Parsing하는 Library를 찾다가 Android Developer site에서 BaseSyncAdapter라는 예제를 찾았는데 간단한 코드가 아니여서 설명을 살펴봤다.

```
This sample demonstrates using SyncAdapter to fetch background data for an app that doesn\'t require a user-visible account type or 2-way synchronization. \n\nThis sample periodically downloads the feed from the Android Developer Blog and caches the data in a content provider. At runtime, the cached feed data is displayed inside a ListView.
```
```
이 예제는 User-visible account type 또는 2-way synchronization을 요구하지 않는 앱에서 사용할 백그라운드 데이터를 받아는 SyncAdapter를 사용하는 데모이다.
이 예제는 주기적으로 안드로이드 개발자 블로그와 CP(Content Provider)에 있는 캐시로부터 feed를 다운받는다. 실행시에 저장된 feed 데이터는 내부 ListView에 보여진다.
```

이 설명만으로는 뭐하는 예제인지 알 수 없어서 중요한 키워드라고 생각된 SyncAdapter를 검색했더니 [Transferring Data Using Sync Adapters](https://developer.android.com/training/sync-adapters/index.html) 이런 링크가 나왔다. SyncAdapter에 관한 내용인것 같아서 이것을 번역하며 공유한다. 워낙 영어를 못하니까 이런거라도 하면 영어실력이 늘지 않을까싶다. 틀리거나 이상한 번역이 있으면 지적해주시길 바랍니다.

## SyncAdapter를 이용한 데이터 전달
안드로이드 디바이스와 웹서버가 데이터를 동기화 하는것은 유저들에게 앱을 상당히 유용하고 눈을 뗄 수 없게 한다.예를들어, 웹서버에 데이터를 전송하면 백업에 도움이 된다. 그리고 서버에  전송한 데이터는 유저의 디바이스가 인터넷에 연결이 안됐을 때도 이용할 수 있다.어쩌면, 유저는 웹 인터페이스 안에서 그들의 데이터를 쉽게 들어가고 수정하고는 그들의 디바이스에서 데이터를 이용할 수 있다. 또는 그들은 데이터를 수집해서 중앙 저장공간에 업로드하길 원할지 모른다.

비록 너가 앱에 데이터를 전달하는 시스템을 설계할 수 있더라도 너는 Android’s sync adapter framework의 사용을 고려해야한다.이 Framework는 관리하고 데이터 자동전송을 도와준다. 그리고 다른앱과도 동기화 연산을 조절한다.이 Framework를 사용할때 너는 데이터 전송 몇가지의 스키마를 설계할 필요가 없는 특징의 이점을 볼 수 있다. 


Plug-in architecture(Plug-in 구조)

*   호출할 수 있는 컴포넌트의 형태에서 시스템에 데이터 전송 코드를 더하는것이 가능하다.

Automated execution(자동 실행)

* GPS상황, 변화하는 데이터 추가, 경과시간, 시계가 가리키는 시간들을 기반으로 데이터 전송을 자동화 하는것이 가능하다.게다가, 시스템은 큐에 돌릴 수 없는 전송을 추가해뒀다가 그것들이 가능할때 돌린다. 

Automated network checking(네트워크 자동 체크)

*   그 시스템은 네트워크에 연결됐을 때만 데이터를 전송한다.

Improved battery performance(향상된 배터리 성능)

*   한 곳의 앱의 데이터 전송 일의 모든것을 중앙집권이 가능하다. 그래서 모든것을 같은 시간에 실행한다.너의 데이터 전송은 또한 다른 앱으로부터 온 데이터 전송과 함께 conjunction에서 스케쥴된다. 이 요인들은 시스템이 네트워크에 전환되야하는 횟수를 줄인다. 그래서 배터리 사용을 줄인다.

Account management and authentication(계정관리와 인증)

*   만약 너의 앱이 사용자의 자격 이나 서버의 로그인을 필요로한다면 데이터 전송안에 추가적으로 계정관리와 인증을 추가할 수 있다. 

> 참고 : Sync adapters는 비동기방식이다. 그래서 효율적이고 규칙적으로 데이터전송의 기대에 맞춰 사용해야한다. 하지만 순식간이진 않다. 만약 실시간으로 데이터전송을 할 필요가 있다면 AsyncTask나 IntentService를 사용해라.

## 과정
[Creating a Stub Authenticator][Creating a Stub Authenticator]

*   account-handling 컴포넌트를 어떻게 더하는지 배운다. 이 과정에서는 간단한 stub 인증 컴포넌트를 어떻게 만드는지 보여준다. 

[Creating a Stub Content Provider][Creating a Stub Content Provider]

*   CP(Content Provider) 컴포넌트를 어떻게 추가하는지 배운다. 이 과정에서는 너의 앱이 CP를 사용하지 않는것으로 가정한다. 그래서 어떻게 stub 컴포넌트를 추가하는지 보여준다. 만약 앱에 CP가 이미 있다면 너는 이 단계를 넘어가도 된다.

[Creating a Sync Adapter][Creating a Sync Adapter]

*   SyncAdapter Framework가 자동적으로 실행할 수 있는 컴포넌트에서 어떻게 너의 데이터 전송 코드를 압축하는지 배운다.

[Running a Sync Adapter][Running a Sync Adapter]

*   SyncAdapter Framework에서 어떻게 데이터 전송을 작동시키고 스케쥴 하는지 배운다.

[Creating a Stub Authenticator]: https://developer.android.com/training/sync-adapters/creating-authenticator.html
[Creating a Stub Content Provider]: https://developer.android.com/training/sync-adapters/creating-stub-provider.html
[Creating a Sync Adapter]: https://developer.android.com/training/sync-adapters/creating-sync-adapter.html
[Running a Sync Adapter]: https://developer.android.com/training/sync-adapters/running-sync-adapter.html