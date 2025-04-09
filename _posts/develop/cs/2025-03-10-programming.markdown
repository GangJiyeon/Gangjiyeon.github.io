---
title: "프로그래밍 기초"
excerpt: "프로그래밍 언어"
categories:
  - cs
tags: [프로그래밍]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---

# 프로그래밍 언어

|세대|구분|
|---|---|
|1세대 언어|• 기계어(machine language)<br>• 0, 1의 이진수로 구성된 언어<br>• 컴퓨터의 CPU는 기계어만 이해하고 처리|
|2세대 언어|• 어셈블리어<br>• 기계어 명령을 ADD, SUB, MOVE 등과 같은 표현하기 쉬운 상징적 단어인 약식기호(mnemonic symbol)로 바꾼 언어 -> needs 어셈블러|
|3세대 언어 (3GL)|• 고급언어<br>• 사람이 이해하기 쉽고, 복잡한 작업, 알고리듬, 자료 구조를 표현
하기 위해 고안한 언어-> needs 컴파일러/해석기(interpreter)<br>• Pascal, Basic, C/C++, Java, C#, Python, Matlab<br>• ‘절차’ 지향 언어와‘객체’ 지향 언어로 구분|
|4세대 언어 (4GL)|• 4세대 언어는 3GL 보다는 자연어에 좀더 가깝게 설계<br>• SQL(Structured Query Language), Lotus, Delphi 등과 Visual Basic, Visual C++, Power Builder 등|
|5세대 언어|• 언어라기 보다, 인공지능 분야의 원리를 사용하는 시스템을 위해 개발된 언어<br>• 지식기반시스템, 전문가시스템, 추론기관, 자연어 처리<br>• 복잡하고 방대한 지식을 분석, 조합하여 컴퓨터가 추론을 수행<br>•  사용자가 원하는 바를 서술하면 시스템이 요구 사항을 구현<br>• 주로 제한조건들을 명시해주는 것만으로 문제 해결을 가능케 한다 (알고리듬, 코드를 직접 구현할 필요 없다)<br>• 1979년 Winograd가 5세대 언어의 특징을 구체화 함: 아직까지 존재하지 않는다?<br>•  GPT-3, AlphaCode? – Transformer 기술 기반|



# 프로그래밍 
> 프로그램 만드는 과정<br>
• 원시 파일(원본,source) : 프로그래밍 언어로 작성된 텍스트 파일<br>
• 컴파일(번역, compile) : 원시 파일을 컴퓨터가 이해할 수 있는 기계어로 만드는 과정

• 자바 : `.java` -> `.class`<br>
• C : `.c` -> `.obj` -> `.exe`<br>
• C++ : `.cpp` -> `.obj` -> `.exe`

소스 프로그램: 설계, 편집 및 개발 > 원시 프로그램 > 컴파일러 > 기계어 > 프로그램 실행