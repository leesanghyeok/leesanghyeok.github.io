---
layout: post
title:  "Android Studio 팁"
date:   2016-11-20 11:57:00 +0700
categories: [Android,Tool]
---
## 목차

* toc
{: toc}

## 개요
---
Android Studio를 이용하는 팁을 정리한 문서

## 팁
---

### Show Line Number 
짜고있는 코드가 몇번째 줄인지 눈여겨 보지는 않지만 에러가 발생하면 몇번째 줄에서 발생했다고 알려준다.
물론 링크가 걸려있어서 클릭하면 해당 라인으로 포커스를 맞춰주지만 이것만으로는 부족하다.
그래서 코드 옆에 라인을 표시해주는 옵션이 대부분에 IDE에서 기본적인 설정이다.
무슨 이윤지 Android Studio에서는 기본적인 설정이 아니라 설정을 해줘야한다.   
설정방법으로 지속적인 설정과 임시적인 설정이 있다.
두가지 설정방법을 알아보자.

> Android Studio의 기반인 IntelliJ 역시 마찬가지다.

#### 임시적인 설정
임시적인 설정은 Android Studio를 재시작하면 설정이 풀린다. 하지만 설정이 간단해서 금방 확인할 수 있다.
파일 탐색기 오른쪽, 코드 부분의 왼쪽 회색 공간에 오른쪽마우스를 클릭하면 아래 이미지와 같이 나온다.
**Show Line Numbers**를 클릭하면 설정이 완료된다.

![line-number-easy](https://raw.githubusercontent.com/leesanghyeok/leesanghyeok.github.io/master/static/img/_posts/line-number-easy.png){: .center-image }

#### 지속적인 설정
지속적인 설정은 Android Studio를 재시작해도 설정이 유지된다.
```
설정 경로 : File - Settings - Editor - General - Appearance
```

**Show Line Numbers**를 클릭하고 OK를 누르면 설정이 완료된다.

![line-number-easy](https://raw.githubusercontent.com/leesanghyeok/leesanghyeok.github.io/master/static/img/_posts/line-number-complex.png){: .center-image }

### .jar 파일 추가하기 정리 필요
Android Studio에서 외부 라이브러리를 추가하려면 Gradle을 이용하는것이 일반적이다.
하지만 최근에 외부 라이브러리를 수정하고 싶어서 소스를 따로 컴파일해서 추가하려는 시도를 했다.
꼭 이런 상황이 아니더라도 외부 라이브러리를 추가하려면 .jar파일을 프로젝트에 넣어야 한다.

일반적으로 ```app - build.gradle```에 이런 코드가 있다. 없으면 추가하자.

```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
}
```

그리고 프로젝트 최상위 경로에 ```libs```라는 폴더를 만들어서 .jar 파일을 넣는다.
다시 Android Studio롤 돌아오면 프로젝트 탐색기에 .jar파일이 생겼을 것이다.
그 파일을 오른쪽마우스로 클릭하고 ```Add As Library```를 눌러서 확인해라.

