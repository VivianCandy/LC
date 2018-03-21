

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




## 16. 3Sum Closest

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

For example, given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

### solution 1：

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



## 18. 4Sum

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Note: The solution set must not contain duplicate quadruplets.

For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],

  [-2, -1, 1, 2],

  [-2,  0, 0, 2]

]

### solution 1:
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

### solution 2: 快！！！太高级看不懂

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

## 31. Next Permutation(排列）

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

### solution 1：
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


## 33. Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

### solution 1：

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

### solution 2：没看懂取余
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

## 34. Search for a Range

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,

Given [5, 7, 7, 8, 8, 10] and target value 8,

return [3, 4].

### solution 1：

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


## 39. Combination Sum（组合问题，有套路，加油背）

Given a set of candidate numbers (C) (without duplicates) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.
Note:

All numbers (including target) will be positive integers.

The solution set must not contain duplicate combinations.

For example, given candidate set [2, 3, 6, 7] and target 7, 
A solution set is: 

[
  [7],

  [2, 2, 3]

]

### solution 1：（dfs，递归）


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


## 48. Rotate Image

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

Given input matrix = 
[

  [1,2,3],

  [4,5,6],

  [7,8,9]

],

rotate the input matrix in-place such that it becomes:
[

  [7,4,1],

  [8,5,2],

  [9,6,3]

]

### solution 1:

	class Solution {
	public:
	    void rotate(vector<vector<int>>& matrix) 
	    {
	        for(int i=0;i<matrix.size();i++)
	        {
	            for(int j=i+1;j<matrix[0].size();j++)
	            {
	                swap(matrix[i][j], matrix[j][i]);
	            }
	        }
	        for(int k=0; k<matrix.size();k++)
	        {
	             reverse(matrix[k].begin(),matrix[k].end());
	        }
	       
	    }
	    
	};

## 54. Spiral Matrix

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,

Given the following matrix:

[

 [ 1, 2, 3 ],

 [ 4, 5, 6 ],

 [ 7, 8, 9 ]

]

You should return [1,2,3,6,9,8,7,4,5].

### solution 1:

	class Solution {
	public:
	    vector<int> spiralOrder(vector<vector<int>>& matrix) 
	    {
	        if(matrix.empty())
	            return {};
	        int m = matrix.size();
	        int n = matrix[0].size();
	        vector<int> spiral;
	        
	        
	        int col, row;
	        int u = 0; // upper most
	        int r = n-1; //right most
	        int d = m-1; // down most
	        int l = 0; //left most
	        
	        while(true)
	        {
	            for(col=l; col<=r; col++)
	            {
	                spiral.push_back(matrix[u][col]);
	            }
	            if(++u>d)
	                break;
	            for(row = u; row<=d; row++)
	            {
	                spiral.push_back(matrix[row][r]);
	            }
	            if(--r<l)
	                break;
	            for(col = r; col>=l; col--)
	            {
	                spiral.push_back(matrix[d][col]);
	            }
	            if(--d<u)
	                break;
	            for(row = d; row>=u; row--)
	            {
	                spiral.push_back(matrix[row][l]);
	            }
	            if(++l>r)
	                break;
	        }
	        return spiral;
	    }
	};


### solution 2: better
	
	class Solution {
	public:
	    vector<int> spiralOrder(vector<vector<int>>& matrix) {
	        vector<int> result;
	        if (matrix.size() == 0 || matrix[0].size() == 0) {
	            return result;
	        }
	        
	        int top = 0, bottom = matrix.size() - 1, left = 0, right = matrix[0].size() - 1;
	        while (left <= right && top <= bottom) {
	            for (int j = left; j <= right; j++) {
	                result.push_back(matrix[top][j]);
	            }
	            
	            top++;
	            if (top > bottom) break; // Important
	            for (int i = top; i <= bottom; i++) {
	                result.push_back(matrix[i][right]);
	            }
	            
	            right--;
	            if (left > right) break; // Important
	            for (int j = right; j >= left; j--) {
	                result.push_back(matrix[bottom][j]);
	            }
	            
	            bottom--;
	            if (top > bottom) break; // Important
	            for (int i = bottom; i >= top; i--) {
	                result.push_back(matrix[i][left]);
	            }
	            
	            left++;
	            if (left > right) break; // Important
	        }
	        
	        return result;
	    }
	};


## 55. Jump Game

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

