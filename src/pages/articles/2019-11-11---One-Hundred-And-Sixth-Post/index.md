---
title: "Bitwise Operators in Solidity"
date: "2019-11-11T07:52:13.121Z"
layout: post
draft: false
path: "/posts/one-hundred-and-sixth-post/"
category: "Ethereum"
tags:
  - "Solidity"
  - "Bitwise Operators"
description: "This is a post about what bitwise operators are in Solidity."
---

## What is a Bitwise Operator? 
In 4 + 5, '4' and '5' are operands and the '+' is an operator. There are several types of operators such as '+' which is an arithmetic operator, a '||', which is a type of logical operator. Overall, there are arithmetic, comparison, logical, assignment, and conditional operators. 

Bitwise operators include the following...

## Bitwise Operators and Example Use
```js
 // Bitwise Operators
    // & Bitwise AND 
    // | Bitwise OR 
    // ^ Bitwise exclusive OR 
    // ~ Bitwise negation
    // >> Bitwise right shift
    // << Bitwise left shift
    var orValue = 0x02 | 0x01; // orValue = 0x03
    uint shiftValue = 0x01 << 2; // shiftValue = 4
```
(Source:<a href="https://www.toshblocks.com/solidity/operators-arithmetic-logical-bitwise/">Tosh Blocks | Solidity | Operators</a>, <a href="https://www.blockchain-council.org/solidity/operators-arithmetic-logical-bitwise/"> Blockchain Council: Operators</a>) 

## Explanation of Bitwise Operators

The Tutorial Points on Bitwise Operators breaks down exactly what each bitwise operator does: 

![bitwise(1)](./bitwise(1).png)

(Source: <a href="https://www.tutorialspoint.com/solidity/solidity_operators.htm">Tutorial Points: Solidity Bitwise Operators</a>)

![bitwise(2)](./bitwise(2).png)

(Source: <a href="https://www.tutorialspoint.com/solidity/solidity_operators.htm">Tutorial Points: Solidity Bitwise Operators</a>)


## Example of Bitwise Operators in Solidity

Navigate in another window in your browser to Remix.ethereum.org and pick the right solidity compiler (0.5.0), compile, then deploy the following code: 

```javascript
pragma solidity ^0.5.0;

contract SolidityTest {
   uint storedData; 
   constructor() public{
      storedData = 10;   
   }
   function getResult() public view returns(string memory){
      uint a = 2; // local variable
      uint b = 2;
      uint result = a & b;  // bitwise operation
      return integerToString(result); 
   }
   function integerToString(uint _i) internal pure 
      returns (string memory) {
      if (_i == 0) {
         return "0";
      }
      uint j = _i;
      uint len;
      
      while (j != 0) {
         len++;
         j /= 10;
      }
      bytes memory bstr = new bytes(len);
      uint k = len - 1;
      
      while (_i != 0) {
         bstr[k--] = byte(uint8(48 + _i % 10));
         _i /= 10;
      }
      return string(bstr);//access local variable
   }
}
```
When you click on the function getResult(), the result you get will appear ("0: string: 2").

(Source: <a href="https://www.tutorialspoint.com/solidity/solidity_bitwise_operators.htm">Tutorials Point: Solidity</a>)

## Further Reading on Bitwise Operators: 

<a href="https://medium.com/@imolfar/bitwise-operations-and-bit-manipulation-in-solidity-ethereum-1751f3d2e216">Bitwise Operations and Bit Manipulation in Solidity</a><br/>

<a href="https://solidity.readthedocs.io/en/v0.5.12/types.html">Solidity Docs: Types (v. 0.5.12 (Latest at the time of this blog post))</a>