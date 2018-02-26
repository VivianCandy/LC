
[26. Remove Duplicates from Sorted Array](#26-Remove-Duplicates-from-Sorted-Array)
# 1.Array(easy)
## 1. Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
Example:
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

### solution 1.

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        vector<int> result;
        int i,j;
        int len = nums.size();
        for(i=0;i<len;i++)
        {
            for(j=i+1;j<len;j++)
            {
                if(nums[i]+nums[j]==target)
                {
                    result.push_back(i);
                    result.push_back(j); 
                    return result;
                }
    
            }  
        }
    }
};
### soluton 2.
 class Solution {
public:
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> imap;
    
    for (int i = 0;; ++i) {
        auto it = imap.find(target - nums[i]);
        
        if (it != imap.end()) 
            return vector<int> {it->second, i};
            
        imap[nums[i]] = i;
    }
}
};


## 26. Remove Duplicates from Sorted Array
Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.

### solution 1:
class Solution {
public:
    int removeDuplicates(vector<int>& nums) 
    {
        int i;
        int j;
        for(i=0;i<nums.size();i++)
        {
            for(j=i+1;j<nums.size();j++)
            {
                if (nums[i]==nums[j])
                {
                    nums.erase(nums.begin() + j);
                    j-=1;
                }
            }
        }
        return nums.size();
        
    }
};

### solution 2:
class Solution {
public:
    int removeDuplicates(vector<int>& nums) 
    {
        int i;
        int j;
        for(i=0;i<nums.size();i++)
        {
            for(j=i+1;j<nums.size();j++)
            {
                if (nums[i]==nums[j])
                {
                    nums.erase(nums.begin() + j);
                    j-=1;
                }
            }
        }
        return nums.size();
        
    }
};

## 27. Remove Element
Given an array and a value, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:

Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.
### solution 1:
class Solution {
public:
    int removeElement(vector<int>& nums, int val) 
    {
        int count=0;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]!=val)
            {
                nums[count++]=nums[i];
            }
        }
        return count;
    }
};
### solution 2:
class Solution {
public:
    int removeElement(vector<int>& nums, int val) 
    {
         int sz = nums.size();
        if( sz == 0 ) return 0;
        while( nums[sz-1] == val && sz >0 ) sz--;
        for( int i=0; i<sz; ++i)
        {
            if( nums[i] == val ) 
            {
                nums[i] = nums[sz-1];
                sz--;
                while( nums[sz-1] == val ) sz--;
            }
        }
        nums.resize(sz);
        return sz;
    }
};
## 35. Search Insert Position
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:

Input: [1,3,5,6], 5
Output: 2
Example 2:

Input: [1,3,5,6], 2
Output: 1
Example 3:

Input: [1,3,5,6], 7
Output: 4

### solution 1:
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) 
    {
        int i=0;
        int len = nums.size()-1;
        while(i<=len)
        {
            if(nums[i] == target)
                return i;
            else if(nums[i]>target)
                return i;
            else if(nums[i]<target)
                i++;
        }
        return i;
    }
};

### solution 2:
class Solution {
public:
    int searchInsert(vector<int>& nums, int target)
    {
        int l = 0, r = nums.size()-1;
        if(target > nums.back()) return nums.size();
        while(l < r)
        {
            int mid = l + (r-l)/2;
            if(nums[mid] == target) return mid;
            else if(nums[mid] < target ) l = mid + 1;
            else r = mid;
        }
        return r;
    }

};
## 53. Maximum Subarray
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

click to show more practice.

More practice:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

### solution 1：（不能处理大量数据，bad）
class Solution {
public:
    int maxSubArray(vector<int>& nums) 
    {
        int i,j;
        int sum;
        int largest;
        int listLarge;
        vector<int> listSum;
        vector<int> vectLargest;
        while(nums.size()==1)
            return nums.front();
        for(i=0;i<nums.size();i++)
        {
            sum=nums[i];
            listSum.push_back(sum);
            for(j=i+1;j<nums.size();j++)
            {
                sum=sum+nums[j];
                listSum.push_back(sum);
            }
             listLarge=*max_element(begin(listSum),end(listSum));
             vector<int>().swap(listSum); 
             vectLargest.push_back(listLarge);
             
        }
        largest=*max_element(begin(vectLargest),end(vectLargest));
        vector<int>().swap(vectLargest); 
        return largest;
    }
};

