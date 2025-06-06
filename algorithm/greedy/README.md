# 그리디 알고리즘

## 그리디 알고리즘이란 무엇인가요?

현재 상황에서 가장 좋아 보이는 선택(최선의 선택)을 반복하며 전체 문제를 해결하는 알고리즘. 탐욕적 접근을 통해 로컬 최적 → 글로벌 최적을 기대

- 빠르고 구현이 간단함
- 대부분 O(n log n) 이하로 동작
- 항상 최적해를 보장하지는 않음, 문제 조건에 따라 정확성 보장 가능

## 어떤 경우에 그리디 알고리즘이 유효한가요?

- Greedy Choice Property: 현재 최적 선택이 전체 최적해로 이어질 때
- Optimal Substructure: 부분 문제의 최적해로 전체 최적해를 구성할 수 있을 때

## 그리디와 DP는 언제 갈리나요?

| 항목           | 그리디                      | DP                          |
| -------------- | --------------------------- | --------------------------- |
| 선택 기준      | 현재 최선                   | 모든 경우 비교              |
| 정답 보장 여부 | 조건부                      | 항상                        |
| 시간복잡도     | O(n)~O(n log n)             | 보통 O(n²) 이상             |
| 예시           | 동전 거스름돈 (단순한 경우) | 동전 거스름돈 (복잡한 경우) |
