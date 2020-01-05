# Arrays and Strings


### 1. Is Unique: Implement an algorithm to determine if a string has all unique characters. What if you cannot use additional data structures?

```javascript
function uniqueCharacters(str) {
  const ASCII_CHARS = 256;
  
  if(str.length > ASCII_CHARS) {
    return false;
  }
  
  const chars = Array(ASCII_CHARS).fill(false);
  
  for(let char of str){
    const index = char.charCodeAt(0);
    if (chars[index] === true) {
      return false;
    }
    chars[index] = true;
  }
  
  return true;
}

console.log(uniqueCharacters('abcd10jk')); // true
console.log(uniqueCharacters('hutg9mnd!nk9')); // false
```

### 2. Check Permutation: Given two strings, write a method to decide if one is a permutation of the other. 

```javascript
function isPermutation(str1, str2) {
  if (str1.length !== str2.length) {
    return false;
  }
  
  const map = new Map();
  
  for(const char of str1) {
    if(map.has(char)) {
      map.set(char, map.get(char) + 1);
    } else {
      map.set(char, 1);
    }
  }
  
  for(const char of str2) {
      if(map.has(char)) {
        const value = map.get(char);
        if(value === 0) {
          return false;
        } else {
          map.set(char, map.get(char) - 1);
        }
      }
  }
  
  for(const value of map.values()) {
    if(value !== 0) {
      return false;
    }
  }
  return true;

}

console.log(isPermutation("god", "dog")); // true
```

### 3. URLify: Write a method to replace all spaces in a string with '%20'.

```javascript
function replaceSpaces(str, trueLength) {
  let output = "";
  let chars = 0;

  for(let char of str) {
    if(char !== " ") {
      chars++;
    }
  }
  
  let spaces = trueLength - chars;
  
  for(let char of str) {
    if(char === " " && spaces > 0) {
      output += "%20";
      spaces--;
    } else if(char !== " ") {
      output += char;
    }
  }
  
  while(spaces > 0) {
    output += "%20";
    spaces--;
  }
  
  return output;
}

console.log(replaceSpaces("Mr 3ohn Smith", 13)); // "Mr%203ohn%20Smith"
```

### 3. Palindrome Permutation: Given a string, write a function to check if it is a permutation of a palindrome
```javascript
function isPermutationOfPalindrome(str) {
  let charCount = 0;
  let map = new Map();
 
  for(let char of str) {
    if (char === " ") {
      continue;
    }
    
    if(map.has(char)) {
      map.delete(char);
    } else {
      map.set(char, true);
    }
    
    charCount++;
  }
  
  if(charCount % 2 === 0) {
    return map.size === 0;
  } else {
    return map.size === 1;
  }
}

console.log(
  isPermutationOfPalindrome("tacoa cat") === true,
  isPermutationOfPalindrome("atco cat") === true,
  isPermutationOfPalindrome(" rac ecar rara ") === true
);
```

### 4. String Compression: Implement a method to perform basic string compression using the counts of repeated characters.

```javascript
function compress (str) {
  const map = new Map();
  let result = '';
  
  for(const char of str) {
    if(map.has(char)) {
      map.set(char, map.get(char) + 1);
    } else {
      map.set(char, 1);
    }
  }
  
  for(let [key, value] of map) {
    result += key + value;
  }
  
  return str.lenght >= result.lenght ? str : result;
}

console.log(compress('aabcccccaaa')); // "a5b1c5"
```

### 5. Rotate Matrix: Given an image represented by an NxN matrix, where each pixel in the image is 4 bytes, write a method to rotate the image by 90 degrees.

```javascript
function rotateMatrix(arr) {
    let n = arr.length - 1;
  
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n - i; j++) {
            let temp = arr[i][j];
          
            arr[i][j] = arr[n - j][n - i]; // top row
            arr[n - j][n - i] = temp; // right column
        }
    }

    return arr;
}


console.log(rotateMatrix([
  [1,2,3],
  [4,5,6],
  [7,8,9]
])); 

/* 
[
    [9, 6, 3], 
    [8, 5, 2], 
    [7, 4, 1]
] 
*/
```

### 6. String Rotation; Assume you have a method isSubs t rin g which checks if one word is a substring of another. Given two strings, s1 and s2, write code to check if s2 is a rotation of s1 using only one call to isSubstring [e.g. "waterbottle " is a rotation oP'erbottlewat")

```javascript
const isSubstring = (str1, str2) => str1.includes(str2);

function isRotation(str1, str2) {
  if(!str1 || !str2) {
    return false;
  }
  
  if(str1.length !== str2.length) {
    return false;
  }
  
  return isSubstring(str1 + str2, str2);
}

console.log(isRotation("waterbottle", "erbottlewat")); // true
console.log(isRotation("aacdf", "acda")); // false
```

### 7. Find the first unique character in a given string or an array

```javascript
function findFirstUniqueCharacter(str) {
  if(!str) return;
  
  const map = new Map();
  
  for(let char of str) {
      if(map.has(char)) {
        map.set(char, map.get(char) + 1);
      } else {
        map.set(char, 1);
      }
  }
  
  for(let [key, value] of map) {
    if(value === 1) {
      return key;
    }
  }
  return "None";
}



console.log(findFirstUniqueCharacter('foobar')); // f
console.log(findFirstUniqueCharacter('aabbccdef')); // d
console.log(findFirstUniqueCharacter('aabbcc')); // 'No Unique Character Found'
```