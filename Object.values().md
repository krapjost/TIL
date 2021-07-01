# Object.values()

`**Object.values()**` 메소드는 전달된 파라미터 객체가 가지는 (열거 가능한) 속성의 값들로 이루어진 배열을 리턴합니다. 이 배열은 [`for...in`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in) 구문과 동일한 순서를 가집니다. (for in 반복문은 프로토타입 체인 또한 열거한다는 점에서 차이가 있습니다.)



 validateAdminInfoInput을 부를 때 반복되는 input을 깨끗하고 읽기쉽게 넣어주고 싶다.

```javascript
  function validateAdminInfoInput(dsptch, ...input) {
    const [boxAdminId, boxAdminPw, pwConfirm, boxAdminName] = input;
    const pwMatch = boxAdminPw === pwConfirm;
    if (!boxAdminId) return showMsg('관리자 아이디를 입력해주세요', dsptch);
    if (!boxAdminPw) return showMsg('관리자 패스워드를 입력해주세요.', dsptch);
    if (!pwConfirm) return showMsg('패스워드 확인을 입력해주세요.', dsptch);
    if (!boxAdminName) return showMsg('관리자 이름을 입력해주세요', dsptch);
    if (!pwMatch) return showMsg('패스워드 확인이 일치하지 않습니다.', dsptch);
    return false;
  }

  async function doMakeFilingBox(boxInfos, dsptch) {
    const { boxAdminId, boxAdminName, boxAdminPw, pwConfirm } = boxInfos;
    if (
      !validateAdminInfoInput(
        dsptch,
        boxAdminId,
        boxAdminPw,
        pwConfirm,
        boxAdminName,
      )
    ) {
      return false;
    }
    setStartMake(false);
    const result = await subscription(boxInfos);
    console.log(result);
    return false;
  }
```



# Array.from()

`**Array.from()**` 메서드는 유사 배열 객체(array-like object)나 반복 가능한 객체(iterable object)를 얕게 복사해 새로운`Array` 객체를 만듭니다.

