# 📢 알파코드

❓ **어려웠던 부분**

- 10, 20과 같이 0이 포함된 경우 10의 자리, 1의 자리를 하나씩 알파벳으로 바꾸면 안된다
  - 0인 경우에는 해당하는 알파벳이 존재하지 않는다
  - 해당 반례

✔ **해결법**

1. 반례가 존재할 상황을 모두 대처하여 조건문으로 예외 처리 해주기
   - 논리적인 방법에 입각한 것이 아닌 주먹구구식 해결
2. 입력된 숫자를 하나씩 순회하며 1 ~ 26까지의 알파벳을 생성할 수 있는 모두 확인한다
   - 10이상의 숫자는 그 뒤의 숫자도 확인하여 두 자리수를 비교한다
   - 마지막 경우 두 자리수를 확인할 때 `index`범위를 벗어나므로 `padding`으로 -1을 추가한다.

```python
def DFS(n, m, s):
    global cnt
    # 입력된 수를 끝까지 순회했을 경우 변경된 알파벳 출력
    if n == m:
        cnt += 1
        print(s)
        return
    else:
        # 1 ~ 26범위 안에 값이 해당하는지 확인하여 알파벳으로 변환진행한다.
        for i in range(1, 27):
            # 1 ~ 9까지는 한개의 자릿값이므로 n 위치만 확인 진행
            if num[n] == i:
                # 아스키 코드에서 대문자 알파벳 A가 65부터 시작하기 때문에 64를 더해준다.
                DFS(n + 1, m, s + chr(64 + i))
            elif i >= 10 and num[n + 1] != -1 and num[n] * 10 + num[n + 1] == i:
                DFS(n + 2, m, s + chr(64 + num[n] * 10 + num[n + 1]))
                

if __name__ == '__main__':
    num = list(map(int, input().rstrip())) + [-1]
    cnt = 0
    DFS(0, len(num) - 1, '')
    print(cnt)
```

