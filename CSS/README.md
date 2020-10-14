# CSS
## 목차
- 텍스트 관련 속성
  - [white-space](#white-space)

## 텍스트 관련 속성
### [white-space](https://developer.mozilla.org/ko/docs/Web/CSS/white-space)
요소가 공백 문자를 처리하는 법을 지정
- `normal` : 연속 공백 합침, **개행문자도 다른 공백과 동일하게 처리**, 자동 줄바꿈
- `nowrap` : 연속 공백을 합침, 줄바꿈은 `<br>` 에서만 발생
- `pre` : 연속 공백 유지, 줄바꿈은 개행 문자 & `<br>`
- `pre-wrap` : 연속 공백 유지, 줄바꿈은 개행 문자 & `<br>`, 자동 줄바꿈
- `pre-line` : 연속 공백 합침, 줄바꿈은 개행 문자 & `<br>`, 자동 줄바꿈
- `break-spaces` : `pre-wrap`과 동일한데 다음 차이점 존재
  - 연속 공백이 줄의 끝에 위치하더라도 공간을 차지
  - 연속 공백의 중간과 끝에서도 자동으로 줄 바꿈
  - 유지한 연속 공백은 요소 바깥으로 넘치지 않고, 공간을 차지하므로 박스 크기에 영향을 미침(`min-content`, `max-content`)
 