### solution 2:
class Solution {
public:
    int maxSubArray(vector<int>& nums) 
    {
        int i;
        int sum=0;
        int max=nums[0];
        for(i=0;i<nums.size();i++)
        {
            sum=sum+nums[i];
            max=(max<sum? sum:max);
            sum=(sum<0? 0:sum);     
        }
        return max;
    }
};
### solution 3: best
#include<math>
class Solution {
public:
    int maxSubArray(vector<int>& nums) 
    {
        int n=nums.size();
 	    int max = nums[0];
 	    int sum[n];
        sum[0]=nums[0];
 	    for(int i = 1; i < nums.size(); ++i)
        {
            sum[i]=nums[i]+(sum[i-1]>0? sum[i-1]:0);
//if sum[i-1]<0, then it will decrease the maximal value, so sum[i-1] will be discarded.
            max=(sum[i]>max? sum[i]:max);
 	    }
 	    return max;
    }
};


## 69.plus one
把给定的一个数加一，其中数的储存形式是[]
例如：
[1,9]+1=[2,0]
[9,9]+1=[1,0,0]
### solution 1:
class Solution 
{
public:
    vector<int> plusOne(vector<int>& digits) 
    {

        for(int i= digits.size()-1; i>=0;i--)
        {
            if(digits[i] == 9)
            {
                digits[i] = 0;
            }
            else
            {
                digits[i]++;
                return digits;
            }
        }
        digits[0] = 1;
        digits.push_back(0);
        return digits;
    }
};


## 88.  Merge Sorted Array

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.
融合两个排序好的数组到第一个数组去，将1的前m个和2的前n个合并到1里排序。假设第一个size大于等于m+n

### solution 1：

class Solution {
public:
    vector<int> merge(vector<int>& nums1, int m, vector<int>& nums2, int n) 
    {
        //int result[m+n];
        //vector<int> result;
        int i=m-1;
        int j=n-1;
        int k=m+n-1;
        while(k>=0)
        {
            if(i>=0 && j>=0)
            {
                if(nums1[i]>=nums2[j])
                {
                    nums1[k--]=nums1[i--];
                }
                else
                {
                    nums1[k--]=nums2[j--];  
                }

            }
            else if(j<0)
            {
                nums1[k--]=nums1[i--];
            }
            else if(i<0)
            {
                nums1[k--]=nums2[j--];
            }

        }
        return nums1;
    }
};

### solution 2：

class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) 
    {
        while( n > 0 )
            nums1[ n + m - 1] =( m == 0 || nums2[n - 1] > nums1[m - 1]) ?nums2[--n] : nums1[--m];
    }
};

### solution 3：（python）

class Solution(object):
    def merge(self, nums1, m, nums2, n):
        nums1[:] = nums1[:m] + nums2[:n]
        nums1.sort()




## 118. Pascal's Triangle

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return

[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]

### solution 1： focus on the usage of vector<vector<int>> size
class Solution {
public:
    vector<vector<int> > generate(int numRows) 
    {
        vector<vector<int> > listArray(numRows);

        if(numRows>0)
        {
                for(int i=0;i<numRows;i++)
                {
                    listArray[i].resize(i+1);
                    listArray[i][0]=1;
                    listArray[i][i]=1;
                    
                    for(int j=1;j<i;j++)
                   {
                       listArray[i][j]=listArray[i-1][j-1]+listArray[i-1][j];
                   }
               }
        }
        return listArray;
    }
};

### solution 2：

