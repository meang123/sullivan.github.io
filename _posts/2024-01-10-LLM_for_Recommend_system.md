---
layout: single
title:  "LLM for Recommend system project"
categories: LLM,Recommend system,open ai,llama2,langchain,CAMEL Agent,RAG
tag : [LLM,Recommend system,open ai,llama2,langchain,CAMEL Agent,RAG]
toc: true
author_profile: false
sidebar:
  nav : "docs"
search: true
typora-root-url: ../
---





# 소개 





산학 프로젝트 핀웨이브에서 했던거 정리 한다. (기간 : 2023 09~12)



**서비스 소개** : 금융 취약자를 위한 멘토 멘티 추천 시스템이다. 



**결과** : 결과적으로 프로젝트는 완성하지 못했다 이유는 내가 만든 결과물과 백엔드 프론트 결과물이 통합되지 못했기 때문이다. 그래서 이 포스트에서는 내가 완성한 부분까지만 남기도록 하겠다. 

알고리즘을 구성할때 환경은 colab환경에서 실행 하였다. 그리고 aws서비스를 위해 도커를 활용했다 이 부분은 및에 성찰 부분에 추가로 언급 하겠다 




![service arichtecture image]({{site.url}}/images/2024-01-10-LLM_for_Recommend_system/image-20240110043128228.png)



------

한가지 언급할것은 산학 프로젝트로써 완성을 못한것이다 하지만 llm으로 추천하는 시스템은 성공적으로 마무리가 되었다 

산학 프로젝트에서는 취약한 금융인이 대상이었다 나의 접근 방식은 금융 멘토와 멘티로 나누고 멘티나 멘토한테 개별적으로 맞는 사람을 찾기 위해 llm이 사용되었다 llm을 통해서 멘토와 멘티가 남긴 글을 분석하여 멘티한테 도움이 되는 멘토인지 그리고 성격적으로 맞는 부분인지를 추출하여 추천 시스템으로 활용 했다 

 

프로젝트에서는 취약한 금융인을 위한 추천 시스템이지만 확장해서 HR 부서에서 사수를 배정할때도 유용하게 사용할수있을것으로 생각된다 무작위로 사수와 사서를 할당하는것보다 성격이나 능력이 서로 부합하는지 llm이 추천 해주어서 매칭해준다면 HR 부서에서 일일이 사수와 사서를 할당하는 일을 줄일수있다 





---------








**프로젝트 팀원에 대한 성찰** : 우선 팀원간에 팀워크는 상당히 부정적이었다.  백엔트 프론트와 ai파트가 따로 가는 느낌이었다. 즉 소통이 부족했던것 같다. 분명 회의는 주기적으로 하였는데도 서로 소통이 안 되었다. 예로 나는 중간 발표때 분명 언급하고 여러번 같은 내용으로 발표를 했었는데 프론트 백엔트 팀은 이 내용을 몰랐다. 그래서 결국 마지막에는 내가 구현했던 기능을 빼는 상황까지 갔었다. (결국 그럼에도 완성을 못했다) 그리고 ai파트는 2명이었지만 사실상 나 혼자 다 했다. 나머지 한명은 정말 아무것도 기여한게 없었다. 혼자서 llm을 사용한 추천시스템 알고리즘을 만들고 + 벡엔드 파트에서 만든 데이터 베이스 관계도 보고 연결 + 프론트엔드와의 연결 + aws서비스 배포를 위해 노력을했어야 했다. 



**나의 부족했던 점** : 팀원간에 팀워크가 안맞았던것도 있었지만 여전히 나의 부족한점이 있었다. 우선 llm을 이용해서 추천시스템 알고리즘을 구상하고 실행까지 완성하는데는 상대적으로 계획 안에 맞추었다. 하지만 나는 aws를 이용해서 배포를 해본적이 없었기 때문에 이 부분에서 상당히 많은 애를 먹었었다. 내가 만든 결과물을 어떻게 aws를 이용해서 배포를 하면 좋을지 고민하는 단계 부터 그걸 완성하는 단계까지 쉽지 않았었고 당장 완성을 해야 하였기 때문에 효율 보다는 우선 작동할수있는 방법을 찾았었다. 그 결과가 위에 사진처럼 구성 한것이다. 하지만 내가 구상한 코드들은 colab환경에서 진행을 했었기 때문에 도커에서 실행할수있도록 하나씩 변형을 했어야 했다. 도커도 처음 사용해보았기 때문에 쉽지 않았다 특히 도커에서 내 프로그램을 실행하기 위해서 read/write하는 작업을 /tmp 폴더로 옮기고 수행하도록 코드를 하나씩 변경 하고 에러를 고치는 과정이 힘들었었다. (이 부분은 및에서 추가로 더 언급 하겠다. )

