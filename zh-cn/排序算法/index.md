# 排序算法


<!--more-->

常用排序算法如下

```java
import java.util.Arrays;
import java.util.Comparator;
//约定
abstract class Sort<T extends Comparable<T>> {
    public abstract void sort(T[] nums);

    protected boolean less(T v, T w) {
        return v.compareTo(w) < 0;
    }

    protected void swap(T[] a, int i, int j) {
        T t = a[i];
        a[i] = a[j];
        a[j] = t;
    }
}
//开始实现不同类型的排序算法

//选择排序
class  SelectionSort<T extends  Comparable<T>> extends Sort<T>{
    @Override
    public void sort(T[] nums) {
        int n = nums.length;
        for (int i = 0;i<n-1;i++){
            int min = i;
            for (int j = i+1;j<n;j++){
                if (less(nums[j],nums[min])){
                    min = j;
                }
            }
            swap(nums,i,min);
        }
    }
}

//冒泡排序
class BubbleSort<T extends Comparable<T>> extends Sort<T> {
    @Override
    public void sort(T[] nums) {
        int n = nums.length;
        for (int i = 0 ;i < n-1;i++){
            for (int j = 0;j<n-1-i;j++){
                if(less(nums[j+1],nums[j])){
                    swap(nums,j,j+1);
                }
            }
        }
    }
}

//插入排序
class InsetionSort<T extends  Comparable<T>> extends Sort<T>{
    @Override
    public void sort(T[] nums) {
        int n = nums.length;
        for (int i = 1  ; i < n ; i ++){
            for ( int j = i ; j >0 && less(nums[j],nums[j-1]);j--){
                swap(nums,j,j-1);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Integer[] arrayToSort = {64, 25, 12, 22, 11};
        SelectionSort<Integer> selectionSort = new SelectionSort<>();
        BubbleSort<Integer> bubbleSort = new BubbleSort<>();
        InsetionSort<Integer> integerInsetionSort = new InsetionSort<>();
//        bubbleSort.sort(arrayToSort);
//        selectionSort.sort(arrayToSort);
        integerInsetionSort.sort(arrayToSort);
        System.out.println(Arrays.toString(arrayToSort));

    }


}
```