class Solution {
public:
    vector<vector<int>> generate(int numRows) 
    {
        vector<vector<int>> res;
        for(auto i=0;i<numRows;++i)
        {
            res.push_back(vector<int>(i+1,1));
            for(auto j=1; j<i; ++j) res[i][j] = res[i-1][j-1] + res[i-1][j];
        }
        return res;
    }
};

### 119. Pascal's Triangle II
Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return [1,3,3,1].

Note:
Could you optimize your algorithm to use only O(k) extra space?


### solution 1：stupid solution ,we don’t use vector<vector<int>> list

class Solution {
public:
    vector<int> getRow(int rowIndex)//+1line
    {
        vector<vector<int> > list;
        vector<int> result(rowIndex+1,1);
        //if i didn't set the size, i could not use reuslt[i]
       
        for(int i=0;i<=rowIndex;++i)
        {
            list.push_back(vector<int>(i+1,1));
        }
        for(int i=0;i<=rowIndex;i++)
        {
            result[0]=1;
            for(int j=1;j<i;j++)
            {
                list[i][j]=list[i-1][j-1]+list[i-1][j];
                if(i==(rowIndex))
                {
                    result[j]=list[i][j];
                }
            }
        }
        return result;
    }
};

### solution 2：
class Solution {
public:
    vector<int> getRow(int rowIndex)//+1line
    {
        vector<int> result(rowIndex+1,0);
        //if i didn't set the size, i could not use reuslt[i]
        for(int i=0;i<=rowIndex;i++)
        {
            result[0]=1;
            for(int j=i;j>0;j--)
            {
                result[j]=result[j-1]+result[j];
            }
        }
        return result;
    }
};

### solution 3: 第i行的第k个数是C_i^k=i!/(k!*(i-k)!

不明白这个方法
Note that this solution is math derived from number of Combinations.
Each line of Pascal’s Triangle is a full set of Combination number based on k .
comb(k,p) = k! /( p! *(k-p)!) = comb(k,k-p)
if p < k-p
comb(k,p) = comb(k,p-1) * (k-p+1) / p
Because :
comb(k,p) = [ k * (k-1) * (k-2) *… (k-p+1)] / [1 * 2 * 3 *…§]

vector<int> getRow(int rowIndex) {
    vector<int> ans(rowIndex+1,1);
    int small = rowIndex/2;
    long comb = 1;
    int j = 1;
    for (int i=rowIndex; i>=small; i--){
        comb *= i;
        comb /= j;
        j ++;
        ans[i-1] = (int)comb;
        ans[j-1] = (int)comb;
    }
    return ans;
}


## 121. Best Time to Buy and Sell Stock

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Example 1:
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
Example 2:
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.

### solution 1：

class Solution {
public:
    int maxProfit(vector<int>& prices) 
    {

        int diff=0;
        int max=0;
        int size=prices.size();
        if (prices.size()==0)
            return 0;
        for(int i=size-1;i>0;i--)
        {
            if(prices[i]!=0)
            {
                for(int j=i-1;j>=0;j--)
                {
                    diff=prices[i]-prices[j];
                    if(diff>max)
                    {
                        max=diff;
                    }  
                }
            }
        }
        return max;
    }
};

### Solution 2：

class Solution {
public:
    int maxProfit(vector<int>& prices) 
    {
        int maxDiff=0;
        int minVal=INT_MAX;
        int size=prices.size();
        
  
        for(int i=0;i<size;i++)
        {
            if(prices[i]<minVal)
            {
                minVal=prices[i];
            }
            else if(prices[i]-minVal>maxDiff)
            {
                maxDiff=prices[i]-minVal;
    
            }
        }
        return maxDiff;
    }
};



## 122. Best Time to Buy and Sell Stock II

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

input: [3,5,3,4,6,8,4,5,6]

output: 9

2+1+2+2+1+1=9

### solution 1：

class Solution {
public:
    int maxProfit(vector<int>& prices) 
    {
        int sum=0;

        for(int i=1;i<prices.size();i++)
        {
            if(prices[i]-prices[i-1]>0)
                sum+=prices[i]-prices[i-1];
        }
        return sum;
    }
};

