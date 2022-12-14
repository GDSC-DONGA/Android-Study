# Chapter 01
### 스마트폰의 개요
  - 스마트폰: 통화기능 + 컴퓨터 + 다양한 기능 내장(MP3, 카메라, DMB, GPS 등)
  - 스마트폰 운영체제의 전세계 점유율(2019기준)
    - 안드로이드 85%, 아이폰 11%, 윈도폰 0.01%

### 안드로이드의 개요
- 안드로이드
  - Google이 2007년 안드로이드사를 인수
- 안드로이드의 주요 기능
  - 애플리케이션 프레임워크를 통해 제공되는 API 사용 -> 코드를 재사용해 효율적이고 빠른 애클리케이션 개발 가능
  - 모바일 기기에 최적화된 달빅 또는 아트런타임 제공
  - 2D 그래픽 및 삼차원 그래픽을 최적화하여 표현
  - 모바일용 데이터베이스 SQLite 제공
  - 각종 오디오, 비디오 및 이미지 형식 제공
  - 모바일 기기에 내장된 각종 하드웨어 지원(블루투스, 카메라, 나침반, WiFi 등)
  - eclipse IDE, Android Studio를 통해 강력하고 빠른 개발환경 제공
- 안드로이드 특징
  - 안드로이드 핵심 커널(Kernel)은 리눅스(Linux)로 구성
  - 안드로이드 개발 언어: Java, Kotlin
  - 안드로이드 SDK에서 많은 라이브러리 포함하고 있어 개발 용이
  - 오픈소스 지향
  - 지속적 업그레이드 제공
- 안드로이드 구조
  - ![안드로이드 구조](https://user-images.githubusercontent.com/101886039/198874406-2f4ba246-ca3a-4b87-9660-723fe5172b7e.png)
  1. 응용 프로그램(Applications)
      - 사용자 입장에서 가장 많이 사용
      - Java, Kotlin으로 제작
  2. 응용 프로그램 프레임워크(Application Framework)
       - 안드로이드 API가 존재하는곳
       - 안드로이드폰 하드웨어에 접근할 때 API를 통해서만 가능
  3. 안드로이드 런타임(Android Runtime)
        - JVM을 사용하지 않고 이곳의 달빅 가상 머신이나 아트런타임을 사용
  4. 라이브러리(Libraries)
        - 시스템 접근 때문에 C로 작성
  5. 리눅스 커널(Linux Kernel)
        - 하드웨어의 운영과 관련된 저수준의 관리 기능
        - 메모리 관리, 디바이스 드라이버, 보안 등
