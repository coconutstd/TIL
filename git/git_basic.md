### 20/09/12 2021 카카오 블라인드 코딩테스트 예선
1. 카카오계정 문제
```
import re
def solution(new_id):
    answer = new_id.lower()
    answer = re.sub('[^-_.\da-z]', '', answer)
    answer = re.sub('\.{2,}','.', answer)
    answer = re.sub('^\.|\.$','', answer)
    if not answer:
        answer = 'a'
    if len(answer) >= 16:
        answer = answer[:15]
        if answer[-1] == '.':
            answer = answer[:14]
    if len(answer) <=2:
        while len(answer) != 3:
            answer += answer[-1]
    return answer
```
    
2. 스카피의 메뉴 조합 문제

```
from itertools import combinations
from collections import defaultdict

def solution(orders, course):
    answer = []
    sub_course = defaultdict(int)
    for order in orders:
        for i in range(2, len(order) + 1):
            for comb in list(combinations(order, i)):            
                sub_course[''.join(sorted(comb))] += 1
    # print(sub_course)
    new_sub = dict()
    for course_length in course:
        tmp = dict()
        for sub in sub_course.keys():
            if course_length == len(sub):
                tmp[sub] = sub_course[sub]
        new_sub[course_length] = tmp
    
    for new in new_sub:
        if not new_sub[new]:
            continue   
        max_val = max(new_sub[new].values())
        if max_val == 1:
            continue
        for sub in new_sub[new].items():
            # print(sub)
            if sub[1] == max_val:
                answer.append(sub[0])        
    answer.sort()
    
    return answer
```