# cisco-js-questions

## 1) Double Base Palindrome

[https://www.hackerrank.com/contests/projecteuler/challenges/euler036/problem](https://www.hackerrank.com/contests/projecteuler/challenges/euler036/problem)

Double base Palindrome as the name suggest is a number which is Palindrome in 2 bases. One of the base is 10 i.e. decimal and another base is k.(which can be 2 or others). 

Note : The palindromic number, in either base, may not include leading zeros. 

Example : The decimal number, 585 = 10010010012 (binary), is palindromic in both bases. 

A Palindrome is a word, phrase, number, or other sequence of characters which reads the same backward as forward, such as madam or 12321.

Find the sum of all numbers less than n which are palindromic in base 10 and base k.

Examples: 


Input :  10 2

Output : 25

Explanation : 

(here n = 10 and k = 2)

1 3 5 7 9 (they are all palindrome 

in base 10 and 2) so sum is : 1 + 3 + 5 + 7 + 9 = 25

Input :  100 2

Output : 157

Explanation : 1 + 3 + 5 + 7 + 9 + 33 + 99 = 157

```javascript
function palindromeSum(value, base) {
  let sum = 0;
  for (let i = 1; i <= value; i++) {
    sum += isPalindrome(i, base);
  }
  console.log({ sum });
  return sum;
}

function isPalindrome(i, base) {
  // creating temp variable
  let temp = i;

  // stores reverse of the value
  let m = 0;

  // reversing the value
  while (temp > 0) {
    m = (temp % 10) + m * 10;
    temp = parseInt(temp / 10, 10);
  }
  // if actual number equal to reversed value
  if (m === i) {
    // Converting to base
    let str = numberIntoString(m, base);
    let str1 = str.split("").reverse().join("");

    if (str1 === str) {
      return i;
    }
  }
  return 0;
}

function numberIntoString(n, base) {
  let str = "";
  while (n > 0) {
    let digit = n % base;
    n = parseInt(n / base, 10);
    str += `${digit}`;
  }
  return str;
}

palindromeSum(5, 2);

```

## 2) Counting Fractions

[https://www.hackerrank.com/contests/projecteuler/challenges/euler072/problem](https://www.hackerrank.com/contests/projecteuler/challenges/euler072/problem)

```javascript
/*

Q) Consider the fraction, n/d, where n and d are positive integers. If n<d and HCF(n,d)=1, it is called a reduced proper fraction.

If we list the set of reduced proper fractions for d ≤ 8 in ascending order of size, we get:

1/8, 1/7, 1/6, 1/5, 1/4, 2/7, 1/3, 3/8, 2/5, 3/7, 1/2, 4/7, 3/5, 5/8, 2/3, 5/7, 3/4, 4/5, 5/6, 6/7, 7/8

It can be seen that there are 21 elements in this set.

How many elements would be contained in the set of reduced proper fractions for d ≤ 1,000,000?

*/

function countingFractions(limit) {
  let sum = 0;
  const phi = Array.from({ length: limit + 1 }, (_, i) => i);

  for (let i = 2; i <= limit; i++) {
    if (phi[i] === i) {
      for (let j = i; j <= limit; j += i) {
        phi[j] = (phi[j] / i) * (i - 1);
      }
    }
    sum += phi[i];
  }
  return sum;
}

// easyway to understand

function countingFractions2(n) {
    let sum = 0;
    for (let i = 1; i < n; i++) {
        for (let j = i + 1; j <= n; j++) {
            if (gcd(i, j) === 1) {
                sum++;
            }
        }
    }
    return sum;
}

function gcd(a, b) {
  if (b === 0) {
    return a;
  }
  return gcd(b, a % b);
}

gcd(8,32);

// console.log(countingFractions(5));
// console.log(countingFractions2(8));
```

## 3) Perfect Substing

[https://leetcode.com/discuss/interview-question/1186735/cisco-oa-substrings-count-with-each-character-as-k](https://leetcode.com/discuss/interview-question/1186735/cisco-oa-substrings-count-with-each-character-as-k)

```javascript
/* 
 A string s comprised of digits from 0 to 9 contains a perfect substring if all the elements 
 within a substring occur exactly k times. Calculate the number of perfect substrings in s.


Example

s = 1102021222
k = 2
The 6 perfect substrings are:

s[0:1] = 11
s[0:5] = 110202
s[1:6] = 102021
s[2:5] = 0202
s[7:8] = 22
s[8:9] = 22

Function Description
Complete the function perfectSubstring in the editor below.

perfectSubstring has the following parameters:
str s: a string where the value of each element s[i] is described by the character at position i (where 0 ≤ i < n)
int k: an integer that denotes the required frequency of the substring

Output
int: an integer that represents the number of the perfect substrings in the given string

Constraints
1 ≤ sizeof(s) ≤ 10⁵
0 ≤ s[i] ≤ 9 (where 0 ≤ i < n)
1 ≤ sizeof(s) ≤ 10⁵

*/


function perfectSubstring(str, k) {
    const charArr = str.split("");
    let count = 0;
    const listPoss = [];
    const mapList = [];
    let i = 1;
  
    while (i <= str.length) {
      for (let j = 0; j < charArr.length - i + 1; j++) {
        const halve = charArr.slice(j, j + i);
        if (halve.length % k === 0) {
          listPoss.push(halve);
        }
      }
      i++;
    }
    listPoss.forEach((item) => {
      let tempObj = {};
      item.forEach((ob) => {
        if (tempObj[ob] === undefined || tempObj[ob] === null) {
          tempObj[ob] = 1;
        } else {
          tempObj[ob] += 1;
        }
      });
      mapList.push(tempObj);
    });
  
    mapList.forEach((item) => {
      let isValid = Object.keys(item).every((key) => item[key] === k);
      
      if (isValid) {
          count++;
        }
    });
  
  
    return count;
  }

console.log(perfectSubstring('1102021222', 2));
```

## 4) How Many Words

[https://leetcode.com/discuss/interview-question/1465225/tata-digital-coding-round-question](https://leetcode.com/discuss/interview-question/1465225/tata-digital-coding-round-question)

```javascript
function howManyWords(sentance) {
    let count = 0;
    const words = sentance.split(" ");
    const isStringHaveSpecialChars = (word) =>  /[@#$%^&*()_+\=\[\]{};':"\\|<>\/]+/.test(word);
    const isStringHaveNumbers = (word) =>   /[0-9]/.test(word);

    words.forEach(word => {
        const newWord = word.replace('-','');
        if (!isStringHaveSpecialChars(newWord) && !isStringHaveNumbers(newWord)) {
            count++;
        }
    });
    return count;
}


let sentance = 'jds dsaf Ikdf kdsa fkldsf, adsbf ldka ads? asd bfdal ds bf[l. akf dhj ds 878 dwa WE DE 7475 dsfh ds RAMU, 748 dj.';
let s2 = 'he is a good programmer, he won 865 competitions, but sometimes he dont. What do you think? All test-cases should pass. Done-done?';


console.log(howManyWords(s2));
```

## 5) Efficient Janitor / Efficient Vineet

[https://leetcode.com/discuss/interview-question/490066/efficient-janitor-efficient-vineet-hackerrank-oa](https://leetcode.com/discuss/interview-question/490066/efficient-janitor-efficient-vineet-hackerrank-oa)

```javascript
function efficientJanitor(arr) {
  arr.sort((a, b) => a - b);
  let left = 0;
  let right = arr.length - 1;
  let count = 0;

  while (left <= right) {

    if (left == right) {
      count++;
      break;
    }
    if (arr[left] + arr[right] <= 3.0) {
      left++;
      right--;
      count++;
    } else {
      right--;
      count++;
    }
  }  
  return count;
}

console.log(efficientJanitor([1.01, 1.99, 2.5, 1.5, 1.01]));
```