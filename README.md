# leetcode

88.合并两个有序数组
var merge = function (nums1, m, nums2, n) {
  // 1. 合并
  nums1.splice(m, nums1.length - m, ...nums2);
  // 2. 排序
  nums1.sort((a, b) => {
    return a - b;
  });
};
415.字符串相加
var addStrings = function(num1, num2) {
  let i = num1.length - 1, j = num2.length - 1, add = 0;
  const ans = [];
  while (i >= 0 || j >= 0 || add != 0) {
    const x = i >= 0 ? num1.charAt(i) - '0' : 0;
    const y = j >= 0 ? num2.charAt(j) - '0' : 0;
    const result = x + y + add;
    ans.push(result % 10);
    add = Math.floor(result / 10);
    i -= 1;
    j -= 1;
  }
  return ans.reverse().join('');
};
3.无重复字符的最长子串
sliding window

1. 创建一个set
2. 两个指针，第一个指向字符串开头j, 第二个随着for循环遍历字符串
3. 如果set里面没有s[i]，说明目前为止还没有重复的字符，把s[i]添加到set里面，然后更新最大不重复字符数
4. 如果set里面有s[i]，则从set里开始删除s[j]，并且递增j，再检查set里是否有s[i]。如此反复重复知道set里没有s[i]为止
5. 重复34，直到遍历完整个字符串
   /**

 * Definition for singly-linked list.
 * function ListNode(val, next) {
 * this.val = (val===undefined ? 0 : val)
 * this.next = (next===undefined ? null : next)
 * }
   */
   var lengthOfLongestSubstring = function (s) {
     const set = new Set();
     let i = 0,
     j = 0,//只有需要的时候移动
     maxLength = 0;
     if (s.length === 0) {
   return 0;
     }
     for (i; i < s.length; i++) {
   if (!set.has(s[i])) {//没有重复的
     set.add(s[i]);
     maxLength = Math.max(maxLength, set.size);//当前长度和maxLength相比
   } else {//有重复的,删除重复的，添加新的
     while (set.has(s[i])) {
       set.delete(s[j]);//删除重复的
       j++;
     }
     set.add(s[i]);//没有s[i]的话添加新的
   }
     }
     return maxLength;
   };
   优雅解法：
   var lengthOfLongestSubstring = function(s) {
   if(s.length===0) return 0;
   const arr = [];
   let maxLength = 0;
   let i = 0,  j = 0;
   for(i; i < s.length; i++) {
       if(!arr.includes(s[i])){
           arr.push(s[i]);
           maxLength=Math.max(arr.length, maxLength)
       }else{
           while(arr.includes(s[i])){
               arr.shift()
               j++;
           }
           arr.push(s[i])
       }
   }
   return maxLength
   };
   165.比较版本号
   var compareVersion = function (version1, version2) {
   const v1 = version1.split('.');
   const v2 = version2.split('.');
   console.log(v1)
   console.log(v2)
   for (let i = 0; i < v1.length || i < v2.length; i++) {
       let x = 0, y = 0;
       if (i < v1.length) {
           x = parseInt(v1[i]);
       }
       if (i < v2.length) {
           y = parseInt(v2[i]);
       }
       if (x > y) {
           return 1;
       }
       if (x < y) {
           return -1;
       }
   }
   return 0;
   };
   console.log(compareVersion('0.1', '1.1'))
