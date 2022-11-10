```javaScript
// you can write to stdout for debugging purposes, e.g.
// console.log('this is a debug message');

function solution(N) {
    // write your code in JavaScript (Node.js 14)


    const binaryNum = N.toString(2);
    //console.log(binaryNum);

    // 첫번째는 무조건 1. 
    //console.log('first 1 comes first : '+binaryNum.indexOf('1'));

    // 그 다음 1은 어디에 있지? 
    //console.log('last 1 index : '+binaryNum.lastIndexOf('1'));

    // 처음 위치하는 1과 끝에 위치하는 1의 인덱스 번호로 문자열을 자른다.  
    // 끝에 1이 오지 않는 (첫번째 1이 마지막 1인) 아이들은 여기서 결과가 나오지 않음 
    const binaryGaps = binaryNum.slice(binaryNum.indexOf('1') + 1, binaryNum.lastIndexOf('1'));
    //console.log('binary gap : '+binaryGaps);

// 중간에 있는 1로 배열을 잘라 여러 개의 0 군집 배열을 만듦
// 모두 1로만 이루어져 있는 배열은 사이즈 0짜리 배열 여러개가 만들어짐 
    const zeroArr = binaryGaps.split('1');
    //console.log('zero arrays : '+zeroArr);

    //각 0으로 이루어진 배열의 길이구하기
    // map 은 ()안의 함수대로 배열을 새로 작성해준다. 
    // => 는 람다식으로, 배열의 각 부분의 길이만 반환하는 함수를 작성한 것이다.  
    const zeroCounted = zeroArr.map(param => param.length);
    // console.log('arrays lengths : '+zeroCounted);

    const longestBinaryGap = Math.max(...zeroCounted);
    // console.log('arrays longest lengths : '+longestBinaryGap);


    

    
    return longestBinaryGap;
}
```