그러다 보니 aws lambda container에서 돌아가는 최종 결과물을 최종 발표 날때 완성을 할수있었고 이제  API gateway를 통해 프론트와 연결만 하면 완성이었다. 하지만 최종 발표때까지 시간이 많이 없었고 연결을 하려고 노력을 해보았지만 결국 프론트와 연결하는데 실패를 하였고 결국 완성하지 못한채 발표를 했어야 했다. 내가 조금 더 빨리 완성을 하고 시간 확보를 했었더라면 프로트와 연결하고 결과를 낼수있었을것이다. 이 부분은 내가 확실히 부족했던 점이었던것 같다 



지금 부터는 내가 구상했던 내용에 대해서 정리를 하겠다 



### 나의 역할 및 목적  

>  기본적으로 멘토와 멘티를 추천해주는 ai를 만드는게 나의 역할이었다. 기존 추천 시스템 처럼 필터 기반으로 추천하는 방법도 있지만 다음과 같은 이유로 LLM을 사용해서 추천시스템을 구성하고 싶었다. 
>
> 
>
> 1. 멘토와 멘티는 각자 사람이고 사람과 사람의 추천 방식은 어렵고 복잡하다.
>
> 2. 필터 기반 추천시스템을 위해 적용할만한 데이터 찾지 못했다. 
>
>    * 적용할만한 데이터를 찾았더라도 기존 추천 시스템 방식을 사용하면 다른 서비스와의 차별성이 부족할것으로 생각 하였다. 
>
>      
>
> 3. LLM은 사람을 조금이라도 이해 할 수 있어서 더 잘 할 것이라는 생각하였다 



그래서 llm을 추천시스템에 적용한 예시나 사례가 있는지 찾아 보았으나 프로젝트를 시작할 당시에는 이제 연구가 시작되는 주제 였었기 때문에 논문을 여러개 보면서 아이디어를 찾아보고자 했다 내가 참고 했던 논문은 다음과 같다 



* Zero-Shot Next-Item Recommendation using Large Pretrained
  Language Models
* RAH! RecSys-Assistant-Human: A Human-Centered
  Recommendation Framework with LLM Agents
* Large Language Models as Zero-Shot Conversational
  Recommenders
* Recommender AI Agent: Integrating Large Language Models for Interactive
  Recommendations



물론 위에 논문을 꼼꼼히 읽은건 아니다. llm을 이용해서 어떤 방식으로 추천시스템을 구현하려고 했는지 아이디어만 봤었다. 하지만 코드가 같이 주어진건 아니라서 논문만 참고를 했어야 했다 



위에 논문을 통해 얻은 결과는 다음과 같다 

1.  prompt engineering이 생각보다 중요하게 작용한다는 사실을 알수있었다. 
2. llm을 통해 도메인에 대한 지식 분석 + 사용자의 의도 분석 + 결과에 대한 성찰하는 과정등 단계를 여러개로 나누어서 추천시스템을 구성하는 아이디어였다 



----

# 멘토 멘티 정보 및 환경 정보



우선 환경은 colab환경이 었고 langchain을 사용했다. llm으로는  llama2 70b chat model을 사용했다.(Together ai api를 사용) 

그리고 라마2를 이용해서 한국어 번역까지 하려고 했는데 생각 보다 잘 작동이 되지 않아서 파파고 api를 통해서 번역 하는 방향으로 갔다. 

> 이 프로젝트에서는 라마2를 사용해서 해결 하려고 했다. 이유는 우선 가격이 있었다. together ai api에서 제공하는 credit이 있어서 거의 공짜로 사용할수있었지만 open ai api사용하려면 유료 결제를 해야 했기 때문이다.  하지만 CAMEL Agent부분에서는 open ai llm이 더 잘 작동 하였기 때문에 CAMEL agent부분에서는 open ai llm을 사용했다. 



소개란(한국어)-> 영어 번역 후 프로그램에 적용 -> 결과(영어-> 한국어 번역) 



멘토 멘티대한 데이터는 chat gpt를 이용해서 만들었다. 그리고 데모 버전이라서 많이 만들지는 못했다. 



### 멘토 정보 



**Trex**

안녕하세요, 저는 책임감과 데이터 중심의 의사 결정을 선호하는 기업 재무 분석가 Trex입니다.저의 핵심 가치는 기업의 재무 건전성을 면밀히 조사하고 미래 성장 가능성을 평가하는 것에 있습니다.글로벌 기업 재무 분석가로서 12년 이상의 경험을 쌓으며 기업 재무 분석과 재무 모델링에 대한 깊은 이해를 쌓았습니다.저의 주된 관심사는 기업의 재무 건전성을 보장하고 효과적인 투자 전략을 세우는 것입니다.저는 제 전문 지식을 공유하고 여러분이 기업 금융의 세계를 개척하는 것을 돕기 위해 여기에 왔습니다.



