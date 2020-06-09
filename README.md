# rules
정규식, validation 모음

```javascript
/*
  사업자 등록번호 검증
  세무서코드(3자리) – 사업구분코드(2자리) – 일련번호+오류검증코드 (5자리) = 총 10자리 ###-##-######
*/
export const checkBn = value => {
  const valueMap = value
    .replace(/-/gi, "")
    .split("")
    .map(function(item) {
      return parseInt(item, 10);
    });

  if (valueMap.length === 10) {
    const keys = [1, 3, 7, 1, 3, 7, 1, 3, 5];
    let checkSum = 0;

    for (let i = 0; i < keys.length; i++) {
      checkSum += keys[i] * valueMap[i];
    }

    checkSum += parseInt((keys[8] * valueMap[8]) / 10, 10);
    // return Math.floor(valueMap[9]) === 10 - (checkSum % 10);
    return Math.floor(valueMap[9]) === (10 - (checkSum % 10)) % 10;
  }

  return false;
};
```

```javascript
// 숫자 포맷 1000단위
const isNumber = (num) => !Number.isNaN(parseInt(num));
const numberFormat = (num) => isNumber ? num.toLocaleString() : "";

// array sort
const arr = [0, 2, 3, 1]
arr.sort((a, b) => a - b)
console.log('오름차순', ...arr)
arr.sort((a, b) => b - a)
console.log('내름차순', ...arr)
```

