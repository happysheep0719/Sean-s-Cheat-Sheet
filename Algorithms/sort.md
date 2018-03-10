# Quick sort

```
public class Solution {
    public void helper(int[] array, int ixs, int ixe){
        // recursion base case
        if (ixs >= ixe){
            return;
        }

        // first partition array into two parts
        // AAAAXBBBBB  X needs to be in the middle, or the program is wrong.
        int l = ixs + 1, r = ixe, threshold = array[ixs]; // IMPORTANT
        while (l <= r){
            if (array[l] < threshold) {
                l++;
            } else {
                // swap the i-th number with the number in the r pivot
                int temp = array[r];
                array[r] = array[l];
                array[l] = temp;

                r--;
            }

        }
        // swap the first number with the middle number.
        // l in [ixs+1, ixe+1], r in [ixs, ixe];
        // A[l] > threshold, A[r] < threshold.
        // A[ixs] should be less than threshold
        // so, we should swap A[ixs] and A[r].
        int temp = array[ixs];
        array[ixs] = array[r];
        array[r] = temp;

        // then partition the two parts of the array separately;
        helper(array, ixs, r-1); // IMPORTANT!!!  l-1 == r, ixe = l-1 or r
        helper(array, r+1, ixe); // IMPORTANT!!!  l-1 == r, ixs = l or r+1

        return;
    }

    public int[] quickSort(int[] array) {
        helper(array, 0, array.length-1);

        return array;
    }

    public static void main(String[] args) {
        Solution s = new Solution();
        for (int i: s.quickSort(new int[]{1,2,3})) {
            System.out.println(i);
        }
        for (int i: s.quickSort(new int[]{4,2,1,6,3,5})) {
            System.out.println(i);
        }
    }
}
```