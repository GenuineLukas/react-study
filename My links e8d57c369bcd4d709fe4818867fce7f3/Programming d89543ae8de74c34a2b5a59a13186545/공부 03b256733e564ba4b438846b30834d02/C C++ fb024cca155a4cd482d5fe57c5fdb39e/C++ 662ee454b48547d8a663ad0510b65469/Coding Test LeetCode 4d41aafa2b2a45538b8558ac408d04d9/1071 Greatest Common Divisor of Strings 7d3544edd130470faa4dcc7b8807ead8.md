# 1071.  Greatest Common Divisor of Strings

For two strings `s` and `t`, we say "`t` divides `s`" if and only if `s = t + t + t + ... + t + t` (i.e., `t` is concatenated with itself one or more times).

Given two strings `str1` and `str2`, return *the largest string* `x` *such that* `x` *divides both* `str1` *and* `str2`.

**Example 1:**

```
Input: str1 = "ABCABC", str2 = "ABC"
Output: "ABC"

```

**Example 2:**

```
Input: str1 = "ABABAB", str2 = "ABAB"
Output: "AB"

```

**Example 3:**

```
Input: str1 = "LEET", str2 = "CODE"
Output: ""

```

**Constraints:**

- `1 <= str1.length, str2.length <= 1000`
- `str1` and `str2` consist of English uppercase letters.

내 코드

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
bool check(string str, string token){
    string start;
    int it = str.length()/token.length();
    for(int i=0; i<it; i++){
        start += token;
    }
    if(str == start) return true;
    else return false;
}
public:
    string gcdOfStrings(string str1, string str2) {
        string ret;
        
        string str;
        int len = min(str1.length(), str2.length());
        for(int i=0; i<len; i++){
            str += str2[i];
            if(check(str1, str) && check(str2, str)) ret=str;
        }
        return ret;
    }
};
```

모범 답안

```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        return (str1 + str2 == str2 + str1)? 
        str1.substr(0, gcd(size(str1),size(str2))): "";
    }
};
```

str1과 str2 둘 다 같은 어떠한 공약수로 나눌 수 있다는 것은

str1 + str2 == str2 + str1 이라는 뜻이고 c++에는 gcd라는 최대 공약수를 구하는 라이브러리가 있다. 그걸 사용해서 str1과 str2간의 최대 공약수를 구한 후 그만큼 substr해주면 된다.. ㅜㅜ