![alt text](../images/isScramble.png)
```javascript
function isScramble(s1, s2) {
    if (s1.length !== s2.length) {
        return false;
    }
    if (s1.length === 0 || s1 === s2) {
        return true;
    }
    const copy1 = s1.split("").sort().join("");
    const copy2 = s2.split("").sort().join("");
    if (copy1 !== copy2) {
        return false;
    }
    for (let i = 1; i < s1.length; i++) {
        const str1 = s1.slice(0, i);
        const str2 = s1.slice(i, s1.length);
        const str3 = s2.slice(0, i);
        const str4 = s2.slice(i, s2.length);
        const str5 = s2.slice(0, s2.length - i);
        const str6 = s2.slice(s2.length - i, s2.length);
        if (isScramble(str1, str3) && isScramble(str2, str4)) {
            return true;
        }
        if (isScramble(str1, str6) && isScramble(str2, str5)) {
            return true;
        }
    }
    return false;
}

isScramble("great", "rgeat");
```
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).
```javascript
function minWindow(s, t) {
    let res = "";
    if (t.length > s.length) {
        return res;
    }
    const target = p.split("").reduce((obj, val) => {
        if (obj[val]) {
            obj[val]++;
        } else {
            obj[val] = 1;
        }
        return obj;
    }, {});
    let left = 0, count = 0, minLen = s.length + 1;
    const map = {};
    s.split("").forEach((e, i) => {
        if (target[e]) {
            if (map[e]) {
                if (map[e] < target[e]) {
                    count++;
                }
                map[e]++;
            } else {
                map[e] = 1;
                count++;
            }
        }
        if (count === t.length) {
            let curr = s[left];
            while (!map[curr] || map[curr] > target[curr]) {
                if (map[curr] && map[curr] > target[curr]) {
                    map[curr]--;
                }
                left++;
                curr = s[left];
            }
            if (i - left + 1 < minLen) {
                res = s.slice(left, i + 1);
                minLen = i - left + 1;
            }
        }
    });
    return res;
}

minWindow("ADOBECODEBANC", "ABC");
```