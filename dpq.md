## 1D Dp

- Clmbing stairs
recusrive ; code ; 
 public int climbStairs(int n) {
        if(n==1 || n==0){
            return 1;
        }
        return climbStairs(n-1)+climbStairs(n-2);
    }

top down
public int climbStairs(int n) {
    int [] dp=new int [n+1];
    Arrays.fill(dp,-1);
    return memo(n,dp);
}
public int memo(int n, int[] dp){
    if(n==0 || n==1){
        return 1;
    }
    if(dp[n]!=-1){
        return dp[n];
    }
    return memo(n-1,dp)+memo(n-2,dp);
}

bottom up
public int climbStairs(int n) {
       int [] dp=new int [n+1];
       dp[0]=1;
       dp[1]=1;
        for(int i=2; i<=n; i++){
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }

space optmisied technique -> dp[i] depends on dp[i-1] and dp[i-2]	O(N) → O(1)	Three variables
public int climbStairs(int n) {    
        if (n == 0) return 1;
        if (n == 1) return 1;
        int a = 1, b = 1;
        for (int i = 2; i <= n; i++) {
            int temp = b;
            b = a + b;
            a = temp;
        }
        return b;
   }    


- min cost climbing stairs
recursive solution
 public int minCostClimbingStairs(int[] cost) {
        int n=cost.length;
        return Math.min(minCost(cost,n-1), minCost(cost,n-2));
    }
    public int minCost(int[] cost,int n) {
        if(n < 0){
            return 0;
        }
        if(n==0 || n==1){
            return cost[n];
        }
        return cost[n]+Math.min(minCost(cost,n-1), minCost(cost,n-2));
    }
top down dp
public int minCostClimbingStairs(int[] cost) {
        int n=cost.length;
        int [] dp=new int[n];
        return Math.min(memo(cost,dp,n-1), memo(cost,dp,n-2));
    }
    public int memo(int[] cost, int[]dp,int n) {
        if(n < 0){
            return 0;
        }
        if(n==0 || n==1){
            return cost[n];
        }
        dp[n]= cost[n]+Math.min(memo(cost,dp,n-1), memo(cost,dp,n-2));
        return dp[n];
    }

bottom  up
 public int minCostClimbingStairs(int[] cost) {
        int n=cost.length;
        int [] dp=new int[n+1];
        dp[0]=0;
        dp[1]=0;
        for(int i=2; i<=n; i++){
            dp[i] = Math.min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2]);
        }
        return dp[n];
    }
space optimised
 public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int first = cost[0];
        int second = cost[1];
        if(n<=2){
            return Math.min(first, second);
        }
        for(int i=2; i<n; i++){
            int curr = cost[i] + Math.min(first, second);
            first = second;
            second = curr;
        }
        return Math.min(first, second);
    }

House Robber
recursive solution
 public int rob(int[] nums) {
        int n=nums.length;
        return maxCost(nums,n-1);
    }
    public int maxCost(int[] cost,int n) {
        if(n < 0){
            return 0;
        }
        if(n==0){
            return cost[0];
        }
        return Math.max(maxCost(cost,n-1),cost[n]+maxCost(cost,n-2));
    }
top down dp
public int rob(int[] nums) {
        int n=nums.length;
        int [] dp=new int[n];
        return memo(nums,dp,n-1);
    }
    public int memo(int[] cost, int[]dp,int n) {
        if(n < 0){
            return 0;
        }
        if(n==0){
            return cost[0];
        }
        dp[n]= Math.max(memo(cost,dp,n-1),cost[n]+memo(cost,dp,n-2));
        return dp[n];
    }
}
bottom up dp
public int rob(int[] nums) {
       int n=nums.length;
       if(n==1){
        return nums[0];
       }
        int [] dp=new int[n];
        dp[0]=nums[0];
        dp[1]=Math.max(nums[0],nums[1]);
        for(int i=2; i<n; i++){
            dp[i] = Math.max(dp[i-1], dp[i-2] + nums[i]);
        }
        return dp[n-1];
    }
space optimised
 public int rob(int[] nums) {
        int n=nums.length;
        if (n == 1) return nums[0];
        if (n == 2) return Math.max(nums[0], nums[1]);

        int prev2 = nums[0];          
        int prev1 = Math.max(nums[0], nums[1]);

        for (int i = 2; i < n; i++) {
            int curr = Math.max(prev1, nums[i] + prev2);
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }

2 keys keyboard 
recusrive solution
copy paste curr
    public int minSteps(int n) {
        if (n == 1) return 0;
        return dfs(1, 0, n);
    }
    private int dfs(int curr, int clip, int n) {
        if (curr == n) return 0;
        if (curr > n) return 10_000_000;
        int result = Integer.MAX_VALUE;

        int copy = 1 + dfs(curr, curr, n);

        int paste = Integer.MAX_VALUE;
        if (clip > 0) {
            paste = 1 + dfs(curr + clip, clip, n);
        }
        return Math.min(copy, paste);
    }

top down 
 public int minSteps(int n) {
        if(n == 1){
            return 0;
        }
        int [][] dp=new int [n+1][n+1];
        return memo(1, 0, n,dp);
    }
    private int memo(int clip, int curr, int n ,int [][] dp) {
        if (curr == n) return 0;
        if (curr > n) return 10_000_000;
        int result = Integer.MAX_VALUE;
        if (dp[curr][clip] != 0){
            return dp[curr][clip];
        }
        int copy = 1 + memo(curr, curr, n,dp);

        int paste = Integer.MAX_VALUE;
        if (clip > 0) {
            paste = 1 + memo(curr + clip, clip, n,dp);
        }
        return dp[curr][clip]=Math.min(copy, paste);
    }

bottom up

 public int minSteps(int n) {
        if (n == 1) return 0;

        int[] dp = new int[n + 1];

        for (int i = 2; i <= n; i++) {
            dp[i] = i;  // worst case: copy once then paste (i-1) times

            for (int j = 2; j * j <= i; j++) {
                if (i % j == 0) {
                    dp[i] = Math.min(dp[i], dp[j] + i / j);
                    dp[i] = Math.min(dp[i], dp[i / j] + j);
                }
            }
        }

        return dp[n];
    }