# 2.array(medium)

## 11. Container With Most Water
Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

### solution 1:

class Solution {
public:
    int maxArea(vector<int>& height) 
    {
        int water;
        int h;
        int j;
        int i=0;
        int size=height.size();
        if(size<=1)
            return 0;
        h=min(height[0],height[size-1]);
        j=size-1;
        water = h*(size-1);
        while(i<j)
        {
            h = min(height[i], height[j]);
            water = max(h*(j-i), water);
            while(height[i]<=h && i<j)
                i++;
            while(height[j]<=h && i<j)
                j--;
        }
        return water;
    }
};


## 15. 3Sum(不太看得懂答案)

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.

For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[

  [-1, 0, 1],

  [-1, -1, 2]

]

### solution 1:

class Solution {

public:

vector<vector<int> > threeSum(vector<int> &num) {
    
    vector<vector<int> > res;

    std::sort(num.begin(), num.end());

    for (int i = 0; i < num.size(); i++) {
        
        int target = -num[i];
        int front = i + 1;
        int back = num.size() - 1;

        while (front < back) {

            int sum = num[front] + num[back];
            
            // Finding answer which start from number num[i]
            if (sum < target)
                front++;

            else if (sum > target)
                back--;

            else {
                vector<int> triplet(3, 0);
                triplet[0] = num[i];
                triplet[1] = num[front];
                triplet[2] = num[back];
                res.push_back(triplet);
                
                // Processing duplicates of Number 2
                // Rolling the front pointer to the next different number forwards
                while (front < back && num[front] == triplet[1]) front++;

                // Processing duplicates of Number 3
                // Rolling the back pointer to the next different number backwards
                while (front < back && num[back] == triplet[2]) back--;
            }
            
        }

        // Processing duplicates of Number 1
        while (i + 1 < num.size() && num[i + 1] == num[i]) 
            i++;

    }
    
    return res;
    
}

};

### solution 2: better

class Solution {
public:
vector<vector<int> > threeSum(vector<int> &num) 
{
    
    vector<vector<int> > res;
    if(num.size()<=2)
        return res;
    std::sort(num.begin(), num.end());
    

    for (int i = 0; i < num.size()-2; i++)
    {
        
        int front = i + 1;
        int back = num.size() - 1;

        while (front < back)
        {

            
            // Finding answer which start from number num[i]
            if (num[i]+num[front]+num[back]< 0)
                front++;

            else if (num[i]+num[front]+num[back]> 0)
                back--;

            else 
            {
                res.push_back({num[i], num[front], num[back]});
                
                // Processing duplicates of Number 2
                // Rolling the front pointer to the next different number forwards
                while (front < back && num[front] == num[front+1]) front++;

                // Processing duplicates of Number 3
                // Rolling the back pointer to the next different number backwards
                while (front < back && num[back] == num[back-1]) back--;
                front++;
                back--;
                
            }
            
        }

        // Processing duplicates of Number 1
        while (i + 2 < num.size() && num[i + 1] == num[i]) 
            i++;
    } 
    return res; 
}
};




16. 3Sum Closest
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

    For example, given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

solution 1：
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target)
    {
        int sum;
        int result;
        int size = nums.size();
        
        int front;
        int back;
        if(nums.size()<3)
            return 0;
        sort(nums.begin(), nums.end());
        result=nums[0]+nums[1]+nums[size-1];
        for(int i=0;i<size-2;i++)
        {
             front=i+1;
             back=size-1;
            while(front<back)
            {
                sum = nums[i]+nums[front]+nums[back];
                if(sum<target)
                { 
                    front++;
                   
                }
                else if(sum>target)
                { 
                    back--;
                }
                else
                {
                    return target;
                }
                if(abs(target-sum)<abs(target-result))
                {
                        result=sum;
                }
            }
        }
            
        return result;
    }
};



18. 4Sum
Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Note: The solution set must not contain duplicate quadruplets.

For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]