**Sulley** 

안녕하세요! 여러분들의 금융 여정에 함께하게 된 멘토로서 매우 기쁩니다.나는 금융 분야에서의 전문 지식을 바탕으로 재테크(financial technology)와 투자에 대한 실질적이고 현실적인 조언을 제공하는 것을 즐깁니다. 금융 전략의 핵심과 효율적인 자산 관리에 대한 이해를 통해 여러분의 재무적인 목표를 달성하는 데 도움이 되고 싶어졌어요.내 성격은 적극적이고 실용적인 편입니다. 무엇보다도, 여러분의 목표 달성을 위해 힘쓰는 모습을 지켜보는 것이 가장 큰 보람입니다. 금융의 복잡성을 단순하게 전달하고, 실제로 적용 가능한 솔루션을 제시하는 것을 목표로 하고 있습니다.가치관 측면에서는 돈을 통한 가치 창출을 중요하게 여기며, 금융 지식을 활용하여 개인과 사회적인 성장에 기여하고자 합니다. 함께 일하면서 여러분의 금융적인 목표를 함께 성취하고, 돈이 주는 자유로움을 함께 누려 나가길 기대합니다. 함께 여행하는 동안 서로에게 영감을 주며, 긍정적이고 풍요로운 여정을 만들어 나가요!



**Ken**

안녕하세요, 저는 Ken입니다.저는 항상 재정적인 문제에 대해 차분하고 분석적인 접근을 해왔습니다.지난 15년 동안 저는 투자 은행 업무와 자산 관리 업무를 할 수 있는 특권을 누려 왔습니다.저에게 재무 안정성과 계획은 단순히 유행어가 아니라 안전한 재무 미래의 초석이 됩니다.저는 특히 사람들이 재무 포트폴리오를 다양화하고 의미 있는 재무 목표를 세울 수 있도록 돕고 싶습니다.궁금한 점이 있거나 안내가 필요하시면 제 경험과 통찰력을 공유하여 금융 여정에 도움을 드리고자 합니다.



**Holly**

안녕하세요, 저는 당신의 부동산 금융 및 주택 담보 대출 전문가인 Holly입니다.저의 접근 방식은 모두 정확성과 명확성에 관한 것입니다. 왜냐하면 저는 감정적이거나 모호한 이야기를 좋아하는 사람이 아니기 때문입니다.제 분야에서 15년 동안 쌓아온 탄탄한 경험을 바탕으로, 저는 제 전문성에 큰 자부심을 느끼며, 부동산 금융 및 주택 담보 대출 분야에서 충분한 정보를 바탕으로 의사 결정을 내리는 데 필요한 가장 정확하고 신뢰할 수 있는 통찰력을 제공하는 데 전념하고 있습니다.



-----

### 멘티 정보



**James**

안녕하세요, 금융 멘토링 프로그램에 참여하게 된 저는 항상 금융 세계에 대한 탐구와 야망을 품은 열정적인 개인입니다. 금융의 복잡성에 도전하고자 하는 강한 욕망과 함께, 미래를 위해 지속적으로 투자하고 싶어하는 목표를 갖고 있습니다.저는 리스크 관리와 금융 안전성을 중시하며, 이를 바탕으로 효율적이고 안정적인 투자 전략을 개발하고자 노력하고 있습니다. 또한, 다양한 금융 상품과 시장 동향에 대한 지식을 확장하여 최신 동향을 반영한 결정을 내릴 수 있도록 노력하고 있습니다.멘토와의 소통을 통해 나만의 투자 철학을 더욱 세련되게 발전시키고, 금융적인 안목을 높여 나가고자 합니다. 멘토의 지혜와 지도 아래에서 더 나은 금융적 안정성을 달성하기 위해 열심히 노력할 것을 약속드립니다. 감사합니다.



**Bailey**

