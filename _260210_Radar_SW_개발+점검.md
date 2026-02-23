---
date: 2026-02-10 11:09:58
layout: post
---

# Radar SW 개발 및 점검  
- 단계별 점검 → Simulation 기반 점검 → 신뢰성 Test 순으로 진행한다  

## 단걔별 점검 (V-모델 기반)  
- 요구사항 분석 및 설계
- Algorithm Simulation 및 검증
  + parameter 정의 : Carrier Frequency, BW, pulse repeatation frequency, pulse width, ...
  + Waveform generation : chirp or Barker code
  + Environment Modeling
    * target 위치/속도/RCS, clutter, noise modeling
    * 송신된 신호가 공간을 거쳐 표적에 반사되어 돌아오는 과정(Delay, Doppler Shift) modeling 
  + Algorithms : 펄스 압축, FFT(도플러 처리), CFAR(표적 탐지), 클러터 제거 알고리즘 등  

- Code 분석_정적 분석 : LDRA나 Polyspace를 주로 사용
  + 라이센스
    * LDRA(방산 및 항공 분야(DO-178C 표준 등)에서 주로 사용), VectorCAST, Coverity, CodeSonar, Polyspace 
  + 오픈소스
    * Cppcheck
    * Clang Static Analyzer (LLVM 컴파일러 기반의 도구)
    * SonarQube Community Edition (코드 품질 관리 플랫폼, 유료)
    * Infer (META에서 개발, Null 포인터 참조나 리소스 누수)

- 단위 test, 통합 test  

## Simulation 기반 점검  
- Scenario 기반 가상환경에서 Algorithm 검증  
  + RadarSimPy (python 기반 open source simulator)
- Simulation data를 활용하여 데이터 신호처리 점검

## 신뢰성 Test를 통한 성능 점검
- 동적 test
  + 탐지확률, 오경보율 (몬테카를로 simulation)


# Simulator
- [RadarSimPy](https://github.com/radarsimx/radarsimpy) : FMCW 파형 모델링, DOA estimation 기능 지원






