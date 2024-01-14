---
layout: single
title:  "RAG for document"
categories: LLM,RAG,document,gpt 4 vision, streamlit, gpt4
tag : [LLM,RAG,document,gpt 4 vision, streamlit, gpt4]
toc: true
author_profile: false
sidebar:
  nav : "docs"
search: true
typora-root-url: ../
---



# 소개 



**Together team 프로젝트 내용 및 목적** : 개인의 데이터에 대한 지식을 바탕으로 내용을 물어보거나  적절한 답변을(요약 및 개념 설명 포함) 하는 프로그램 만들기



**기간** : 2023-10 ~ 2023-12



**구성 환경 및 사용 기술** : colab환경에서 진행 하였고 llm은 open ai llm을 사용한다. UI는 streamlit을 사용했다. open ai llm을 사용했지만 번역을 위해 파파고 api도 같이 사용했다. 



**결과** : 짧은 기간안에 구현 예정이었던 기술을 모두 마무리 할수있었기 때문에 좋은 결과를 얻었다고 생각한다





**프로젝트 팀원 성찰** : 나를 포함해서 총 2명에서 진행한 프로젝트였다. 팀원간에 팀워크는 긍정적이었다. 작업 분배와 의견 제시 등등 원할하게 이루어졌고 소통도 잘 되었다. 그리고 무엇 보다 혼자 작업 하는게 아니라 같이 작업을 하는 느낌이 들었기 때문에 상당히 만족스러웠던 팀이었다. 



-------

# 프로젝트 기능 및 어려웠던 점 및 해결과정





### RAG pipeline 


![service arichtecture image]({{site.url}}/images/2024-01-10-LLM_for_Recommend_system/image-20240112002228970.png)



일반적으로 RAG시스템에서 사용되는 유사도 기반의 검색이 아니라 다음과 같은 pipeline을 통해 검색 속도 향상 및 Reranking을 통해 가장 의미론적으로 높은 문서를 indexing할수있다. (이를 위해 cohereRerank를 사용한다 langchain에서도 지원 다만 open ai llm에서만 작동됨 라마2나 다른 llm에서 그대로 사용하면 안되고 변형해야 한다 CustomCohereRerank)



### multi Query Retriver 

사용자의 질문과 유사한 질문을 뽑아내는 과정에서 



```python
def generate_queries(question):
    
    text = multi_qa.generate_queries(question=question, run_manager = CallbackManagerForRetrieverRun(run_id = 'runid', handlers = [],inheritable_handlers = [] ) )
    
    return text 
```

다음과 같이 구성 하여 뽑아 낼수도 있다 하지만 streamlit에서 구현 할때 버튼을 눌렀을때 진행 하는 방식과 파파고 번역도 같이 사용해야 하였기 때문에 위에 방식 보다 logging 정보에서 추출하는 방식으로 구성했다. 



### Agent 구성 

prompt는 기본으로 제공하는 React로 구성하였다. React 기반으로 사용자의 질문이 pipeline으로 작동해야 하는지 아니면 duckduckgo search로 작동해야하는지(google search로 해도 됨 duckduckgo는 google같은 웹서비스이다) 판단할수있게 함으로 써 개인 자료 안에 없는 질문을 했을때 대처 하도록 하였다. 





**어려웠던 점 및 해결 과정**: 처음에는 개인 자료 기반으로 RAG시스템 만들었었다. 하지만 피드백 과정에서 이미지나 테이블에 대해서도 같이 적용하는 방향도 고려 해보는것이 좋을것 같다는 피드백을 받았었다. 우리 프로젝트에서 개인 자료가 pdf등등도 있지만 논문 pdf를 주 자료로 생각을 했었다. 논문에는 이미지 뿐 아니라 테이블에 대한 정보도 같이 있는데 pdf loader에서는 이미지에 대한 설명이나 테이블을 인식 할수 없었기 때문에 처음에 문제 해결 방식에서 고민이 있었다. (pdf 이미지, 테이블 정보를 분석할수있는 RAG시스템을 구축하는게 목표로 전환됨)



고민 과정에서 첫번째로 나온 해법은 보통 논문에서 이미지는 figure 1,2..이런식으로 있는데 질문을 할때 figure1에 대해서 설명해줘 같이 명시적으로 같이 작성을 해주면 pdf에서 관련 내용을 찾을 것으로 예상을 하고 진행했었다. 하지만 실제로 실행 해 보았을때는 실행 할때마다 결과가 달라서 조금 애매 했었다. 이 방법을 그대로 가져 가면서 추가적으로 보완하는 방법이 더 필요한 시점이었다. 그래서 보완할 방법으로 gpt 4 vision모델을 사용해서 이미지 정보를 같이 넘기고 분석 하게 하자는 아이디어가 제시 되었고 이 방법을 적용하여  문제를 보완하기로 하였다. 

그리고 근본적으로 실행할때마다 결과가 달라지는 문제를 해결하기 위해 multi query QA를 사용하기로 하였다. multi query를 통해 사용자가 질문한 질문과 유사한 3가지 질문을 생성 할수가 있따. 

예로 figure1에 대하여 설명해줘 같은 질문을 했을때 관련 설명이 없다거나 엉뚱한 대답이 나온다면 multi query가 만든 유사한 3가지 질문지에서 다시 선택하여 결과를 받을수있었다. 

그래서 정리를 하자면 이미지와 테이블에 대한 정보를 같이 처리 하기 위해 gpt 4 vision모델을 같이 사용함과 동시에 multi query QA를 이용해서 유사한 질문을 생성하여 보완 하였다. 



그리고 streamlit에서 새 질문 적용 버튼 눌렀을때  새 질문이 적용하지 않는 문제가 있었는데 

```py
if 'session_state' not in st.session_state:
    st.session_state.session_state = {"selected_text": None, "tuple_data": []}


```

위에 처럼 seestion state를 나누어서 처리 해야 함을 알게 됨으로 써 해결 할수있었다. 





### 구현 기능 

1. 사용자가 입력한 질문과 유사한 질문 3가지를 선택할수있는 기능 

2. 사용자가 이미지 업로드한 거에 대한 질문 할수있는 기능 

3. 개인 데이터 이외에 질문을 했을때 인터넷 기반으로 검색 할수있는 기능 

4. 사용자가 질문하고 생성한 대답에 대해 (최근 10개) 요약하여 출력하는 기능 

   





-----



# 마무리 및 아쉬운점 



다음 깃헙 주소에서 코드를 확인할수 있습니다 

[meang123/RAG_for_document (github.com)](https://github.com/meang123/RAG_for_document)



**아쉬운점** : gpt 4를 사용하기 때문에 구지 파파고 api를 사용해서 번역 하지 말고 프롬프트 단계에서해결하게 하는게 더 간편했을수 있겠다는 아쉬운점이 있었다 

그리고 기능을 구현 하는것에 집중한 나머지 ui 디자인이나 구성에 대해 미흡했던 부분더 아쉬운점인것 같다 