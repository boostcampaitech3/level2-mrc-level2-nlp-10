## 📋 Report

- [NLP] MRC 대회 WrapUP 리포트(PDF 파일 다운로드) : [MRC_NLP_팀 리포트(10조).pdf](https://github.com/boostcampaitech3/level2-mrc-level2-nlp-10/files/8732083/MRC_NLP_.10.pdf)

## 💯 Feedback

<details markdown="1"> 
<summary> <b>WrapUP 리포트 피드백 접기/펼치기</b> </summary>

<br/>

**오수지 멘토님**

wrap up report 피드백을 본격적으로 시작하기 앞서 다들 5주간 너무 수고 많으셨습니다! 첫 인사를 드렸던 게 엊그제 같은데 벌써 wrap up report를 받아보다니 감회가 정말 새롭네요..🥺 (해당 피드백은 노션으로 작성되어서 복붙해서 노션에서 보시면 더 가독성있게 보실 수 있을 것 같습니다!)

- EDA
- 표로 첨부해주신 text 길이 정보들도 histogram으로 그려보시면 좋을 것 같습니다! (표는 아무래도 정보가 직관적으로 들어오지 않은 면이 있어서요😢)
- Augmentation
- KorQUAD 1.0을 추가했을 때도, 대회 데이터로 Back Translation을 수행하셨을 때도 두 시도 다 성능 하락이 있었던 게 맞을까요? 그렇다면 정확히 어느 정도의 성능 하락이 있었는지, 왜 성능 향상을 보지 못했을지 이유도 팀원들과 함께 고민해보면 좋을 것 같습니다ㅎㅎ (면접에선 ‘왜 그런 결과를 보였을지'와 같이 정확한 답변이 존재하지 않는, 열린 질문을 많이 하시는 것 같습니다)
- 예를 들어, KorQUAD 1.0의 경우 질문이나 context의 길이가 대회 데이터의 길이와 다른 편인 것으로 알고 있습니다. 그 점이 모델이 학습하는데 있어 방해가 됐을 거라고 생각됩니다.
- Reader Model
- Figure에서 노란색이랑 초록색으로 표시된 부분은 무엇을 나타내는 걸까요...!?
- kernel size가 3인 Conv1d의 Output에 kernel size가 1인 Conv1d를 또 통과시킨 이유가 있을까요? 제가 1기 때 저희 팀에서 했던 실험에서도 kernel size가 1인 Conv1d를 활용하긴 했지만([https://www.ohsuz.dev/3e741502-5598-4f24-8e1e-9d7f362e4ebd](https://www.ohsuz.dev/3e741502-5598-4f24-8e1e-9d7f362e4ebd)), 저희의 경우 다양한 kernel size의 output을 concat해서 사용할 예정이라 기존 백본 모델 output의 정보를 보존하기 위해 사용했었습니다! 해당 구조에서 kernel size가 1인 Conv1d의 역할이 무엇일지 함께 고민해보면 좋을 것 같습니다ㅎㅎ
- 그리고 다른 대회에서 모델을 깊게 쌓을 일이 있으시면 추가 layer엔 drop out을 추가해보시는 걸 추천드립니다! (저같은 경우 drop out rate를 0.5로 세게 걸었을 때 가장 좋은 성능을 보였던 적이 있습니다 ㅎㅎ)
- 저같은 경우엔 AutoModelForQuestionAnswering이 어떻게 정답을 내는지 헷갈렸었는데 [https://mccormickml.com/2020/03/10/question-answering-with-a-fine-tuned-BERT/#part-1-how-bert-is-applied-to-question-answering](https://mccormickml.com/2020/03/10/question-answering-with-a-fine-tuned-BERT/#part-1-how-bert-is-applied-to-question-answering) 해당 페이지가 도움이 많이 되었습니다! 혹시 헷갈리시는 분은 참고해주세요ㅎㅎ
- 기원님께서 tokenizer 변경을 통해 다양한 실험을 진행하신 걸로 알고있는데 비록 성능 향상으로 이어지진 못했더라도 너무 상심하진 않으셨으면 좋겠습니다..! 어떤 목적을 가지고 실험을 함에 있어 issue가 발생하고, 해결하고, 다시 issue가 발생하고, 해결한 과정은 포트폴리오에 있어 정말 좋은 양분이 되거든요ㅎㅎ (그러한 issue가 없으면 오히려 할 말이 없어집니다...ㅠㅠ) 다만 최종적으로 성능 향상을 보이지 못한 실험의 경우, ‘왜 이 모든 시도들에도 불구하고 성능 향상으로 이어지지 못했을지'는 확실히 잡고 가시는 걸 추천드립니다!
- Ensemble
- Reader 모델의 경우 가장 성능이 좋았을 klue/roberta-large로 고정을 하셨는데, 비록 단일 모델로는 해당 모델이 가장 성능이 잘 나오겠지만 (제 경험상) 베이스 모델을 다양하게 해서 앙상블을 할수록 성능 향상을 확인할 수 있었습니다!
- 예를 들어, klue/roberta-large를 베이스로 이것저것 실험을 해서 낸 결과 A, B, C와, koelectra를 베이스로 이것저것 실험을 해서 낸 D, E, F를 비교해보면 A, B, C와 D, E, F 내에선 서로 예측값들이 크으으으게는 차이가 없는 걸 확인할 수가 있어요. 그래서 A, B, C를 앙상블 한다해도 결과가 크게 바뀌진 않습니다. 하지만 A, B, C ↔ D, E, F 사이엔 경향이 크게 다르기 때문에 앙상블을 했을 때 기존 결과들과 양상이 달라진(비록 이 양상이 성능 향상으로 이어질지는 미지수이지만) 결과를 확인할 수가 있습니다! 사람과 마찬가지로 모델들도 모델마다 잘 맞추는 문제가 다르더라구요ㅎㅎ 물론 앙상블에 ‘정답'은 존재하진 않지만 다음에 대회를 나가시게 된다면 다양한 베이스 모델을 활용해보시는 걸 추천드립니다!

추가적으로 강조드리고 싶은 부분

- wrap up report나 블로그에 수행했던 태스크를 정리할 땐 관련된 이미지를 첨부할 수 있으므로 비교적 본인이 한 일을 글을 읽는 사람들에게 이해시키는 것이 쉽다고 생각합니다. 하지만 면접에선 오로지 말로 설명해야하므로, 해당 태스크를 그 자리에서 처음 듣게 된 면접관님들을 제대로 이해시키는 것이 미리 준비하지 않으면 매우 어렵다고 생각해요. (제 경험담..) 엄청나고 멋진 일을 해도 그것을 제대로 설명해내지 못하면 말짱도루묵이므로 이렇게 wrap up report에 정리한 내용들을 팀원들과 서로 말로 설명하고, 이해시키는 연습을 면접 전에 꼭 해보시는 걸 추천드립니다!
- 그리고 포트폴리오 발표 면접을 보는 회사가 꽤 있어서 이렇게 정리하신 김에 본인이 기여하신 부분만 따로 ppt에 정리해보는 걸 추천드립니다! 이렇게 정리할 때 수학적인 수식은 [https://mathpix.com/](https://mathpix.com/) 사이트를 이용하시면 화질이 깨지지 않는 상태로 첨부할 수 있습니다ㅎㅎ(괜한 디테일..)
- 아마 멘토링 때 말씀드렸었던 것 같지만 한번 더 강조드리자면 사용하신 모델들에 대한 논문(RoBERTa, ELECTRA 등)은 한번이라도 제대로 리뷰해보시는 걸 추천드립니다! 면접에서 왜 그 모델을 사용했는지, 어떤 특징이 있는지는 반드시 물어보더라구요..

마지막으로, 지난 5주간 덕분에 너무 즐겁게 멘토링했습니다! 이번에 아쉬웠던 부분들도 물론 있겠지만 최종 프로젝트 진행하시면서 하나둘씩 보완하실 수 있을거라 믿어요ㅎㅎ 다들 수고 많으셨고, 남은 한달도 지금처럼 열심히 하셔서 모두 좋은 결과 있으시길 바랍니다~!👍🏻

</details>

<br/>

# 👋 팀원 소개
### Members
|김남현|민원식|전태양|정기원|주정호|최지민|
|:-:|:-:|:-:|:-:|:-:|:-:|
|<img src='https://avatars.githubusercontent.com/u/54979241?v=4' height=80 width=80px></img>|<img src='https://user-images.githubusercontent.com/73579424/164642795-b5413071-8b14-458d-8d57-a2e32e72f7f9.png' height=80 width=80px></img>|<img src='https://avatars.githubusercontent.com/u/55140109?v=4' height=80 width=80px></img>|<img src='https://user-images.githubusercontent.com/73579424/164643061-599b9409-dc21-4f7a-8c72-b5d5dbfe9fab.jpg' height=80 width=80px></img>|<img src='https://user-images.githubusercontent.com/73579424/164643280-b0981ca3-528a-4c68-9331-b8f7a1cbe414.jpg' height=80 width=80px></img>|<img src='https://avatars.githubusercontent.com/u/97524127?v=4' height=80 width=80px></img>|
|[Github](https://github.com/NHRWV)|[Github](https://github.com/wertat)|[Github](https://github.com/JEONSUN)|[Github](https://github.com/greenare)|[Github](https://github.com/jujeongho0)|[Github](https://github.com/timmyeos)|

<br>

# NLP 10조 ODQA 대회

### ○ 프로젝트 개요

- **프로젝트 주제**
    
    Open-Domain Question Answering (ODQA) 주어지는 지문이 따로 존재하지 않고 사전에 구축되어있는 Knowledge resource 에서 질문에 대답할 수 있는 문서를 찾는 Task
    
- **프로젝트 개요**
    - 프로젝트 목표
        
        사용자가 원하는 질문에 답변을 해주는 ODQA 시스템을 구축하는 것
        
    - 구현 내용
        - EDA
            - Jupyter Notebook을 이용하여 데이터 특성 분석
        - Data Processing
            - 정규식 및 한글 관련 라이브러리 활용하여 데이터 전/후처리 구현
            - 위키피디아 데이터 문단 단위로 분리 (DPR, BERTSerini 논문 참고)
        - Reader Model
            - pretrained model 에 cnn layer를 추가 시도
        - Retrival Model
            - Sparse Retrieval (BM25)
            - Dense Retrieval (논문참조, Dense Passage Retrieval for Open-Domain Question Answering)
        
    - 교육 내용의 응용
        
        사전 구축된 대규모 데이터를 이용해 ODQA 시스템 구축이 가능
        

- **활용 장비 및 재료**(개발 환경, 협업 tool 등)
    - 서버환경 : Ubuntu 18.04.5 LTS , GPUv100
    - 개발툴 : vscode, jupyter notebook
    - 협업툴 : Git, Github Project Slack, Zoom

- **프로젝트 File tree 및 Workflow**

### ○ 프로젝트 팀 구성 및 역할

- 김남현(T3021) : DPR+Reader Model 실험
- 민원식(T3079) : DPR 모델, BM25 구현 및 실험
- 전태양(T3194) :  EDA, retriever 관련 실험 진행
- 정기원(T3195) :  Data Processing, Tokenizer/MLM 관련 실험,  협업 환경 구축
- 주정호(T3211) : Reader Modeling & Fine-Tuning, Ensemble, Augmentation
- 최지민(T3223) : EDA, DPR(In-batch negative) 구현 및 Fine-Tuning

### ○ 프로젝트 수행 절차 및 방법

- **프로젝트 개발 Process**
    
    개발 과정을 아래와 같이 크게 5가지 파트로 분류함.
    
    - EDA : Jupyter Notebook을 이용하여 데이터 특성 및 이상치 분석
    - Data Processing : 모델 학습에 유용한 형태로 데이터를 처리
    - Modeling : 모델을 구현하고 성능 향상을 위해 Parameter Tunning 및 다양한 기능 추가
    - Model Test & Monitor : Monitoring Tool을 이용하여 모델을 다양한 환경에서 테스트
    - 협업 Tool 관리 및 기타(문서 정리) : Git Flow 적용

- **프로젝트 역할분담**
    
    모든 Process를 경험하고 싶다는 팀원들의 의견에 따라 팀원 별로 파트를 나누지 않고 모든 파트에 모든 팀원이 언제든 참여할 수 있도록 자유롭게 진행
    

- **프로젝트 수행 및 완료 과정**(Work Breakdown Structure)
    <img width="1058" alt="스크린샷 2022-05-12 오후 6 52 08" src="https://user-images.githubusercontent.com/62659407/169454384-fc992672-325e-40cc-931d-d6140311e039.png">    

### ○ 프로젝트 수행 결과

1. **EDA**
    - 데이터셋 구성
        ![Untitled (1)](https://user-images.githubusercontent.com/62659407/169454495-f94ce525-f755-47dc-ab9e-c6e38e55f2a6.png)
        
        **train** 
        ![Untitled (2)](https://user-images.githubusercontent.com/62659407/169454519-4d27fbc3-7348-4366-8999-a5493516ef6b.png)
        
        **validation**
        ![Untitled (3)](https://user-images.githubusercontent.com/62659407/169454591-db205737-4d9c-4439-acb0-5cfb1f337b5b.png)
        
        **test**
        ![Untitled (4)](https://user-images.githubusercontent.com/62659407/169454614-e57e18e8-6fb0-4aff-affc-9cc4bb0fef65.png)
        
        - context, question, answer 길이 모두 train, validation 데이터 유사
        - test 데이터의 question 길이 또한 train, validation 데이터와 유사
        
    - Context, Answer, Wiki 데이터셋 길이 파악
        - Context 내 Answer의 시작 위치 파악

    💡 Answer start 위치는 0~1974이며 대부분 문장의 앞부분에 분포했다.
  
    ![output1 (1)](https://user-images.githubusercontent.com/62659407/169454694-cd205ff4-445f-4624-a9b9-919a1c55b387.png)
    
    💡 Context, Answer 내 존재하는 특수문자
      1. 한문, 일어, 러시아어
      2. 개행문자 : \n, \\n, \n\n, \\n\\n                                                                                      
      3. 특수 개행문자 : *, **                                                                                                          4. 따옴표 : “, ‘
      5. 괄호 : 《》, 〈〉, ()
      6. 기타 문자 : ・, 『』, ⑥, ↑, ≪, ° ׁ, ç
    
    

- Retrieval 과정에서 사용하는 wiki corpus
    
    
    개수 및 text 길이
    ![Untitled (5)](https://user-images.githubusercontent.com/62659407/169454728-596a2099-e7d3-40e5-bca6-477b8ea2f224.png)
    
    예시
    ![Untitled (6)](https://user-images.githubusercontent.com/62659407/169454746-12628e27-a023-4481-a40a-f2b81f572391.png)
    
    - 중복을 제거하면 56737개의 unique한 문서로 이루어져 있음

1. **데이터 처리**
    - 전처리 (KoBERT clean 함수 참고)
        - 정규식을 활용하여 문장기호, ASCII문자, 한글, 히라가나, 가타카나, 한자, 영어를 제외한 문자 및 URL 주소형태의 문장을 제거
        - Soynlp 기능을 통해 ‘ㅋㅋㅋㅋ’와 같이 동일한 문자가 중복해서 발생하는 데이터를 제거
        - 전각 문자를 반각 문자로 치환
    - 후처리
        - utils_qa.py에서 정답을 기록할 때 Mecab을 활용하여 형태소 분리 후 한국어 불용어 사전을 통해 불용어를 제거한 값을 넣어줌
        - 한국어 불용어 사전은 [https://bab2min.tistory.com/544](https://bab2min.tistory.com/544) 참고하였음
    - Augmentation
        - KorQuAD 1.0
        - 학습 데이터의 Question을 영어와 일본어로 Backtranslation (Pororo의 Machine Translation 이용)
            
          ![1 (18)](https://user-images.githubusercontent.com/62659407/169454763-245073de-de8d-4032-bc26-46e0279d3a9c.png)    

            
        - 성능 비교
            - 학습 데이터만을 학습한 것보다 성능이 하락하였다.
    - 위키피디아 데이터 문단 단위 분리
        - DPR, BERTserini 논문에서 Retrieval 모델에 활용한 위키피디아 데이터를 문장 단위로 묶어 Passage에서 Paragraph로 데이터 단위를 축소할 때 성능이 향상된 것을 확인
        - 주어진 위키 데이터가 ‘\n’ 개행문자를 통해 문장을 분리하고 있어, 하나의 문단에 포함할 문장의 개수 및 최소 문단길이를 조절하며 실험
        - 실험 결과 문장 개수 = 5, 최소 문단길이 = 15로 설정할 때 EM, F1 값이 비슷하면서 예측값은 다른 경우를 발견하였음. 이를 앙상블에 활용함.

1. **모델 개요**
    - Reader Model
        - AutoModelForQuestionAnswering
            - Klue/bert-base
            - Klue/roberta-small
            - Klue/roberta-large를 이용해 학습 데이터를 임베딩
                ![1 (19)](https://user-images.githubusercontent.com/62659407/169454778-533dafe7-7c2a-461f-a3de-b9dd232a1de0.png)

        - CNN을 이용한 모델
            - Klue/roberta-large를 이용해 학습 데이터를 임베딩
                ![2 (2)](https://user-images.githubusercontent.com/62659407/169454799-28b34325-5ea7-4a7b-8a26-adb09a20ad3a.png)
                
        
        - 성능 비교(EM / micro f1)
            - **AutoModelForQuestionAnswering - Klue/roberta-large : 70 / 78.64**
            - CNN을 이용한 모델 : 67.91 / 78.76
            
        - Reader Tokenizer 교체
            - 허깅페이스에 등록된 토크나이저 및 Konlpy.tag 라이브러리(Mecab, KKma, Komoran)를 사용한 Reader 성능을 실험해봄.
            - 실험 결과 Klue/roberta-large 토크나이저의 성능이 제일 좋아 배제하였음.
        
        - Vocab 교체
            - Klue/roberta-large 토크나이저의 vocab을 교체하는 작업을 진행함.
            - Mecab을 활용하여 형태소 단위로 단어를 자르고 허깅페이스 토크나이저 학습 함수를 활용하여 새로운 32000개의 vocab을 제작하였음.
            - 성능은 미흡하여 원인을 분석하다 새로운 vocab을 사용할 경우 MLM을 통해 pretrain을 진행해야 되는 것을 알게 되어 후속실험으로 MLM을 진행함.
        
        - MLM 학습
            - Mecab을 통해 새로 구축한 Vocab을 적용한 RoBERTa 모델을 제작하기로 함.
            - fairseq 깃헙 게시물을 참고하여 진행
            - train+valid data, KLUE-MRC data 두 종류로 실험하였으나, GPU 성능 한계상 fairseq에서 제시한 실험 설정을 충족하지 못하여 성능이 미흡하였음.
        
    - Retrival Model
        - Spaerse Retrieval
            - TF-IDF
            단어의 등장빈도와 단어가 제공하는 정보의 양을 이용하여 벡터화된 passage embedding BoW를 구성
            - BM25
            TF-IDF의 개념을 바탕으로 문서의 길이까지 고려하여 점수를 산출
            - 토크나이저
                - sangrimlee/bert-base-multilingual-cased-korquad
                - monologg/koelectra-base-v3-finetuned-korquad
                - klue/roberta-large
            
        - Dense Retrieval
        사용자 Question과 찾고자 하는 Passage를 각각 Embedding하는 encoder 구현
            
            In-batch negative 방식 사용
            
            - Encoder Model
                - 실험 모델
                    - bert-base-multilingual-cased
                    - klue/roberta-base
                    - klue/bert-base
                - 토크나이저
                각 실험 모델별 기본 토크나이저 사용
                - KorQuAD 1.0 데이터로 추가 학습
    
    - Reader Model + Retrieval Mode 성능 비교(EM / micro f1)
        
        reader modeld를 동일한 환경으로 하였을때 아래와 같은 결과를 관찰함
        <img width="970" alt="스크린샷 2022-05-13 오후 5 16 29" src="https://user-images.githubusercontent.com/62659407/169454833-a83b9b31-e6a0-4520-8bf2-654d67a6b9f4.png">
        
        - Dense Retrieval 인코더 모델 간 비교
            - 총 3개의 인코더 모델(’klue/bert-base’ , ‘klue/roberta-base’, ‘bert-base-multilingual-cased’)을 사용함.
            - epoch 10인 ‘klue/bert-base’가 epoch 20인 ‘bert-base-multilingual-cased’ 보다 성능이 우수하여 인코더 모델로 선정함.
        - Sparse Retrieval 성능 비교
            - TF-IDF : ‘klue/roberta-base’와 ‘monologg/koelectra-base-v3-finetuned-korquad’의 성능이 비슷하였음
            - BM25 : ‘monologg/koelectra-base-v3-finetuned-korquad’의 성능이 가장 우수하였음
        - Dense Retrieval & Sparse Retrieval 비교
        참고 논문 ["Dense Passage Retrieval for Open-Domain Question Answering"](https://arxiv.org/pdf/2004.04906.pdf)의 내용을 구현해 보고자 하였지만 본 대회 실험 환경에서는 Sparse Retrieval가 더 나은 성능이 나왔음.

- SOTA 모델
    - Reader Model
        - Model
            - AutoModelForQuestionAnswering - Klue/roberta-large
        
        - Hyper Parameter
            - Learning Rate : 3.00e - 6
            - Batch Size : 8
            - max_seq_len : 512
            - Epoch : 5
            - Loss Function : CrossEntropy
            - Optimizer : AdamW
            - fp16 : True
    
    - Retrieval
        - BM25
        - 토크나이저 : monologg/koelectra-base-v3-finetuned-korquad

- Ensemble
    - Reader Model은 AutoModelForQuestionAnswering - Klue/roberta-large로 고정
    - Retrival Model
        - Tokenizer, top_k, 데이터 처리 방식으로 경우를 나누어 앙상블을 진행하였음.
        - 시간 제한 상 네 개의 모델에 대해 앙상블을 진행하였음.
    
    [앙상블 실험 테이블](https://www.notion.so/a6b4bf5b3c5e4c8790826e4abc8075ac)
    
    - 성능 비교
        - 단일 SOTA 모델에 비해 EM이 Public 2.9%, Private 6.7% 상승하였음 (Public: 55.83→58.75%, Private: 53.89→60.56)
        

### ○ 자체 평가 의견

- **프로젝트의 의도 및 달성 정도**
    - 프로젝트의 의도 : 사전에 구축되어있는 Wikipedia 에서 질문에 대답할 수 있는 문서를 찾고, 해당 문서에서 질문에 대한 답을 하는 인공지능 구현
    
    - 달성 정도
        - Public (11팀 中 6등)
            ![1 (20)](https://user-images.githubusercontent.com/62659407/169454860-d4dca96d-118c-466d-817d-f1fda94848b0.png)
            
        
        - Private (11팀 中 7등)
            ![1 (21)](https://user-images.githubusercontent.com/62659407/169454877-d486891c-e28a-4d53-b890-ede646b7fe09.png)
            

- **계획 대비 달성도, 완성도 등**(자체적인 평가 의견과 느낀 점)
    - 성능 향상으로 이루어지진 않았지만, 계획에 대해 대부분의 실험을 모두 수행하였다.

- **잘한 점과 아쉬운 점**(팀 별 공통 의견 중심으로 작성하며, 2~3장 분량을 고려하여 개인적인 의견은 개인 회고 부분에서 작성할 수 있도록 합니다.)
    - **잘한 점들**
        - 데이터 처리를 통해 앙상블 결과를 올렸다.
        - 비록 성능 향상으로 이루어지진 않았지만, 여러 외부 데이터를 이용한 Augmentation을 하여 실험해보았다.
    - **시도 했으나 잘 되지 않았던 것들**
        - ElasticSearch 모듈화를 시도했으나 잘 되지 않았다.
        - ["Dense Passage Retrieval for Open-Domain Question Answering"](https://arxiv.org/pdf/2004.04906.pdf) 논문 구현을 하였으나 GPU 메모리 한계로 인해 batch size를 늘리지 못해 논문 성능 재현이 되지 않았다.
    - **아쉬웠던 점들**
        - Reader의 성능을 많이 개선하지 못했다.
    - **프로젝트를 통해 배운 점 또는 시사점**
        - ODQA에서는 Retrieval의 성능이 매우 중요하다.
<br>

# ODQA 실행 화면

<img src="https://user-images.githubusercontent.com/97524127/169532321-a0b090d1-47e3-4a3f-85ad-29db4a544066.gif" height=500>
