ANY PROBLEM?

# 2.array(medium)

## 11. Container With Most Water
Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

### solution 1:

'''C
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
'''


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