저는 금융에 대한 흥미와 재테크(financial technology), 투자에 대한 강한 관심을 가진 개인으로, 적극적이고 목표 지향적인 성격을 가지고 있습니다. 일상의 금융 의사결정에 있어서는 신중한 성향으로 접근하며, 목표를 달성하기 위해 노력하는 것을 중요하게 생각합니다.금융 멘토링 프로그램에 참여하면서 전문가의 지도를 받아 더욱 효과적인 재테크(financial technology) 전략과 투자 방법을 습득하고자 하는 목표를 가지고 있습니다. 다양한 금융 상품과 시장 동향에 대한 이해를 높이며, 개인적인 금융 목표를 달성하기 위해 노력하고 있습니다. 목표 지향적인 성격을 바탕으로 멘토링을 통해 성장의 기회를 극대화하고, 금융적인 안목을 높여 미래의 재무적 안정성을 구축하고자 합니다.멘토와의 소통과 지도를 통해 나만의 투자 철학을 더욱 발전시키고, 금융적인 지식을 심화해 나가고자 하는 목표를 가지고 있습니다. 제 경험과 노력을 통해 멘토링 프로그램을 통해 제 금융적인 역량을 향상시키고, 미래를 위한 지혜를 쌓아가는데 적극적으로 참여하겠습니다. 감사합니다.



**Sarah**

안녕하세요, 여러분! 저는 금융의 무한한 가능성을 탐험하는 여정에 도전하고 있는 Sarah입니다.제 성격은 호기심과 열정이 가득한데요, 금융 세계에서 새로운 지식을 습득하고 다양한 경험을 통해 성장하는 것에 큰 흥미를 느낍니다.교육을 통한 재정적인 안정과 미래 투자에 대한 심사숙고가 제 가치 중 하나입니다. 재무적 기본을 탄탄히 다지고, 저축 습관을 꾸준히 기르며 투자의 세계로 나아가는 여정에서 끊임없는 호기심을 가지고 있습니다.저는 여러분과 함께 배우고 성장하며, 이 재정적인 모험을 함께할 수 있어 기쁨을 느낍니다. 함께 여행하는 동안 서로에게 영감을 주고 받으며, 금융의 감동적인 순간들을 만들어 나가고 싶습니다.



**Michel**

안녕하세요! 지식의 즐거움과 전문성 강화에 열중하는 Michel입니다. 대학과 금융 분야에서의 탐험을 통해 나만의 진로를 발견하고 있는데요.내가 빠져 있는 영역은 주식시장과 금융기술(Fintech)입니다. 특히 주식 시장의 다양한 흐름과 동향에 대한 탐구심을 가지고 있어, 기존 투자 전략을 현대적이고 효율적인 방식으로 혁신하고자 합니다. 또한 금융기술(Fintech)의 발전이 금융 분야에 미치는 영향에 대한 지속적인 연구를 통해, 디지털 금융 혁명에 어떻게 기여할 수 있을지에 대한 열망을 품고 있습니다.학문적인 학습과 다양한 경험을 바탕으로, 금융의 다양한 측면을 이해하고자 끊임없이 노력하고 있습니다. 여러분과 함께 이 길에서 배우고 성장하며, 금융의 새로운 지평을 열어나가고 싶어졌습니다.



**Robert**

안녕하세요, 여러분! 저는 Robert라고 합니다. 현재 기업 금융과 투자 분야를 새롭게 탐험하고 있는 여행자입니다.제 성격은 학습에 대한 강한 의욕과 진로개발에 대한 열정이 두드러지는데요, 새로운 분야에서의 도전에 대한 열망이 항상 저를 움직이게 만듭니다.기업금융과 투자 분야에서 보람 있는 경력을 쌓고 싶은 간절한 열망이 저를 이곳에 세우게 했습니다. 특히, 기업 재무, 재무 모델링, 그리고 투자 의사 결정의 복잡한 기술에 대한 깊은 관심을 가지고 있습니다.대학생으로서 새로운 도전을 향해 나아가고자 여러분과 함께 배우고 성장하고 싶습니다. 이 자리에서 함께 복잡한 금융의 세계를 탐험하며, 서로에게 영감을 주고 받으며 발전해 나가는 여정을 함께하고 싶습니다.



**Olivia**

안녕하세요! 저는 Olivia, 호기심 가득한 여행을 즐기며 끊임없이 새로운 것을 배우는 것에 즐거움을 느끼고 있어요.현재 대학생활의 다채로운 경험을 즐기며, 기업금융과 투자 분야에서의 흥미로운 커리어를 꿈꾸고 있습니다. 기업 재무, 재무 모델링, 그리고 전략적 투자 결정에 필요한 복잡한 기술에 대한 이해와 열정을 가지고 있어요.다양한 기회를 열렬히 환영하며, 금융계의 다양한 영역을 탐험하고 싶어졌습니다. 특히 부동산 투자 분야에 대한 흥미와 깊은 관심을 품고 있어, 부동산 시장의 동향과 투자 전략에 대한 지식을 향상시키고자 합니다.



**Aiden**

