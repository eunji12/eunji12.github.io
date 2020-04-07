## 2018 카카오 기출문제 (하) 비밀지도
1. 비트연산
- and: a&b
- or: a|b
- xor: a^b (서로 다른 값일때 1)
- not: ~a (모든 비트값을 반대로)

2. 바이너리 변환
- 10 -> 2진 String 변환 Integer.toBinaryString(i);
- 10 -> 8진 String 변환 Integer.toOctalString(i);
- 10 -> 16진 String변환 Integer.toHexString(i);
- 2, 8, 16진수 -> 10진수 변환시 Integer.partInt(i, (2 or 8 or 16));

3. 문제 요약  - 아래 참고 링크 확인
----
#비밀지도
- 지도는 한 변의 길이가### n
인 정사각형 배열 형태로, 각 칸은“공백”(““) 또는”벽“(”#”) 두 종류로 이루어져 있다.
- 전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각“지도 1”과“지도 2”라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.
- “지도 1”과“지도 2”는 각각 정수 배열로 암호화되어 있다.
- 암호화된 배열은 지도의 각 가로줄에서 벽 부분을### 1
, 공백 부분을### 0 으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

---
4. 작성코드
``` java
class Solution {
  public String[] solution(int n, int[] arr1, int[] arr2) {
      String[] answer = new String[n];
      for(int i=0; i<n; i++){
          answer[i] = String.format("%"+n+"s",Integer.toBinaryString(arr1[i]|arr2[i])).replace("1","#").replace("0"," ");
      }
      return answer;
  }
}
```

5. 처리 중 발생한 문제
- Integer.toBinaryStirng()을 사용했을 때 변환된 이진수의 첫 값이 0인 경우 0이 생략되어 자리수가 맞지 않았다. 
ex. 010111이 출력되어야하는데  맨 앞이 0인 경우 10111로 출력
—> String.format(‘%6s’, str) 을 사용하여 자릿수를 맞추고 0 -> ” “, 1 -> “#”으로 변환하였다. 이 때 맨앞의 0은 자릿수를 포맷에 맞출 경우 자동 공백 출력되어 치환이 필요 없었다.
- 평소 ArrayList<String>()과 같은 컬렉션을 많이 사용하다 보니 String 배열에 값을  넣으려니 생소했다. answer.add() 혹은 answer.append()와 같은 메서드? 호출만 생각나서 어떻게 값을 대입해야하는지 검색으로 확인을 했다. (결론. 인스턴스 생성 후/사이즈지정 후 그냥 대입 하면됨)

6. 메모(느낀점)
- replace로 변환 처리를 했는데 replaceAll을 썼어야했을까? 평소에 생각없이 대충 써버릇해서 차이가 정확히 기억이 안나는 것들은 다시 찾아보고 정확하게 기억하자
**replaceAll 은 정규식 사용 가능 / 정규식도 다시 공부하자
- String.format()은 처음 써봤는데 자바에서의 lpad() 가 있다면 이 걸 사용했을 것이다. 찾아보니 org.apache.commons.lang.StringUtils에서 leftPad() 를 제공하긴한다.
- 정수를 이진으로 변환하는 방법을 검색했는데 어떤 사람은 값을 1이 남을때까지 2로 나눠 나머지를 배열에 저장 후  값을 역순으로 출력해 찐 2진수 구하는 방법을 구현해서 2진 값을 구했다. 오랜만이네.. 이거 계산하는거 ~

7. 참고  
[카카오 신입 공채 1차 코딩 테스트 문제 해설 – tech.kakao.com](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)
[코딩벌레 :: Java자바 진수변환(10진수->2진수,8진수,16진수)](https://dpdpwl.tistory.com/92)
[Java 연산자 비트연산자 & 쉬프트 연산자 (Bit & shift operator) : 네이버 블로그](http://blog.naver.com/PostView.nhn?blogId=choigohot&logNo=40193772915)
[java - 배열에 새로운 원소를 추가하려면 어떻게 해야하죠? | Hashcode](https://hashcode.co.kr/questions/1028/%EB%B0%B0%EC%97%B4%EC%97%90-%EC%83%88%EB%A1%9C%EC%9A%B4-%EC%9B%90%EC%86%8C%EB%A5%BC-%EC%B6%94%EA%B0%80%ED%95%98%EB%A0%A4%EB%A9%B4-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%B4%EC%95%BC%ED%95%98%EC%A3%A0)
[Java - convert int to binary String with leading zeros - DirAsk](https://dirask.com/q/java-convert-int-to-binary-string-with-leading-zeros-OpBXq1)

