#### Lintcode：183. Wood Cut
##### Difficulty: Hard
```java
public class Solution {
    /*
     * @param L: Given n pieces of wood with length L[i]
     * @param k: An integer
     * @return: The maximum length of the small pieces
     */
    public int woodCut(int[] L, int k) {
        // write your code here
        if (L == null || L.length == 0){
            return 0;
        }
        int most = L[0];
        for (int i = 1;i < L.length;i++){
            if (L[i] > most){
                most = L[i];
            }
        }
        int i = 0;
        int j = most;
        int mid;
        while (i + 1 < j){
            mid = i + (j - i) / 2;
            if (isMatch(L,mid,k)){
                i = mid;
            }else{
                j = mid;
            }
        }
        if (isMatch(L,j,k)){
            return j;
        }else{
            return i;
        }
    }
    public boolean isMatch(int[] L, int x, int k){
        int sum = 0;
        for (int i = 0;i < L.length;i++){
            sum += L[i] / x;
        }
        if (sum >= k){
            return true;
        }else{
            return false;
        }
    }
}
```

