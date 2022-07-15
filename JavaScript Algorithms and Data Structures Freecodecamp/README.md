# JavaScript Algorithms and Data Structures Freecodecamp

* [Palindrome Checker](#palindrome-checker)

* [Roman Numeral Converter](#roman-numeral-converter)

* [Caesars Cipher](#caesars-cipher)

* [Telephone Number Validator](#telephone-number-validator)

* [Cash Register](#cash-register)




***

## Palindrome-Checker

Return true if the given string is a palindrome. Otherwise, return false.

A palindrome is a word or sentence that's spelled the same way both forward and backward, ignoring punctuation, case, and spacing.

Note: You'll need to remove all non-alphanumeric characters (punctuation, spaces and symbols) and turn everything into the same case (lower or upper case) in order to check for palindromes.

We'll pass strings with varying formats, such as ```racecar```, ```RaceCar```, and ```race CAR``` among others.

We'll also pass strings with special symbols, such as ```2A3*3a2```, ```2A3 3a2```, and ```2_A3*3#A2```.

```javascript

function palindrome(str) {

  str = str.toLocaleLowerCase();

  let pattern = /[a-z0-9]/g;

  let text = str.match(pattern);

  let output = true;

  console.log(text);

  let length = text.length;
  let lastIndex = text.length - 1;
  let i = 0;

  console.log(text.length);

  while (i < length){
    if (text[i] !== text[lastIndex - i]){
      output = false;
      console.log(output);
    }
    i++;
  }

  console.log(output);
  return output;
}

palindrome("A man, a plan, a canal. Panama");

```


***

## Roman-Numeral-Converter

Convert the given number into a roman numeral.

All roman numerals answers should be provided in upper-case.

```javascript

function convertToRoman(num) {

  let map = {
    M:  1000,
    CM: 900,
    D:  500,
    CD: 400,
    C:  100,
    XC: 90,
    L:  50,
    XL: 40,
    X:  10,
    IX: 9,
    V:  5,
    IV: 4,
    I:  1,
  };

  let output = "";

  for (var n of Object.keys(map)){
    output += n.repeat(Math.floor(num/map[n]));
    num = num % map[n];
  }

  console.log(output.constructor);
  console.log(output);
  return output;
}

convertToRoman(2);

```

***

## Caesars-Cipher

One of the simplest and most widely known ciphers is a Caesar cipher, also known as a shift cipher. In a shift cipher the meanings of the letters are shifted by some set amount.

A common modern use is the ROT13 cipher, where the values of the letters are shifted by 13 places. Thus A ↔ N, B ↔ O and so on.

Write a function which takes a ROT13 encoded string as input and returns a decoded string.

All letters will be uppercase. Do not transform any non-alphabetic character (i.e. spaces, punctuation), but do pass them on.

```javascript

function rot13(str) {

  var alph = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');
  var output = '';

  for (var i=0; i<str.length; i++){
    let curr = str[i];
    let pattern = /[^A-Z]/g;
    if (curr.match(pattern)){
      output += curr;
      continue;
    }

    let currIndex = alph.indexOf(curr);
    let move = 13 + currIndex ;

    if (move > 25){
      move = move - 26;
    } else if (move < 0){
      move = 26 + move;
    }

    console.log(curr);
    console.log(alph.indexOf(curr));
    console.log(move);

    let n = alph[move];
    console.log('n: '+n);

    output = output + n;
    console.log(output);
  }

  console.log(output);
  return output;
}

rot13("SERR CVMMN!");

```


***

## Telephone-Number-Validator

Return true if the passed string looks like a valid US phone number.

The user may fill out the form field any way they choose as long as it has the format of a valid US number. The following are examples of valid formats for US numbers (refer to the tests below for other variants):

```555-555-5555```
```(555)555-5555```
```(555) 555-5555```
```555 555 5555```
```5555555555```
```1 555 555 5555```

For this challenge you will be presented with a string such as ```800-692-7753``` or ```8oo-six427676;laskdjf```. Your job is to validate or reject the US phone number based on any combination of the formats provided above. The area code is required. If the country code is provided, you must confirm that the country code is 1. Return true if the string is a valid US phone number; otherwise return false.

```javascript

function telephoneCheck(str) {

  const pattern = [
    //555-555-5555
    /^(\d{3})-(\d{3})-(\d{4})$/g,
    //1 555-555-5555
    /^1 (\d{3})-(\d{3})-(\d{4})$/g,    

    //(555)555-5555
    /^(\(\d{3}\))(\d{3})-(\d{4})$/g,

    //(555) 555-5555
    /^(\(\d{3}\)) (\d{3})-(\d{4})$/g,

    //555 555 5555
    /^(\d{3}) (\d{3}) (\d{4})$/g,

    //5555555555
    /^(\d{10})$/g,

    //1 555 555 5555
    /^1 (\d{3}) (\d{3}) (\d{4})$/g,

    //1 (555) 555-5555
    /^1 (\(\d{3}\)) (\d{3})-(\d{4})$/g,

    //1(555)555-5555
    /^1(\(\d{3}\))(\d{3})-(\d{4})$/g

  ];

  return pattern.some(check);

  function check(pattern){
    return pattern.test(str);
  }

}

telephoneCheck("555-555-5555");

```

***


## Cash-Register

Design a cash register drawer function checkCashRegister() that accepts purchase price as the first argument (price), payment as the second argument (cash), and cash-in-drawer (cid) as the third argument.

cid is a 2D array listing available currency.

The checkCashRegister() function should always return an object with a status key and a change key.

Return {status: "INSUFFICIENT_FUNDS", change: []} if cash-in-drawer is less than the change due, or if you cannot return the exact change.

Return {status: "CLOSED", change: [...]} with cash-in-drawer as the value for the key change if it is equal to the change due.

Otherwise, return {status: "OPEN", change: [...]}, with the change due in coins and bills, sorted in highest to lowest order, as the value of the change key.

> Currency Unit	Amount
> Penny	.01 (PENNY)
> Nickel	.05 (NICKEL)
> Dime	.1 (DIME)
> Quarter	.25 (QUARTER)
> Dollar	 (ONE)
> Five Dollars	 (FIVE)
> Ten Dollars	0 (TEN)
> Twenty Dollars	0 (TWENTY)
> One-hundred Dollars	00 (ONE HUNDRED)

See below for an example of a cash-in-drawer array:

```
[
  ["PENNY", 1.01],
  ["NICKEL", 2.05],
  ["DIME", 3.1],
  ["QUARTER", 4.25],
  ["ONE", 90],
  ["FIVE", 55],
  ["TEN", 20],
  ["TWENTY", 60],
  ["ONE HUNDRED", 100]
]
```

Here is the solution

```javascript

function checkCashRegister(price, cash, cid) {

  const money = {
  "ONE HUNDRED": 100,
  "TWENTY": 20,
  "TEN": 10,
  "FIVE": 5,
  "ONE": 1,
  "QUARTER": 0.25,
  "DIME": 0.10,
  "NICKEL": 0.05,
  "PENNY": 0.01,
  }

  let map = new Map();

  for (var i=0; i<cid.length; i++){
    let amount = cid[i][1];
    map.set(cid[i][0], amount);
  }

  let cidTotal = 0;
  for (var c=0; c<cid.length; c++){
    cidTotal = ((cidTotal + cid[c][1])*100)/100;
  }

  let checkCid = cidTotal
  console.log('checkCid: '+ checkCid);


  let list = [];
  let amount = '';

  let needChange = cash - price;
  let checkChange = needChange;

  console.log('checkChange:' + checkChange);  


  for (var m of Object.keys(money)) {
    let rollover = 0;
    if (needChange > money[m]){
      console.log(m);
      if (map.get(m) === 0 || needChange > cidTotal){
        continue;
      }       
      let n = needChange % money[m];
      console.log("map: "+map.get(m));
      if (n*money[m] > map.get(m)){
        rollover = needChange - map.get(m);
      } else {
        rollover = n;
      }
      rollover = rollover.toFixed(2);
      console.log('rollover: '+rollover);
      let pushAmount = needChange - rollover;
      pushAmount = Math.round(pushAmount * 100) / 100;
      console.log(pushAmount);
      list.push([m, pushAmount]);
      needChange = rollover;      
    } 
    cidTotal -= map.get(m);
  }

  console.log("list: "+ list);



  if (checkChange > checkCid || list.length === 0){
    return {status: "INSUFFICIENT_FUNDS", change: []};
  } else if ( checkChange === checkCid){
    return {status: "CLOSED", change: cid};
  } else {
    return {status: "OPEN", change: list};
  } 
  
}

checkCashRegister(19.5, 20, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 1], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]);

```