안녕하세요! 저는 금융에 대한 깊은 흥미를 가지고 있으며, 재테크(financial technology)와 투자에 대한 실질적인 지식을 얻고자 합니다. 저의 목표는 금융 전략의 핵심을 이해하고, 자산을 효율적으로 관리하여 재무적인 목표를 달성하는 것입니다. 저는 적극적이고 실용적인 성격을 가지고 있으며, 복잡한 금융 개념을 이해하고 실제로 적용 가능한 솔루션을 찾는 것에 큰 도전감을 느낍니다. 저는 돈을 통해 가치를 창출하는 것을 중요하게 생각하며, 금융 지식을 활용하여 개인적인 성장과 사회적인 성장에 기여하고자 합니다. 함께 금융의 복잡성을 단순하게 전달하고, 실제로 적용 가능한 솔루션을 찾아내는 것을 목표로 하고 있습니다. 돈이 주는 자유를 체험하며, 서로에게 영감을 주는 긍정적이고 풍요로운 여정을 만들어 가고 싶습니다. 저의 금융 목표를 달성하고, 함께 성장하며, 금융의 복잡성을 이해하는 데 도움이 되기를 바랍니다. 감사합니다!





# 프로그램 흐름도 



**cf**  : 소개란과 피드백을 통해 유저의 성향을 강화 하는 방식인데 지금 상황에선 유저를 멘티로 가정한다. 실제로 앱으로 적용할때는 유저를 멘토로 설정하면 멘토의 성향을 강화 할수있다. 여기서는 이미 멘토의 성향 강화가 마무리 되었다는 가정이 있다.   



위에서 얻은결과를 통해 나는 다음과 같은 프로그램 흐름도를 구성 하였고 다음과 같다



1. 성격,가치관, 전문성,경험,흥미 5가지에 대한 특성을 멘토 멘티 소개란 작성문장에서 뽑아낸다 

   > 멘티 멘토는 각각 소개란을 작성하는데 이 소개란에서 5가지 특성을 추출하여서 추천하는 방향으로 흐름을 잡았다. 위에 5가지는 내가 임의로 정한 특성이었기 때문에 다른 특성으로 대체 할수있다. 





2. 좋은 멘토 멘티 매칭에 관한 파일 내용 (총 3개의 pdf파일 사용) 바탕으로 (RAG) 소개란에서 뽑아낸 멘토의 5가지 특성 + 멘티의 5가지 특성을 서로 비교 하여서 추천 하도록 한다 

>  번역은 파파고 api 사용, 프롬프트에서 5가지 특성을 바탕으로 추천하도록 프롬프트 작성, 
>
> 유저와 멘토의 매칭 이유와 긍정적인 이유,부정적인 이유 총 3개가 매칭 결과로 출력이 된다 



다음 3개의 pdf파일은 좋은 멘토 멘티에 관한 파일 내용이다 

<a href="{{site.url}}/pdfs/file1_1.pdf">file1 PDF</a>


<a href="{{site.url}}/pdfs/file2_1.pdf">file2 PDF</a>


<a href="{{site.url}}/pdfs/file3_1.pdf">file3 PDF</a>







3.  2번에서 얻은 결과를(모든 멘토에 대해서 해당 유저와 잘 맞는 이유, 긍정적인 이유, 부정적인 이유) 유저(멘티)에게 보여 준다 

   > 유저는 결과를 보고 피드백을 반영할수가 있다 



4.   유저의 피드백을 통해 CAMEL Agent 적용한다 AI는 profiler, user는 member로 설정 하여 기존 소개란과 피드백을 통해 해당 유저의 성향을 강화하는 단계를 거친다. 이 과정을 통해 2번에서 얻은 5가지 특성 정보를 더 풍부하게 강화 할수가 있다. 상세하게 얻은 유저의 5가지 특성을 바탕으로 다시 멘토와 매칭 하여 추천을 진행하다 

   > 가상의 유저의 반응 : 재무분석과 모델링에 대한 Trex의 전문성은 나에게 그 넓은 시야를 줄 수도 있고 긍정적인 면이 많다. 그러나 Sulley의 적극적인 접근은 협력적이고 해결 중심적인 멘토링 관계를 형성할 수 있을 것으로 보인다
   >  또한 재테크와 투자에 대한 전문성이 나의 관심사나 전문성과 잘 부합한다. 그리고 개인의 사회적 성장과 경제적 지식을 통해 돈의 가치를 창출하는 것이 목표이기 때문에 더 잘 맞을 것이라 생각한다
   >
   > ( Trex와 Sulley는 멘토이다)



