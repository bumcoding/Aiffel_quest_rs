# HuggingFace 커스텀 프로젝트

---

### 1. 프로젝트 목표
- 모델과 데이터를 정상적으로 불러오고, 작동하는 것을 확인하였다.
- Preprocessing을 개선하고, fine-tuning을 통해 모델의 성능을 개선시켰다.
- 모델 학습에 Bucketing을 성공적으로 적용하고, 그 결과를 비교분석하였다.


### 2. 평가 기준
- klue/bert-base를 NSMC 데이터셋으로 fine-tuning 하여, 모델이 정상적으로 작동하는 것을 확인하였다.
- Validation accuracy를 90% 이상으로 개선하였다.
- Bucketing task을 수행하여 fine-tuning 시 연산 속도와 모델 성능 간의 trade-off 관계가 발생하는지 여부를 확인하고, 분석한 결과를 제시하였다.


### 3. Bucketing & Dynamic Padding
- 새 변환 함수 transform_no_pad()
  - padding=False, truncation=True, max_length=128로 사전 패딩 제거.
  - 동일하게 s1=document, s2="" 유지해 베이스라인 인터페이스 고정  
- Data Collator:
  - DataCollatorWithPadding(tokenizer=..., pad_to_multiple_of=8)
  - 배치가 만들어질 때 그 배치의 최장 시퀀스 길이에 맞춰 동적 패딩 적용 → 패딩 낭비 최소화.


### 4. 관찰한 Trade-off 관계
- 고정 패딩
  - 장점: 구현 간단, 데이터로더/배치가 일정해 디버깅 쉬움
  - 단점: 패딩 낭비가 많아 속도가 매우 느리고 메모리를 많이 차지함
- 동적 패딩
  - 장점: 고정 패딩에 비해 속도가 빨라졌고 메모리를 적게 차지함
  - 단점: 배치 길이가 때마다 가변적이라 디버깅이 약간 복잡함

### 5. 시행착오 & 해결 포인트
- load_dataset("nsmc")가 막혀 GitHub TSV를 csv 빌더로 직접 로드했음
- label이 Value 타입 > ClassLabel로 캐스팅 후 train_test_split(..., stratify_by_column='label')
- TrainingArguments 인자 호환성: 환경에 따라 evaluation_strategy 등 최신 환경을 지원하지 않음 > default로 기존 lms 상의 코드를 참조함



### 6. 결과
| 설정                                     | Validation Acc |    Test Acc |           학습 시간 |
| -------------------------------------- | -------------: | ----------: | --------------: |
| 고정 패딩 (`padding='max_length'`) | 0.9132 | 0.9050 | 2:45:17 |
| 동적 패딩 (Bucketing & Dynamic Padding)              |    | |  |



### 회고
- 우선 nsmc 데이터를 전체 학습하는데 시간이 매우 오래걸렸음 > 기본적으로 한 에포크 돌리는데 1시간 씩 걸리는 수준이라 절망스러웠다. (early stop이 필요할 듯)
- Bucketing을 사용했을 때 크게 Acc가 변하지 않았으며 오히려 초반 Acc는 미세하게 줄었음 > 정확도 면에서는 크게 차이를 못느꼈다.
- 그나마 속도가 확실이 Bucketing을 했을 때 빠르다는 점이 장점이었음 > 속도면에서 그래도 이점을 확인해서 사용할 수 있는 경우에는 Bucketing을 쓰는 게 좋아보였다.

