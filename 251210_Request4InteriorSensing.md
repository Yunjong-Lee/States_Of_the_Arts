---
date: 2025-12-10 13:43:02
layout: post
---


# RFI @BMW  
- Basis system : nudernath the rear-view mirror, 1 camera
- High Option B : , 2 cameras, One camera from the basis system and one TOF camera in the function center roof  

    ## Camera System  
- camera is integrated in the rear-view mirror base cover underneath the rear-view mirror.
- RGB-IR at 940nm, 160º/120º(HFOV/VFOV), 5MP, 60fps

    ## SW Features
    ### driver  
#### 1) Driver Monitoring System  
- Drowsiness:  
  + Characteristics
       * eye : open/closed
       * head position
       * signs showing drowsiness : body posture, yawning, gestures (hands in the face/on eyes), level of drowsiness (attentive, drowsy, fall asleep, sleeping, ...)
  + KPI: at least every 200ms (t.b.d)

- Distraction:  
  + Visual distraction (driver/co-driver) : Gaze tracking, head position  
    * Characteristics : Eyes, pupils(iris), head position, gaze direction
    * KPI
      - Detection of gaze direction : "Eyes on road" regions accuracies 
        ※ zones for gaze accuracy : 5º/7.5º/10º (시야각을 의미하는 것 같음, 각이 좁을 수록 멀리 응시...)
      - Eyes on road? → Yes/ No
  + Cognitive/ Manual distraction: Passenger activity recognition
    * driver가 driving 동안 (딴짓...) 하고 있음  
    * Characteristics : Eating, drinking, smoking, use of external or internal devices, interaction with any objects, detection of hand and arm  
    * KPI : at least every 200ms (t.b.d)  

