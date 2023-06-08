---
layout: post
title: "Android 이론"
subtitle: "Android 이론 공부."
date: 2023-06-03
background: ''
categories:
  - Android
tags:
  - IT
  - Android

---

# 안드로이드 이론공부

## 안드로이드란

- 구글에 의해 개발되고 배포되는 오픈소스 플랫폼
- 리눅스 기반 운영체제로 리눅스 커널위에 자바 코드로 작성된 애플리케이션을 실행하는 가상머신이 탑재됬다.
- 어플리케이션 프레임워크를 통해서 제공되는 API를 사용함으로써 코드를 재사용하여 효율적이고 빠른 어플리케이션이 개발가능하다.
- 모바일기기에 최적화된 달빅 또는 아트런타임 제공
- 2D 그래픽 및 3차원 그래픽을 최적화하여 표현
- Android Studio를 통해 강력하고 빠른 개발환경 제공
- 롤리팝(5.0)부터는 다양한 안드로이드 기기를 통합 지원

## 안드로이드 특징

- 다양한 통신환경 및 센서 지원
- 오픈소스
- 다양한 미디어 포맷 지원
- 런타임 라이브러리 제공
- Java언어 기반 손쉬운 App개발
- 우월한 이식성으로 다양한 기기에 적용

## 안드로이드 아키텍쳐

<img src="https://github.com/YonggyuCho/YonggyuCho.github.io/assets/127103253/73e9d287-d938-40fb-9676-4682f9f51b4e" width="500" height="300">

- 리눅스 커널
- 하드웨어 추상화 계층
- 네이티브 라이브러리
- 안드로이드 런타임
- 안드로이드 프레임워크
- 어플리케이션

### 리눅스커널

- 안드로이드는 리눅스 커널위에 만들어졌지만 안드로이드가 리눅스는 아니다
- **핵심적인 시스템 서비스들을 제공하며, 프로세스, 메모리, 전원 관리, 네트워크, 드라이브, 보안 등의** 내용을 포함
- 표준 리눅스 도구를 모두 제공하지 않는다.
- 안드로이드 커널도 공개되어 있다.
- 보안 : 하드웨어와 프로세서의 보안을 담당
- 자원관리 : 한정된 시스템 자원을 효율적 관리, 프로그램의 실행을 원만하게 수행하도록 한다.
- 추상화 : 커널은 운영체제의 복잡한 내부를 감추고 일관성 있는 인터페이스를 하드웨어에 제공하기 위해 같은 종류의 하드웨어에 대한 공통 명령어 집합인 추상화들로 이루어짐
- 하드웨어 드라이버 : 카메라, 블루투스 등 각종 하드웨어를 제어하는데 필요로 하는 명령어 모음인 드라이버들을 포함
- 전력관리(Power Management) : 전원을 끄거나 비활성화 하는 등 Wifi/Bluetooth/CPU/GPU 등 하드웨어 공급되는 전력을 관리


### 하드웨어 추상화 계층

- 다소 복잡한 하드웨어를 감추고 일관성 있는 인터페이스를 제공하기위해, 같은 종류의 하드웨어에 대한 공통 명령어 집합으로 묶었다 이를 **추상화**라한다.
- 프로그래머가 여러 장비에서 개발하는것을 도와준다.

### 안드로이드 런타임

- 기계어가 아닌 하나의 바이트코드로 여러가지 CPU와 플랫폼 환경에서 구동되기위해 가상머신(달빅, 안드로이드 런타임)이 사용된다
- 달빅을 사용하느냐 ART을 사용하느냐에 따라 동작하는 형태도 달라진다.
- 안드로이드2.2부터 달빅에 JIT(Just In Time)이 추가됨으로써 성능적 향상은 엄청난 차이가 보였다.
- 하지만 문제점도 생겼다(배터리소모, 메인메모리 관리 문제 등)
- 이를 해결하기위해 ART이 등장 하지만 ART에도 단점이 있다.
- 안드로이드 7.0 부터는 앱 설치시간을 단축하기 위해서 최초 설치시에는 JIT를사용, 충전중이거나 기기를 사용하지 않을 때, 즉 대기모드 상태일 때 일부분컴파일 작업을 실시하여 점진적으로 AOT방식으로 바꾸어 나가도록 되어있음

### 네이티브 라이브러리

- ART 및 HAL 등 많은 핵심 안드로이드 시스템 구성요소와 서비스는  C/C++로 작성된 네이티브 라이브러리를 필요로 하는 네이티브 코드 기반으로 이루어져 있다.
- 안드로이드는 JAVA 프레임워크 API를 이용, 일부 네이티브 라이브러리기능을 앱에 제공하고 있음
- 코드의 보안이나, 성능을 필요로 하는 경우, C/C++ 코드가 필요로하는 NDK(Native Development Kit)을 이용, 네이티브 코드에서 직접 여러가지 네이티브 플랫폼 라이브러리에 접근할 수 있음

### 안드로이드 프레임워크
- 안드로이드에서 제공하는 애플리케이션도 애플리케이션 프레임워크의 API에 기반한 경우가 많다
- 간단한 재사용 컴포넌트, 어떤 애플리케이션과도 호환 가능한 호환성을 제공

- 액티비티 관리자 (Activity Manager) : 애플리케이션의 라이프사이클을 제어함
- 내용 제공자 (Content Provider) : 애플리케이션 간에 데이터를 공유할 수 있도록 함
- 리소스 관리자 (Resource Manager) : 코드 이외의 부분인 리소스를 관리함
- 위치 관리자 (Location Manager) : 자신의 위치 파악에 필요한 기능을 제공함
- 알림 관리자 (Notification Manager) : 알림 기능을 사용자에게 방해가 되지 않도록 제공함

### 어플리케이션
- 안드로이드는 이메일/ SMS 메세지 / 캘린더 / 인터넷 브라우저 / 주소록 등 주요 애플리케이션 세트와 함께 제공된다.
- 플랫폼에 기본적으로 포함된 앱은 사용자가 선택하여 설치하는 어플리케이션과 특별한 구분이 없어 설정 등 일부 어플리케이션을 제외하면 설치된 다른 어플리케이션이 기본 어플리케이션으로 지정가능
- 시스템 어플리케이션은 사용자가 직접 사용하는 용도도 되지만, **개발자가 자신의 앱에서 접근할 수있는 주요 기능을 제공하기위한 용도로 사용됨**
- 예를들어 SMS 어플리케이션 같은 경우 개발자가 기능을 직접 만들필요없이, 시스템 앱에 내장된 SMS 어플리케이션을 호출하여 데이터를 주고받아 지정한 사람에게 메세지를 전달가능

## APK

- Android Project에서 컴파일과 패키징 과정을 거치면 AndroidPackage 파일이 생성된다.
- Signing 과정을 거치면 단말이나 AVD로 만들어진 에뮬레이터에 설치가능한 APK가 최종적으로 생성

### APK 파일 생성 3단계

#### 컴파일
- CPU가 이해할 수 있는 언어로 바꿔주는과정
- 원시코드에서 기계가 이해할 수 있는 `.dex`파일로 변환
#### 패키징
- 앱이 동작하기 위한 파일을 포장
- APK내의 여러 파일을 보호하고 배포하기 편하게 관리
#### 서명
-  APK 위변조를 방지하기위해 서명 정보 저장