solution 1:
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) 
    {
        vector<vector<int>> list;
        int size=nums.size();
        int j, front, back;
        if(size<4)
        {
            return list;
        }
        sort(nums.begin(),nums.end());
        for(int i=0;i<size-3;i++)
        {
            for(j=i+1;j<size-2;j++)
            {
                front=j+1;
                back=size-1;
                while(front<back)
                {
                    if(nums[i]+nums[j]+nums[front]+nums[back]>target)
                    {
                        back--;
                    }
                    else if(nums[i]+nums[j]+nums[front]+nums[back]<target)
                    {
                        front++;
                    }
                    else if(nums[i]+nums[j]+nums[front]+nums[back]==target)
                    {
                        list.push_back({nums[i], nums[j], nums[front], nums[back]});
                        
                        while( front<back && nums[front]==nums[front+1])//when equal to target then test num[front] and nums[front+1]
                        {
                            front++;
                        }
                        while(front<back && nums[back]==nums[back-1])
                        {
                            back--;
                        }
                        front++;
                        back--;
                    }
                
                }
                while(nums[j]==nums[j+1] && j<size-2)
                {
                    j++;
                }
            }
            while(nums[i]==nums[i+1] && i<size-3)
            {
                i++;
            }
        }
        
        return list;
    }
};

solution 2: 快！！！太高级看不懂
class Solution {
    void threeSum(vector<int>& nums, int target, int left, vector<vector<int>> &results) 
    {
        for (int i = left; i < nums.size() - 2; ++i) 
        {
            if ((i != left && nums[i] == nums[i - 1]) || nums[i] + nums.back() * 2 < target || nums[i] * 3 > target) 
            {
                continue;
            }
            
            int l = i + 1, r = nums.size() - 1;
            while (l < r) 
            {
                int sum = nums[i] + nums[l] + nums[r];
                if (sum == target) 
                {
                    results.push_back({nums[left - 1], nums[i], nums[l], nums[r]});
                    while (l < r && nums[l] == nums[l +1]) 
                    {
                        ++l;
                    }
                
                    while ( l < r && nums[r] == nums[r - 1]) 
                    {
                        --r;
                    }
                    ++l;
                    --r;
                }
                else if (sum < target)
                {
                    ++l;
                } else 
                {
                    --r;
                }
               /* 
                while (l != i + 1 && l < r && nums[l] == nums[l - 1]) 
                {
                    ++l;
                }
                
                while (r != nums.size() - 1 && l < r && nums[r] == nums[r + 1]) 
                {
                    --r;
                }
                */
            }
        }
    }
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) 
    {
        vector<vector<int>> results;
        
        if (nums.size() < 4) return results;
        
        sort(nums.begin(), nums.end());
        
        for (int i = 0; i < nums.size() - 3; ++i) 
        {
            if ((i != 0 && nums[i] == nums[i - 1]) || nums[i] + nums.back() * 3 < target || nums[i] * 4 > target)
            {
                continue;
            }
            threeSum(nums, target - nums[i], i + 1, results);
        }
        
        return results;
    }
};

31. Next Permutation
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1

原来是数学中的排列组合，比如“1，2，3”的全排列，依次是：

1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
所以题目的意思是，从上面的某一行重排到期下一行，如果已经是最后一行了，则重排成第一行。

但是也不能根据给出的数组中的数字列出所有排列，因为要求不能占用额外的空间。


解题方法：从最后往前找第一个递减的数，记住这个递减的数a和位置p，再从最后往前找第一个a大的数b，再交换a，b的值，再从p+1到最后一个位置重新排序（上升方式）
若整个数组是递减的，则将整个数组倒叙排，
若没有找到b，则也是p+1开始重新排序。

solution 1：
class Solution {
public:
    void nextPermutation(vector<int>& nums) 
    {
        int len = nums.size(), flag = 1, index = len - 1;
        for (int i = len - 1; i>0; i--)
        {
            if (nums[i] <= nums[i - 1]) index--;
            else
            {
                for (int j = len - 1; j >= index; j--)
                {
                    if (nums[j]>nums[i - 1])
                    {
                        swap(nums[i - 1], nums[j]);
                        break;
                    }
                }
                sort(nums.begin() + i , nums.end());
                flag = 0;
                break;
            }
        }
        if (len&&flag) sort(nums.begin(), nums.end());
    }
};