#### 2) Availability of driver/ADAS  
: falling asleep, failure due to health problems (recognition of unconsciousness, recognition of cramps (epileptic shock)), influenced by alcohol, drugs etc. (detecting whether the driver is on the driver's seat and not sleeping.)   
: All features of driver must be detected up to a head turning of min. +/-30° in „yaw“ from the longitudinal axis of the vehicle.  
: Eyes/drowsiness level can be detected while driver is looking on his lap (e.g. mobile phone) → t.b.d.  
- Characteristics
  * Seat occupancy
  * drowsiness/overall condition (unconsciousness?)
  * distraction (of hands)
  * head pose and gaze vector
- KPI : at least every 200ms (t.b.d)

#### 3) Hands on Wheel Detection  
: At least one hand needs to be at the steering wheel (or also close to it → time to take over!). 
: holding something in his hands 상태태 감지 (Distance (hand-steering wheel) 감지는 case dependent함). 
- characteristics : position of hands, close to steering wheel, detection of object in hands
- KPI : tbd  

#### 4) Child Presence Detection  
: children in in-cabin are detected and reminds to the driver.  
- characteristics : child seat/child seat + child/Child seat + blanket
- KPI : tbd  

    ### passenger  
- 앞좌석에 유아용 카시트가 설치되어 있는지 감지
- in-cabin에서 passenger 감지 
  + passenger 감지 : seat belt usage check 
  + passenger 미 감지 : → animal(dog/cat) 감지 → 카시트+child
   감지  
- 움직임이 감지되지 않으면 : empty

#### 1) SBR (Seat belt reminder)  
- characteristics : seat belt usage
- KPI : tbd  

#### 2) Classification of passengers  
: passengers classification  
  + possible conditions : empty/occupied(person)/child seat empty/child seat occupied/child seat occupied unknown object  
: 앞좌석 승객의 차이 (Differentiation on passenger), €NCAP/FMVSS 208 참조 
  + empty seats/child seats + child/person(size of 5% woman or larger)    
- KPI : tbd  

#### 3) "Body Part Tracking" out of position and Cocoon Airbag (High Option B)  
: head, upper body, arms and legs are positioned in the interior (body part tracking) → Skeleton tracking.  
: The body volume and clothing is detected and weight is estimated.  
- KPI : tbd  

    ### Natural Interaction
#### 1) lite
: Natural Interaction “lite” (gesture only)  
   → Fist, arm, open/close, swipe, rotate, rock-paper-scissors  
- KPI 
  * The coordinates of all determined reference points must possess a precision of at least 1cm. 
  * The precision must be established in 95% of the recorded scenes. Gestures must be recognized in less than 60ms and must be send in less than 20ms after being recognized. 
  * The system must be able to detect all gestures at any lighting condition amongst others at darkness, direct sunlight or at quickly changing lighting conditions. 
  * Rate of false identification: max 0.5 false identifications per hour. If a hand is not located in the space of interaction no false identifications are allowed to occur. 
  * Non-identification rate (Quotient of number of cases in which the system does not identify a gesture and number of cases in which this gesture was performed): < 5%  

#### 2) full  
: high accuracy gaze tracking and finger vector(High Option A)  
: basis of interpersonal communication  
: Gestures, gaze and language are combined → Interaction with displays, cockpit, surrounding.  
- KPI : tbd

    ### Customer Functions  
#### 1) Entertainment  
: Snapshot and Video Call function.  
- KPI : Resolution/color matching/distortion/illumination  
#### 2) Face Recognition  
: face authentication, anti-spoofing, iris-detection?  
: gender can be detected  
: classification of age is possible (Baby, child, teenager and adult) with an estimated age indication  
: various clothing conditions (incl. caps/ hats, burkas, costumes (e.g. masks), glasses, wigs).  
: Animals must be distinguished from persons. Facial emotional expressions can be recognized as well as child mimic detection.  
- KPI (검토 필요)
  * Passengers can still be recognized when moving on their respective seat and turning their heads +/- 45° in reference to the optical axis of the camera.  
  * The feature recognition must be able to analyze images with up to 50% occlusion of the faces. 
  * All implemented algorithms have to be able to work with quickly varying lighting conditions. 
  * All implemented algorithms have to be able to perform the same using RGB or IR images (grey values). Algorithm estimating categorical emotions has to achieve a recall and precision of 98% per class. False positives < 2%. Algorithm estimating continuous affect has to achieve concordance correlation coefficient of 0.96 on valence and arousal.  

#### 3) Object Detection  
: Various objects and animals can be identified  
- KPI : Classifier accuracy/ detection accuracy > 99% and false positive rate < 1%.  

#### 4) Health: Vital Sensing (High Option)  
: Heartbeat rate, respiratory rate  
- KPI 
  * 5 ~ 10% (medical devices)  
  * Accuracy > 85%/false positives < 1%.

#### 5) Smoke detection  
- KPI : detection accuracy > 99% (false positive rate < 1%)  

    ### AR HUD (High Option B)  
: image projection  
- KPI : tbd

    ## Conceptual Questions  

- Can the software features be partitioned in different functions? What is the most efficient software architecture for having all this features on one soc?  
  ㅁ.1. 소프트웨어 기능을 여러 기능으로 분할할 수 있다. 모든 기능을 하나의 SoC에 구현하기 위한 가장 효율적인 소프트웨어 아키텍처는 radar soc에서 신호처리를 담당하고 point cloud or detection result를 통합 soc로 보내어 dcu 등으로 보내는 방법이 효율적

- Comparison of gaze direction in Basis and High System: what precision is possible in Basis System, how much improvement can be achieved in the High Option A?  
  ㅁ.1. 기본 시스템과 고급 시스템에서 시선 방향 감지 비교: 기본 시스템에서 가능한 정밀도는 어느 정도이며, 고급 옵션 A에서는 얼마나 개선될 수 있습니까?  

- Is a detection of pointing vector possible in the basis system?  
  ㅁ.1. 기본 시스템에서 포인팅 벡터 감지 가능함.
  ㅁ.2. 레이더에서는 function에 따라 포인팅 벡터 대신 point cloud를 출력한다.  

- ASIL conformity, what is needed for ASIL A or B?  
  ㅁ.1. ASIL A/B 인증을 받기 위해 필요한 사항은 ...

- How to handle the scheduling of the processor for all the functions?  
  ㅁ.1. 레이더에서 프로세서 스케줄링은 rtos에서 수행 (task scheduling)
  ㅁ.2. 레이더 출력은 멀티스레딩을 활용하여 cycle하게 시리얼 통신 수행

- Is it expected to have issues switching between several “deep networks” applications concerning the runtime behavior?  
  ㅁ.1. machine learning을 활용하여 features를 추출하고 그 결과(weighting factor)를 code화하여 사용중이므로 “deep networks” apps. 간 전환 시 런타임 동작과 관련하여 문제는 발생하지 않을 것으로 예상

- Do you have certain expectations regarding the picture quality during day/night?  
  ㅁ.1. 레이더는 lighting에 의한한 performance degradation point가 없으므로 주야간 화질에 대한 특정 기대치는 없으며, 동일한 expected value를 가짐  

- Do you see risks to porting from your framework to BMW target platform? 
  ㅁ.1. semco radar에 대한 SW 프레임워크는 radar soc에 embedded되므로로 BMW 타겟 플랫폼으로 포팅할 때 위험 요소는 거의 없을 것으로 예상되지만, 혹시 rist point가 발생될 때를 대비하여 cross check가 필요할 것 같음  

- Can you handle the integration of automotive software in a given ECU like the BMW Head Unit? 
  ㅁ.1. BMW 헤드 유닛과 같은 특정 ECU에 radar 구동에 필요한 SW 통합은 선택적으로 가능할 것 같지만, 통합이 어려운 부분도 있음.
