+ camel agent를 넣은 이유는 유저의 피드백에서 내용을 더 강화 하기 위해 AGI를 고려 하게 되었는데 Baby AGI와 auto gpt, CAMEL중에서 CAMEL을 적용하고 싶어서 적용하게 되었다 

  [langchain/cookbook/camel_role_playing.ipynb at master · langchain-ai/langchain (github.com)](https://github.com/langchain-ai/langchain/blob/master/cookbook/camel_role_playing.ipynb)





아래는 소개란만 가지고 추출한 특성이다 


![extract info image]({{site.url}}/images/2024-01-10-LLM_for_Recommend_system/image-20240112015548505.png)



다음은 CAMEL Agent를 통해 강화된 정보이다 

![camel agent image]({{site.url}}/images/2024-01-10-LLM_for_Recommend_system/image-20240112015613262.png)


[위에 사진처럼 소개란보다 유저의 피드백을 통해 강화된 풍부한 정보를 기반으로 가질수 있다면 해당 유저에 맞는 추천을 할수있을것으로 생각 했다.]



다음은 위에서 강화한 특성 가지고 다시 추천을 하였을때의 결과이다 

![before image]({{site.url}}/images/2024-01-10-LLM_for_Recommend_system/image-20240112015754195.png)




![after image]({{site.url}}/images/2024-01-10-LLM_for_Recommend_system/image-20240112015810324.png)



+  초반에는 Trex멘토에 대한 부정적의견이 없었으니 유저의 반응 이후 Trex멘토의 부정적 의견이 추가 되었다. 하지만 Sulley멘토에 대해서는 여전히 부정적인 의견은 없다 (풍부한 특성이 반영되었다는 의미)

  

+ 마음에 드는 비슷한 멘토가 여러명 있을때 나의 의견을 반영하여서 여러명의 멘토 중에 더 좋은 선택지를 제공 할 수가 있다



**cf** : 실행 할때마다 다르니 깃헙 주소의 ipynb  파일의 결과를 다시 한번 확인해 주면 좋겠습니다



다음은 Camel agent에서 나온 결과이다 (구체적인 작업 내용과 이 내용 기반으로 나온 결과를 합친 내용이다)



```python
"""
**Task Specifications: Personality Profiling Through Opinion Analysis**

**Objective:** Utilize the user’s opinion to assess personality traits and characteristics and identify potential areas for personal growth or professional alignment.

**Analysis Points:**
1. Preference for broader analytical perspectives versus active, hands-on mentoring.
2. Alignment of personal interests and expertise with professional activities and goals.
3. Identified aspirations in creating value through personal social growth and economic knowledge.

**User’s Opinion Summary:**
The user appreciates Trex’s broad financial analysis and modeling expertise, suggesting a preference for comprehensive strategic viewpoints. They see the merit in this for gaining a wide-ranging understanding of financial structures. However, there’s also an affinity for Sulley’s more engaged and collaborative mentoring style, which indicates an inclination towards dynamic, interpersonal engagements and a hands-on approach to problem-solving and learning.

Furthermore, the user’s background in financial technology and investment is closely tied with their interests, showing a strong sense of professional and personal coherence. There is a distinct desire to merge financial acumen with social growth and economic knowledge, implying a holistic view of value creation that transcends monetary gains, aiming instead for a broader impact.

**Personality Profiling:**
- **Analytical Competence:** The user has demonstrable analytical skills, suggested by their appreciation for financial analysis and the conceptualization of value through economic understanding.
- **Interpersonal Skills:** The preference for a collaborative and solution-oriented mentoring relationship reveals a likely proficiency in teamwork and communication.
- **Proactive Learning:** A leaning towards an active mentor indicates a proactive approach to acquiring knowledge, perhaps with a preference for experiential learning over purely theoretical methods.
- **Integrative Thinking:** The desire to combine financial expertise with personal social growth suggests integrative thinking, bridging disparate concepts to form a coherent life and career philosophy.
- **Value-Oriented:** The goal of creating value through knowledge signifies a purpose-driven personality with a potentially altruistic streak, valuing social contributions alongside personal achievements.

**Potential Job Roles or Career Paths:**
1. Social Impact Investing - utilizing financial expertise to drive investments in social enterprises.
2. Financial Education - designing programs or tools that improve economic literacy and foster social development.
3. Strategic Consultancy - advising companies on how to align financial growth with societal benefits.

**Guidance for Member:**
The member is advised to explore opportunities that allow for strategic thinking and interpersonal collaboration. Seeking roles that involve social impact will likely be fulfilling. They should consider mentorship that balances strategic oversight with personal interaction, supporting both broad and dynamic learning experiences.

**Conclusion:**
The user’s opinion reveals a multi-faceted personality that is equally analytical and action-oriented. With a clear interest in integrating financial savvy with social betterment, they are likely to find satisfaction in roles that allow them to leverage their economic knowledge to make meaningful contributions. The member’s focus should be on opportunities that align with these dual aspirations, offering both breadth and depth in their professional endeavors.CAMEL_TASK_DONECAMEL_TASK_DONECAMEL_TASK_DONESolution: The user can enhance their economic knowledge with a focus on social impact by utilizing the following resources:

1. Books such as "Capital in the Twenty-First Century" by Thomas Piketty or "The Social Entrepreneur's Playbook" by Ian C. MacMillan and James D. Thompson for insights into economic inequality and social entrepreneurship.
2. Online courses from platforms like Coursera or edX that offer classes on social impact, sustainable finance, and impact investing.
3. Subscriptions to journals and magazines like the Stanford Social Innovation Review or The Economist for current trends and research on the intersection of economics and social issues.
4. Membership in professional organizations such as the Global Impact Investing Network (GIIN) for access to industry reports and networking opportunities.
5. Attendance at conferences and webinars focused on social impact and economics, such as the Social Capital Markets (SOCAP) conference or the Aspen Institute's events.

Next request.Solution: The user can connect with professionals in social impact investing and strategic consultancy by employing the following networking strategies:

1. Join LinkedIn groups dedicated to social impact investing and strategic consultancy to engage in discussions and connect with industry professionals.
2. Attend industry-specific events, such as the SOCAP conference or local meetups, to meet peers and leaders in the field.
3. Participate in webinars and virtual conferences to build connections and stay informed about the latest trends and opportunities.
4. Volunteer for committees or projects within professional organizations to increase visibility and demonstrate commitment to the field.
5. Utilize alumni networks from their educational institutions to find mentors or collaborators with similar interests.
6. Reach out directly to professionals whose work they admire via email or social media to request informational interviews or casual coffee meetings.
7. Offer to speak at or host panels and workshops on topics related to social impact investing and strategic consultancy to establish thought leadership.

Next request.
"""
```





여기서 나온 결과에서 5가지 특성을 다시 추출하여 내용을 강화 한다 그렇기 때문에  처음 소개란 보다 유저의 피드백의 내용에 편향 되어있다. (**한계점 : 소개란에서 추출한 5가지 특성을 포함 하지 않고 유저의 피드백에만 편향 되어있기 때문에 이 부분은 추후에 개선 할 여지가 있는 부분 같다**)







5.  멘토 중에서 유저와 가장 잘 맞는 멘토를 찾는다

> 해당 사용자와 멘토와의 추천 결과를 바탕으로 가장 잘 맞는 멘토를 찾아서 반환한다 
>
> **한계** : 멘토의 사용자가 많을때 시간 소요가 크다는 한계가 있다. 왜냐하면 모든 멘토에 대해 유저(멘티)와의 관계를 보기 때문이다. 





6. 찾은 잘 맞는 멘토에 대한 리뷰를 찾는다.

> 데이터 베이스에서 해당 멘토에 남겨진 리뷰를 본다 이때 리뷰를 작성한 유저(멘티) id를 통해 멘티 정보에서 검색하여 멘티에 대한 정보를 가져 온다.



7. 해당 유저(멘티)와 비슷한 사람(다른 멘티들)을 정보에서 찾는다

> 이때 일반적으로 유사도 결과로 rag 검색하는 대신 Contextual compression pipeline을 구성한다(검색 속도 향상 및 비용절감)

<img src="/images/2024-01-10-LLM_for_Recommend_system/image-20240112002228970.png" alt="image-20240112002228970" style="zoom:67%;" />



8. 5번에서 구성한 pipelin이 적용된 Retrieval QA chain을 활용하여 4번에서 가져온 파일에서 검색과정을 진행 한다. 멘토에 남겨진 많은 리뷰 중에서 나와 비슷한 사람이 남긴 리뷰를 가져 가기 위한 단계



9. 얻은 리뷰를 바탕으로 멘토의 평판을 얻는다. 이때 평판의 정보에서 횡설수설 하는 현상을 방지 하기 위해 RCI(Recursive Criticism and Improvement)방식을 사용한다 3개의 단계를 거친다 초기 질문 -> 비판 -> 향상 -> 최종 출력



10. 가장 잘 맞는 멘토에 대해서 이유 ,긍정적 이유, 부정적 이유 + 최종 결과를 summary_checker 사용해서 사실 기반 + 횡설수설 현상 방지 하면서 요약한다 



11. 요약된 최종 정보를 유저한테 보여 준다 



```python
"""
Best mentor : Sulley. Positive Opinion:\n\nThe mentor and mentee share similar values, expertise, and interests, and their personalities complement each other.\n\nThe mentor's practical and active approach will help the mentee achieve their goals in financial analysis and strategic thinking, while the mentee's analytical and action-oriented personality will help the mentor refine their ideas and create a clear plan for their mentee's development.\n\nThe mentor's experience in mentorship and financial advice will provide valuable guidance for the mentee, and the mentee's background in financial technology and investment will provide a strong foundation for their mentorship.\n\nNegative Opinion: None.\n\nThis matching result is reasonable because the mentor and mentee have a good balance of complementary skills, values, and interests. Their personalities also complement each other, with the mentor's practicality and the mentee's analytical approach creating a synergy that can help them work well together. The mentor's experience and expertise will provide valuable guidance for the mentee, while the mentee's background and interests will provide a strong foundation for their mentorship. Overall, this matching result has the potential to create a positive and productive mentor-mentee relationship.\n\nChecked Assertions:\n\n1. The mentor and mentee share similar values, expertise, and interests. (True)\n2. The mentor's practical and active approach will help the mentee achieve their goals in financial analysis and strategic thinking. (True)\n3. The mentee's analytical and action-oriented personality will help the mentor refine their ideas and create a clear plan for their mentee's development. (True)\n4. The mentor's experience in mentorship and financial advice will provide valuable guidance for the mentee. (True)\n5. The mentee's background in financial technology and investment will provide a strong foundation for their mentorship. (True)\n\nSuggestions for Corrections:\n\n1. None.\n\nThe mentor and mentee have a good balance of complementary skills, values, and interests, and their personalities complement each other well. The mentor's experience and expertise will provide valuable guidance for the mentee, while the mentee's background and interests will provide a strong foundation for their mentorship. This matching result has the potential to create a positive and productive mentor-mentee relationship.
"""
```









# 평가 방식 



llm에서 나온 결과에 대해 평가 하는 방식은 크게 사람이 직접 평가 하거나 llm이 평가 하는 방식이 있는것으로 알고 있다. 

[Evaluate LLMs and RAG a practical example using Langchain and Hugging Face (philschmid.de)](https://www.philschmid.de/evaluate-llm)



내가 선택한 평가 방식은 사람이 평가 하는 방식으로 구성 하였다. 최종으로 나온 결과를 보고 나서 유저가 직접 판단한다. 요약된 정보 기반으로 선택 하여도 괜찮고 아닌것 같으면 다른 사람을 선택 할수있게 한다. 





# 마무리 



이 프로젝트는 금융 취약자를 대상으로 멘토 멘티 추천 하는 프로젝트였지만 확장할 영역은 충분히 많을것으로 예상한다. 예를 들어 it 회사에서 인턴한테 사수를 배치 하기 위해 인사 부서(HR)에서 배치 해주는것으로 알고 있는데 그 과정을 내가 만든 프로그램을 사용한다면 인사 부서에서 할 작업을 자동화 할수있을것으로 예상한다. 물론 지금은 실질적인 서비스를 위한 준비가 되어있지 않다(대량의 사람 처리, 알고리즘 효율성등등 개선의 여지가 많기 때문이다.) 



사람과 사람간에 추천 하는 방식에 대해 내가 생각한 알고리즘으로 구성하였다. 그래서 알고리즘 흐름에서 부족한 부분이 있을것같다. 이 부분에 대해서 피드백이 있으면 댓글로 알려주세요. 그리고 실질적인 서비스를 위해서는 대량의 사람을 처리 할수있어야 하는데 이 부분 역시 부족하다.  



해당 코드는 다음 깃헙 주소에서 확인 할수있다 

[meang123/LLM-for-recommend-system (github.com)](https://github.com/meang123/LLM-for-recommend-system)



도커 버전은 다음 깃헙 주소에서 확인할수있다. 다만 CAMEL agent부분 즉 유저의 피드백을 받고 수정하는 기능은 빠져 있다 자세한 사항은 README를 보면 될것 같다. 그리고 위에 ipynb 파일은 모든 기능을 한번에 넣었기 때문에 가독성이 좋지 않은데 도커 버전으로 만든 부분은 기능을 세부적으로 나눠서 정리 했기 때문에 위에 코드와 같이 보는것을 추천 한다. 

[meang123/llm_for_rec_docker_version (github.com)](https://github.com/meang123/llm_for_rec_docker_version)



마지막으로 이 프로젝트에서 llm으로 라마2를 사용했지만 langchain에서 지원 하는 기능에서 한계가 있었다. (bind,cohereReranker등등 작동 하지 않는 부분이 많았다) 그래서 open ai llm을 사용하는것을 추천한다 그리고 더 다양하고 간단하게 코드 구현을 할수있다는 장점이 있다. 