33. Search in Rotated Sorted Array
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
You are given a target value to search. If found in the array return its index, otherwise return -1.
You may assume no duplicate exists in the array.
solution 1：
class Solution {
public:
    int search(vector<int>& nums, int target)
    {
        int nPosition;
        if(nums.size()<1)
            return -1;
        vector <int>::iterator iElement = find(nums.begin(),  
                               nums.end(),target);  
         if( iElement != nums.end() )  
         {  
             nPosition = distance(nums.begin(),iElement);  
             return nPosition;  
        }
        else
        {
            return -1;
        }
    }
};

solution 2：没看懂取余
class Solution {
public:
    int search(vector<int>& nums, int target)
    {
        int n=nums.size();
         int lo=0,hi=n-1;
        // find the index of the smallest value using binary search.
        while(lo<hi){
            int mid=(lo+hi)/2;
            if(nums[mid]>nums[hi]) lo=mid+1;
            else hi=mid;
        }
        // lo==hi is the index of the smallest value and also the number of places rotated.
        int rot=lo;
        lo=0;hi=n-1;
        // The usual binary search and accounting for rotation.
        while(lo<=hi){
            int mid=(lo+hi)/2;
            int realmid=(mid+rot)%n;
            if(nums[realmid]==target)return realmid;
            if(nums[realmid]<target)lo=mid+1;
            else hi=mid-1;
        }
        return -1;
    
    }
};
solution 3：没看懂异或
class Solution {
public:
    int search(vector<int>& nums, int target)
    {
    int lo = 0, hi = int(nums.size()) - 1;
    while (lo < hi) {
        int mid = (lo + hi) / 2;
        if ((nums[0] > target) ^ (nums[0] > nums[mid]) ^ (target > nums[mid]))
            lo = mid + 1;
        else
            hi = mid;
    }
    return lo == hi && nums[lo] == target ? lo : -1;
    
    }
};

34. Search for a Range
Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
solution 1：
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target)
    {
        int size = nums.size();
        int front=0;
        int back= size-1;
        int mid;
        int min;
        int max;
        vector<int> result;
        
        while(front<=back)
        {
            mid = (front+back)>>1;
            if(target>nums[mid])
            {
                front = mid+1;
            }
            else if(target<nums[mid])
            {
                back = mid-1;
            }
            else
            {   
                max=mid;
                min=mid;

                while(nums[max+1]==target && max<size-1)
                {
                    max++;
                    
                }
                while(nums[min-1]==target && min>0)
                {
            
                    min--;
                    
                }
                result.push_back(min);
                result.push_back(max);
                return result;
                //return vector<int> {min, max};
            }
        }
        result.push_back(-1);
        result.push_back(-1);
        return result;
        //return vector<int> {-1,-1};
    }
};


39. Combination Sum（组合问题，有套路，加油背）
Given a set of candidate numbers (C) (without duplicates) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.
The same repeated number may be chosen from C unlimited number of times.
Note:
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set [2, 3, 6, 7] and target 7, 
A solution set is: 
[
  [7],
  [2, 2, 3]
]

solution 1：（dfs，递归）


class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> ans;
        vector<int> cur;
        std::sort(candidates.begin(), candidates.end());
        dfs(candidates, target, 0, cur, ans);
        return ans;
    }
private:
    void dfs(vector<int>& candidates, int target, int s, vector<int>& cur, vector<vector<int>>& ans) {
        if (target == 0) {
            ans.push_back(cur);
            return;
        }
        
        for (int i = s; i < candidates.size(); ++i) {
            if (candidates[i] > target) break;
            cur.push_back(candidates[i]);
            dfs(candidates, target - candidates[i], i, cur, ans);
            cur.pop_back();
        }
    }
};
