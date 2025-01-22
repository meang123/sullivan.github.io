---
layout: single
title:  "Transformer model 정리 및 lagnchain 정리"
categories: LLM,langchain,Transformer model,chain,agent,conversational memory,RAG,prompt 
tag : [LLM,langchain,introduction,Transformer,Transformer model,chain,agent,conversational memory,RAG,prompt]
toc: true
author_profile: false
sidebar:
  nav : "docs"
search: true
typora-root-url: ../
---





# 소개 



langchain을 경험해보면서 얻은 정보를 정리 해보려고 합니다. langchain 공식 문서에 정리가 잘 되어 있어서 대부분 langchain 공식 문서 내용 기반으로 작성이 되었습니다. 추가로 transformer model에 대하여 알고 있으면 좋을것 같아서 같이 정리를 했습니다. 



### 참고링크 

다음은 주로 참고 한 영상 주소와 공식 문서 주소 입니다 



[(233) James Briggs - YouTube](https://www.youtube.com/@jamesbriggs)

[(233) Sam Witteveen - YouTube](https://www.youtube.com/@samwitteveenai)



몇달만에 또 다른 내용들이 추가가 계속 되고 있으니 자주 공식 사이트 참고 하면 도움이 될것 같습니다. 밑에서 정리한 내용 + 밑에 사이트에서 소개하는 use case에 대해서 같이 보면 더 풍부한 내용을 얻을수있을것 같습니다 



그리고 pdf에 나와있는 영상이나 블로그 글들을 모두 보고 나서 정리 한게 아니라 가볍게 참고 하거나 안본 영상들도 있기 때문에(자료 찾아보다가 참고 하면 좋을것들을 정리 했기 때문) 혹시 무작정 영상에 대한 요약도 같이 있을것이라고 생각하지 않았으면 좋겠습니다.



[Use cases | 🦜️🔗 Langchain](https://python.langchain.com/docs/use_cases)

[LangChain AI Handbook | Pinecone](https://www.pinecone.io/learn/series/langchain/)





그리고 모든 정리 내용은 pdf로 제공 되기 때문에 pdf로 참고 해 주시면 감사 하겠습니다 



------



# Transformer model 정리 


<a href="{{site.url}}/pdfs/transformers model.pdf">Transformers model PDF</a>



#### Self attention

Query @key transpose **[내적은 얼마나 비슷한가 유사성을 나타내기 때문에 결국 Q와 K들의 유사성을 확인하는 작업인것이다] :**    

 각 chunk에 대한 score 값 그대로 사용할수없으니 row방향으로 softmax적용한다 그리고 나서 Value matrix곱한다 

예를 들어 I love you all의 chunk가 있을때 Q@key T의 score에서 I끼리는 0.9정도이고 I query와 you key값의 softmax값이 0.1의 상관관계가 나왔다고 하면 softmax(Q@key T) @V를 해줌으로써 

I와 you에 대한 상관관계가 적용된 새로운 I 벡터를 형성하게 되는 효과를 가진다 



각 쿼리에 대한 키 정보의 가중치 합이다 즉 쿼리와 키와의 관련 정보를 얻고 키에 대한 value를 weithed sum한것이 attention에 대한 결과 이다 

각각의 쿼리에 대해 키와 내적 구한다 : self attention => 동음이의어 , 순서 맥락을 구분 할수있다 









#### Multi head attention



CNN에서 커널 여러개 만들어서 서로 다른 피쳐 구하는 필터맵 구한것처럼 self attetion을 여러개 만들어서 각기 다른 가중치 값을 가진 attention을 concate한것이다 








# prompt 



<a href="{{site.url}}/pdfs/prompt templates.pdf">prompt PDF</a>


# conversation memory for llm 



<a href="{{site.url}}/pdfs/Conversational memory for LLM.pdf">conversational memory PDF</a>



# retrival augemented generation(RAG)

<a href="{{site.url}}/pdfs/retrival.pdf">retrival PDF</a>



# chain 



<a href="{{site.url}}/pdfs/chain.pdf">chain PDF</a>



# Agent 



<a href="{{site.url}}/pdfs/agent.pdf">Agent PDF</a>