### solution 1

    bool canJump(vector<int>& nums)
    {
        int size = nums.size();
        int largestPosition = 0;
        int i=0;
        for(largestPosition = 0; i <size && i <= largestPosition ; i++ )
        {
            if(i + nums[i] > largestPosition)
                largestPosition = i+ nums[i];
        }
        return i==size;
    }

## 56. Merge Intervals


Given a collection of intervals, merge all overlapping intervals.

For example,

Given [1,3],[2,6],[8,10],[15,18],

return [1,6],[8,10],[15,18].

### solution 1
sorting->

if the last element is smaller than the the start of Inters, then Inters should be push back

	/**
	 * Definition for an interval.
	 * struct Interval {
	 *     int start;
	 *     int end;
	 *     Interval() : start(0), end(0) {}
	 *     Interval(int s, int e) : start(s), end(e) {}
	 * };
	 */
	class Solution {
	public:
	    vector<Interval> merge(vector<Interval>& inters)
	    {
	        if(inters.size()<1)
	            return inters;
	        vector<Interval> res;
	        std::sort(inters.begin(), inters.end(), [](Interval a,Interval b){return a.start < b.start;});
			// Interval:type a:object
	        //sort(begin, end, com) ascending order
	 
	        res.push_back(inters[0]);
	        for(int i=1; i<inters.size();i++)
	        {
	            if (res.back().end < inters[i].start)
	            {
	                res.push_back(inters[i]);
	            }
	            else if(res.back().end < inters[i].end)
	            {
	                res.back().end = inters[i].end;
	            }
	
	        }
	        return res;
	    }
	};

## 59. Spiral Matrix II

iven an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,

Given n = 3,

You should return the following matrix:

[

 [ 1, 2, 3 ],

 [ 8, 9, 4 ],

 [ 7, 6, 5 ]

]

### solution 1

	class Solution {
	public:
	    vector<vector<int>> generateMatrix(int n) 
	    {
	        vector<vector<int>> Mat(n,vector<int>(n,0));
	        int top=0,right=n-1,bottom=n-1,left=0;
	        int count=1;
	        while(top<=bottom && left<=right)
	        {
	            for(int i=left; i<=right;i++)
	            {
	                Mat[top][i]=count++;
	            }
	            top++;
	            if(top>bottom)
	                break;
	            for(int j=top; j<=bottom;j++)
	            {
	                Mat[j][right]=count++;
	            }
	            right--;
	            if(left>right)
	                break;
	            for(int i=right; i>=left; i--)
	            {
	                Mat[bottom][i]=count++;
	            }
	            bottom--;
	            if(top>bottom)
	                break;
	            for(int j=bottom; j>=top;j--)//because top has already be increased
	            {
	                Mat[j][left]=count++;
	            }
	            left++;
	            if(left>right)
	                break;
	        }
	        return Mat;
	        
	        
	    }
	};


## 60. Permutation Sequence

