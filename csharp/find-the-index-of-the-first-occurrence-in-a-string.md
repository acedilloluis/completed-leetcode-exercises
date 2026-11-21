## Find the Index of the First Occurrence in a String
### Problem Statement
Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.Example 1:Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
Example 2:Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
Constraints:1 <= haystack.length, needle.length <= 104haystack and needle consist of only lowercase English characters.
### Solution
```csharp
public class Solution {
    public int StrStr(string haystack, string needle) 
    {
        //kmp algorithm
        if (needle.Length == 0 || needle.Length > haystack.Length)
            return -1;

        //compute lps (longest prefix suffix) array
        //stores length of longest proper prefix of needle[0..i] that is also suffix of needle[0..i]
        int[] lps = new int[needle.Length];
        //length of previous longest prefix suffix
        int len = 0;
        int i = 1;

        while (i < needle.Length)
        {
            if (needle[i] == needle[len])
            {
                len++;
                lps[i] = len;
                i++;
            }
            else
            {
                //previous prefix match so fallback
                if (len != 0)
                    len = lps[len - 1];
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }

        int k = 0;
        int j = 0;
        
        while (k < haystack.Length)
        {
            if (haystack[k] == needle[j])
            {
                k++;
                j++;
            }

            if (j == needle.Length)
                return k - j;

            if (k < haystack.Length && haystack[k] != needle[j])
            {
                //partial match occurred
                if (j != 0)
                    j = lps[j - 1];
                else
                    k++;
            }
        }

        return -1;
    }
}
```
### Notes
