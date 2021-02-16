# 9663번 N-Queen
[문제 보러가기](https://www.acmicpc.net/problem/9663)

## 🅰 설계
하나의 행에는 하나의 퀸만 있을 수 있다는 것에 착안하여 각 행마다 퀸을 하나씩 배치하고
행을 하나씩 증가시켜 재귀 호출을 하는 방식으로 구현했습니다. 이 문제에서 가장 고민하게
되는 부분은 **이전에 배치된 모든 퀸들과 대각선으로 마추칠 수 없다는 것을 체크하는 방법**
입니다. 가장 먼저 떠올랐던 해결책은 이전 퀸들의 위치를 저장하면서 좌표의 기울기의 크기가
1임을 확인하는 방법이였습니다. AC는 됐지만 다른 코드들을 보면서 대각선 역시 column처럼
몇 개의 그룹으로 묶어서 생각할 수 있다는 아이디어를 얻었습니다. 또 오늘 수업시간에 
비트마스크를 배웠고 규태님이 비트마스크로 코드를 짜신 것을 보아 저도 비트마스크를
연습할 겸 비트마스크로 구현해보았습니다.

```java 
for(int col=0; col<n; col++) {
    if((colMask & (1 << col)) == 0 &&
            (leftMask & (1 << row+col)) == 0 &&
            (rightMask & (1 << row-col+n-1)) == 0) {
        sol(row+1, colMask | (1 << col),
                leftMask | (1 << row+col),
                rightMask | (1 << row-col+n-1));
    }
}
```

이전에 boolean 배열을 썼을 때엔 함수 내부에서 boolean 배열을 생성할 수 없었습니다.
재귀호출이 수 없이 많이 수행되기 때문에 지나치게 많은 메모리 낭비로 이어지기 때문
입니다. 그래서 어쩔 수 없이 static 변수로 선언하고 함수 내에서 `true false`로 계속
바꾸어 주는 작업이 필요했습니다. 하지만 비트마스크를 사용할 땐 int형 변수를 하나 더
생성하는게 그렇게 큰 메모리 낭비로 이어지지 않을 거라 생각하고 함수의 인자로 넣어서
키고 끄는 과정을 생략할 수 있었습니다.

## ✅ 후기
비트마스크를 계속 연습해보려 했는데 좋은 기회가 되었던 문제였습니다. 문제의 난이도가
올라 갈수록 비트마스크를 활용해야 하는 문제가 많기 때문에 boolean 배열의 사용을 피하고
비트마스크를 계속 사용해보는 습관을 길러야겠습니다.