The set [1,2,3,…,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

解释

123

132

213

231

312

321

可以发现最高位上每个数出现了两次，当第一位数确定后，第二位每个数出现了1次，当第二位数确定了，第三位只能出现一次。

若n=4，
1234

最高位每个数出现6次，当第一位数确定后，后面三位数每个数字都出现2次。当第二位数也确定了，后面的数字只出现一次。当第三位确定了，第四位数字也只能出现一次。

k从1开始算（没有第0行）

假设k=17，可以转换为数组下标16：

最高位取1,2,3,4,间的一个数，每个数字出现6次=3！。当k=16时，最高位的数字下标应该是16/6=2（6个数一变），所以最高位是3。

第二位数从1,2,4中间取3，k'=k%(3!)=4,每个数字出现2次=2！，所以第二位数的下标是4/2=2，所以是4.

第三位数是1,2中取一个，k''=k'%(2!)=0,剩下的数字出现一次，所以第三位数的下标是0/1=0.所以是1

第四位数是从2中取一个，k'''=k''%(1!)=0,剩下的数字出现0！=1次，所以第四个数的下标是0/1=0，也就是数字2.

规律：
a1 = k /(n-1)!

k1=k

a2 = k1 /(n-2)！

k2 = k1 %(n-2)!

...

an-1 = kn-2 /1!

kn-1 = kn-2 %1!


an = kn-1 /0!

kn = kn-1 % 0!


### solution 1
	class Solution {
	public:
	    string getPermutation(int n, int k) {
	        string res;
	        string num = "123456789";
	        vector<int> f(n, 1);
	        for (int i = 1; i < n; ++i) f[i] = f[i - 1] * i;
			\\f存的是阶乘的值
	        --k;//to get index
	        for (int i = n; i >= 1; --i) {
	            int j = k / f[i - 1];
	            k %= f[i - 1];
	            res.push_back(num[j]);
	            num.erase(j, 1);
				//delete index j(1 length) in string num
	        }
	        return res;
	    }
	};


### solution 2 i don't understand how it works, amazing!

	string getPermutation(int n, int k) {
	    int pTable[10] = {1};
	    for(int i = 1; i <= 9; i++){
	        pTable[i] = i * pTable[i - 1];
	    }
	    string result;
	    vector<char> numSet;
	    numSet.push_back('1');
	    numSet.push_back('2');
	    numSet.push_back('3');
	    numSet.push_back('4');
	    numSet.push_back('5');
	    numSet.push_back('6');
	    numSet.push_back('7');
	    numSet.push_back('8');
	    numSet.push_back('9');
	    while(n > 0){
	        int temp = (k - 1) / pTable[n - 1];
	        result += numSet[temp];
	        numSet.erase(numSet.begin() + temp);
	        k = k - temp * pTable[n - 1];
	        n--;
	    }
	    return result;
	}

## 62 Unique Paths

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

### solution 1
	int uniquePaths(int m, int n)
	{
		int N = m+n-2;//total steps we need
		int down = m-1;//number of steps we need to go down
		double res = 1;
		/*calculate the total possible path
		combination(N,down) = N! / (down!(N-down)!)
	    reduce the numerator and denominator and get
	 	C = ((N-down+1)*(N-down+2)*...*N) / down!
		number of loop (N-(N-down+1)+1)=down
		*/
		for(int i=1; i<=down; i++)//number of loop:down
		{
			res *= N-down+i / i!
		}
		return (int)res;
	}
### solution 2 easy to understand
	class Solution {
	public:
	    int uniquePaths(int m, int n) 
	    {
	        double path=1.0;
	        int step = m+n-2;
	        int down = m-1;
	        //Combination = step!/(down!(step-down)!)
	        for(int i=1; i<=down; i++)
	        {
	            path =path* (step-down+i) / i;
	        }
	        return (int)path;
	    }
	   
	};

### solution 3: this is slower and time complesity is o(n2). Anyway ,it is a new method.

if you want to know how many way to reach point[i][j], then it is the sum of the way to reach point[i-1][j]and point[i][j-1]

	class Solution {
	public:
	    int uniquePaths(int m, int n) 
	    {
	        vector<vector<int>> dp(m,vector<int>(n,1));
	        for(int i=1; i<m; i++)
	        {
	            for(int j=1; j<n; j++)
	            {
	                dp[i][j] = dp[i-1][j]+dp[i][j-1];//the number of way to go to point[i][j]
	            }
	        }
	            return dp[m-1][n-1];
	    }
	   
	};


## 63. Unique Paths II

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.

[

  [0,0,0],

  [0,1,0],

  [0,0,0]

]

The total number of unique paths is 2.
### solution1

	class Solution {
	public:
	    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) 
	    {
	        int m = obstacleGrid.size();
	        int n = obstacleGrid[0].size();
	        vector<vector<int>> dp(m+1,vector<int>(n+1,0));
	        dp[0][1]=1;
	        for(int i=1;i<=m;i++)
	        {
	            for(int j=1;j<=n;j++)
	            {
	                if(!obstacleGrid[i-1][j-1])//obstacleGrid[i-1][j-1]!=1
	                {
	                    dp[i][j]=dp[i-1][j]+dp[i][j-1];
	                }
	            }
	        }
	        return dp[m][n];
	    }
	};

## 64. Minimum Path Sum

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example 1:

[[1,3,1],

 [1,5,1],

 [4,2,1]]

Given the above grid map, return 7. Because the path 1→3→1→1→1 minimizes the sum.

### solution 1(don't understand)

	class Solution {
	public:
	    int minPathSum(vector<vector<int>>& grid) 
	    {
	        int m = grid.size();
	        int n = grid[0].size();
	        
	        vector<int> cur(m,grid[0][0]);
	        
	        for(int i=1;i<m;i++)
	        {
	            cur[i]=cur[i-1] + grid[i][0];
	        }
	        
	        for(int j=1;j<n;j++)
	        {
	            cur[0] += grid[0][j];//the sum of row
	            for(int i=1; i<m;i++)
	            {
	                cur[i]=min(cur[i-1],cur[i])+grid[i][j];
	            }
	        }
	        
	
	            return cur[m-1];
	    }
	};