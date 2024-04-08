# Code questions from karat
## Sources
1. https://www.jianshu.com/p/fdbcba5fe5bc
## Questions
1. [68. Text Justification](https://leetcode.com/problems/text-justification)  
   Refer https://www.1point3acres.com/bbs/thread-1037241-1-1.html  
    1. Wrap Lines  
       描述： 实现函数wrapLines(String[] words, int maxLen): 给一个string数组 string[] words，要求把word依次用-连接拼凑成n个句子，每个句子长度不超过maxLen。
#例如：
#输入words = {"a", "b", "cd", "e"}, maxLen = 4, 输出 {"a-b", "cd-e"}
#输入words = {"a", "b", "cd", "e"}, maxLen = 10, 输出 {"a-b-cd-e"}
更详细的描述见 https://www.1point3acres.com/bbs/thread-1038275-1-1.html

         我的答案见：https://leetcode.com/playground/WyMSj8Gx 
    3. ReflowAndJustify  
       描述：#Given an array containing lines of text and a new maximum width, re-flow the text to fit the new #width. Each line should have the exact specified width. If any line is too short, insert '-' (as #stand-ins for spaces) between words as equally as possible until it fits.A single word on a line is not padded with spaces  
       例子：lines = [ "The day began as still as the","night abruptly lighted with","brilliant flame" ]
   结果：[ "The--day--began-as-still","as--the--night--abruptly","lighted--with--brilliant","flame" ]

         我的答案见 https://leetcode.com/playground/SwmqoeCJ
2. Given a list of people who enter and exit, find the people who entered without
their badge and who exited without their badge.
例子：badgeRecords = [["Martha",   "exit"],
                ["Paul",     "enter"],
                ["Martha",   "enter"],
                ["Martha",   "exit"],
                ["Jennifer", "enter"],
                ["Paul",     "enter"],
                ["Curtis",   "enter"],
                ["Paul",     "exit"],
                ["Martha",   "enter"],
                ["Martha",   "exit"],
                ["Jennifer", "exit"],]
结果： ["Paul", "Curtis"], ["Martha"]     

   我的答案见： https://leetcode.com/playground/io7YdAK2
4. Invalid access in an hour  
   描述：We want to find employees who badged into our secured room unusually often. We have an unordered list of names and access times over a single day. Access times are given as three or four-digit numbers using 24-hour time, such as "800" or "2250".
Write a function that finds anyone who badged into the room 3 or more times in a 1-hour period, and returns each time that they badged in during that period. (If there are multiple 1- hour periods where this was true, just return the first one.)
   例子：badgeRecords = [
  ["Paul", "1315"],
  ["Jennifer", "1910"],
  ["John", "830"],
  ["Paul", "1355"],
  ["John", "835"],
  ["Paul", "1405"],
  ["Paul", "1630"],
  ["John", "855"],
  ["John", "915"],
  ["John", "930"],
  ["Jennifer", "1335"],
  ["Jennifer", "730"],
  ["John", "1630"],
]
print(getMultipleAccessInHour(badgeRecords))

   结果：{"John": [830, 835, 855, 915, 930]， "Paul": [1315, 1355, 1405]}
   
   我的答案见： https://leetcode.com/playground/UmNRzSo5 
1. 给一些单词和一个字符串，判断是否有单词可以有字符串中的字母拼成，其中字符串中每个字母只能用一次。
    例子：["cat", "baby", "dog", "bird", "car", "ax"],字符串 "tcabnihjs”
   
    我的答案见： https://leetcode.com/playground/gq8DxSu8
1. 给一个全是字符的二位数组，和一个目标字符串，判断这个字符串是否可以有二位数组中的某些字符组成， 如果是输出这些字符的具体位置。在二位数组中，只可以向下或者向右移动。

   例子： grid = [["c", "c", "x", "t", "i", "b"],  
        ["c", "c", "a", "t", "n", "i"],  
        ["a", "c", "n", "n", "t", "t"],  
        ["t", "c", "s", "i", "p", "t"],  
        ["a", "o", "o", "o", "a", "a"],  
        ["o", "a", "a", "a", "o", "o"],  
        ["k", "a", "i", "c", "k", "i"]]    
  s = "catnip"   
   结果： [(1, 1), (1, 2), (1, 3), (2, 3), (3, 3), (3, 4)]  
   我的答案见： https://leetcode.com/playground/inuEZpUh
1. [811. Subdomain Visit Count](https://leetcode.com/problems/subdomain-visit-count)
   The key is to use hash map to increase count for domain, and then when seeing dot, increase count for parent domain.
   我的答案：
   <details>

      ```python
          def subdomainVisits(self, cpdomains: List[str]) -> List[str]:
        domainFreq = Counter()
        for cpdomain in cpdomains:
            freq, domain = cpdomain.split()
            freq = int(freq)
            domainFreq[domain] += freq
            print(domain)
            for i in range(len(domain)):
                if domain[i] == ".":
                    domainFreq[domain[i + 1:]] += freq
            
        return ["{} {}".format(freq, domain) for domain, freq in domainFreq.items()]
      ```
   </details>
1. 给每个user访问历史记录，找出两个user之间longest continuous common history
   例子：
   输入: [
["3234.html", "xys.html", "7hsaa.html"], // user1
["3234.html", ''sdhsfjdsh.html", "xys.html", "7hsaa.html"] // user2 ], user1 and user2 (指定两个user求intersect)
   输出:["xys.html", "7hsaa.html"]

   我的答案：https://leetcode.com/playground/36tWr9Tb
1. Ads Conversion Rate
   描述：a list of user ids + IPs, a list of user ids who have made purchases, a list of advertisement clicks with user IPs.
Each user id has at most 1 IP.
Output: for each ad, output the number of clicks and the number of purchases.

   例子：completedId = ["3123122444", "234111110", "8321125440", "99911063"]  
adClicks = ["122.121.0.1,2016-11-03 11:41:19,Buy wool coats for your pets",
            "96.3.199.11,2016-10-15 20:18:31,2017 Pet Mittens",
            "122.121.0.250,2016-11-01 06:13:13,The Best Hollywood Coats",
            "82.1.106.8,2016-11-12 23:05:14,Buy wool coats for your pets",
            "92.130.6.144,2017-01-01 03:18:55,Buy wool coats for your pets",
            "92.130.6.145,2017-01-01 03:18:55,2017 Pet Mittens"]  
userIps = ["2339985511,122.121.0.155", "234111110,122.121.0.1",
            "3123122444,92.130.6.145",
"39471289472,2001:0db8:ac10:fe01:0000:0000:0000:0000",
            "8321125440,82.1.106.8", "99911063,92.130.6.144"]  
   答案： ['3 of 3 Buy wool coats for your pets', '1 of 2 2017 Pet Mittens', '0 of 1 The Best Hollywood Coats']

   我的答案见：https://leetcode.com/playground/9J7goUJq
   
1. [1160. Find Words That Can Be Formed by Characters](https://leetcode.com/problems/find-words-that-can-be-formed-by-characters)  
   Compare character frequency
1. [2133. Check if Every Row and Column Contains All Numbers](https://leetcode.com/problems/check-if-every-row-and-column-contains-all-numbers)
2. [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku)
   Easy. Just use hash set.
1. [79. Word Search](https://leetcode.com/problems/word-search)  
   Backtrack.
1. [718. Maximum Length of Repeated Subarray](https://leetcode.com/problems/maximum-length-of-repeated-subarray)  
   Use dp[i][j] to represent the longest common suffix between nums1[0..i-1] and nums2[0..j-1].
1. [1275. Find Winner on a Tic Tac Toe Game](https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game)
1. You are going on a camping trip, but before you leave you need to buy groceries. To optimize your time spent in the store, instead of buying the items from your shopping list in order, you plan to buy everything you need from one department before moving to the next.  

   Given an unsorted list of products with their departments and a shopping list, return the time saved in terms of the number of department visits eliminated.  

   更详细的描述见： https://www.1point3acres.com/bbs/thread-1045441-1-1.html。帖子里还有另外一题，我觉得比较难，如果有时间时也可酷看看。

   我的答案见：https://leetcode.com/playground/LZxQF7PH
    
1. [348. Design Tic-Tac-Toe](https://leetcode.com/problems/design-tic-tac-toe)
2. [794. Valid Tic-Tac-Toe State](https://leetcode.com/problems/valid-tic-tac-toe-state)
