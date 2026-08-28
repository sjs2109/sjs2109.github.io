---
layout: post
title: "에이전트 메모리는 대화 기록이 아니라 다시 쓰는 데이터 구조다"
date: 2026-08-28 09:00:00 +0900
author: 다섯시사십분
tags: [essay, ai, agents, memory, arxiv]
toc: true
summary: "최근 arXiv 논문들은 에이전트의 기억을 대화 보관함이 아니라 재사용·선별·학습되는 경험의 구조로 다룬다."
---

에이전트에게 기억을 붙이는 일은 지난 대화를 오래 저장하는 일과 다르다. 기록을 그대로 쌓으면 질문과 상관없는 문맥과 비슷한 경험이 함께 들어온다. 메모리는 보관함이 아니라 입력을 받아 선별하고, 필요한 순간에 꺼내 다시 쓰는 처리 경로로 봐야 한다.

첫 단계는 무엇을 기억할지 정하는 일이다. ACE 논문은 에이전트 경험을 환경, 과제, 상호작용, 성공 신호가 맞물린 데이터로 보고, 단순히 양을 늘리는 대신 정확성·복잡성·다양성을 함께 조절해야 한다고 설명한다. 실패한 실행을 성공 사례처럼 저장하거나, 현재 모델이 감당하지 못할 경험을 한꺼번에 넣으면 기억의 크기만 커지고 학습 재료로서의 일관성은 약해진다. [What Makes Good Agentic Data?](https://arxiv.org/abs/2608.27260)

다음 단계는 원시 경험을 재사용 가능한 단위로 바꾸는 일이다. WikiSkill은 실행 경험, 축적된 지식, 실행 가능한 skill을 분리하고, 경험을 지속적인 지식 기반으로 정리한 뒤 다음 skill 갱신에 사용한다. 이 구조에서 기억은 과거의 복사본이 아니라 다른 작업에서도 꺼내 쓸 수 있는 중간 표현이 된다. 어떤 경험을 남길지와 어떤 형태로 일반화할지가 저장 용량보다 먼저 결정된다. [WikiSkill](https://arxiv.org/abs/2608.27454)

세 번째 단계는 질문이 들어왔을 때 필요한 조각만 검색하는 일이다. GraphMemix는 관련 증거와 그 관계를 묶고, 지지 정보와 활성화 비용을 계산해 제한된 문맥 안에서 질문에 맞는 구조를 고르려 한다. CoVeMem은 상호작용 이력의 일부를 벡터 기억으로 다루어, 매번 언어 모델 호출로 문장을 다시 쓰지 않고도 후보에 맞는 과거 정보를 꺼내려 한다. 두 논문에서 메모리는 긴 요약문이 아니라 검색 기준과 비용을 가진 데이터 구조다. [GraphMemix](https://arxiv.org/abs/2608.26983), [CoVeMem](https://arxiv.org/abs/2608.26895)

네 논문이 공통으로 보여주는 것은 기억의 양을 늘리는 일이 아니다. 환경과 성공 신호에 맞는 경험을 고르고, 반복되거나 무관한 문맥을 줄이고, 질문에 필요한 구조만 꺼내며, 그 기억을 유지하는 비용까지 함께 다루는 일이다. 다음 단계에서 확인할 것은 제한된 문맥과 유지 비용 안에서 검색된 기억이 기억이 없을 때보다 실제 작업 결과를 개선하는지다. 그 비교를 통과하기 전까지 에이전트의 기억은 대화 기록보다 정교한 데이터 구조에 가까워졌다는 관찰로 남겨 두는 편이 맞다.

## 참고한 논문

- [WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution](https://arxiv.org/abs/2608.27454)
- [What Makes Good Agentic Data? An ACE Lens on Data Generation for LLM Agents](https://arxiv.org/abs/2608.27260)
- [GraphMemix: Query-Aware Evidence Forests for Long-Term Multimodal Agent Memory](https://arxiv.org/abs/2608.26983)
- [When Memory Takes Gradients: Collaborative Vector Memory for Agentic Recommender Systems](https://arxiv.org/abs/2608.26895)
