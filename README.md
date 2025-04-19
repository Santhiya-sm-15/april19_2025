# april19_2025
The problems that I solved today

1.Given a 0-indexed integer array nums of size n and two integers lower and upper, return the number of fair pairs.

A pair (i, j) is fair if:

0 <= i < j < n, and
lower <= nums[i] + nums[j] <= upper

Code:
class Solution {
    public int ubound(int i,int j,int[] nums,int lower,int upper,int ind)
    {
        int ans=-1;
        while(i<=j)
        {
            int mid=(i+j)/2;
            int x=nums[ind]+nums[mid];
            if(x>=lower && x<=upper)
            {
                ans=mid;
                i=mid+1;
            }
            else if(x>upper)
                j=mid-1;
            else
                i=mid+1;
        }
        return ans;
    }
    public int lbound(int i,int j,int[] nums,int lower,int upper,int ind)
    {
        int ans=-1;
        while(i<=j)
        {
            int mid=(i+j)/2;
            int x=nums[ind]+nums[mid];
            if(x>=lower && x<=upper)
            {
                ans=mid;
                j=mid-1;
            }
            else if(x<lower)
                i=mid+1;
            else
                j=mid-1;
        }
        return ans;
    }
    public long countFairPairs(int[] nums, int lower, int upper) {
        Arrays.sort(nums);
        int n=nums.length;
        long cnt=0;
        for(int i=0;i<n;i++)
        {
            int x=lbound(i+1,n-1,nums,lower,upper,i);
            int y=ubound(i+1,n-1,nums,lower,upper,i);
            if(x!=-1 && y!=-1)
                cnt+=(y-x+1);
        }
        return cnt;
    }
}
