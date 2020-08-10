```java
import java.util.Arrays;
class test {
	public static void main (String[] args) throws java.lang.Exception {
		int[] arr = new int[100];
		for (int i=0;i<arr.length;i++) {
		    arr[i] = (int) (Math.random() * 100);
		}
		int[] arr1 = arr;
		int[] arr2 = arr;
		System.out.println(Arrays.toString(arr));
        // 插入排序
		for (int i=1,j,current;i<arr.length;i++) {
		    current = arr[i];
		    for (j=i-1;j>=0 && arr[j]>current;j--) {
		        arr[j+1] = arr[j];
		    }
		    arr[j+1] = current;
		}
		System.out.println(Arrays.toString(arr));
		
		// 冒泡排序
		boolean hasChange = true;
		for (int i=0; i<arr1.length && hasChange; i++) {
		    hasChange = false;
		    for (int j=0; j<arr1.length-1-i;j++) {
		        if (arr[j] > arr[j+1]) {
		            hasChange = true;
		            int temp = arr[j];
		            arr[j] = arr[j+1];
		            arr[j+1] = temp;
		        }
		    }
		}
		System.out.println(Arrays.toString(arr1));
		
        // 选择排序
		for (int i=0,modifi;i<arr2.length-1;i++) {
		    modifi = i;
		    for (int j=i+1;j<arr2.length;j++) {
		        if (arr[j] < arr[modifi]) {
		            modifi = j;
		        }
		    }
		    int temp = arr[modifi];
		    arr[modifi] = arr[i];
		    arr[i] = temp;
		}
		System.out.println(Arrays.toString(arr2));
		
		int a = binarySearch(arr, 34);
		System.out.println(a);
		System.out.println(binarySearchRecursion(arr, 34, 0, arr.length - 1));
		
	}
	// 非递归二分法
	public static int binarySearch(int[] arr, int flag) {
	    int low = 0;
	    int hig = arr.length-1;
	    while (low <= hig) {
	        int middle = (low + hig) / 2;
	        if (arr[middle] > flag) {
	            hig = middle - 1;
	        } else if (arr[middle] < flag) {
	            low = middle + 1;
	        } else {
	            return middle;
	        }
	    }
	    return -1;
	}
	// 递归二分法
	public static int binarySearchRecursion(int[] arr, int flag, int low, int hig) {
	    if (low <= hig) {
    	    int middle = (low + hig) / 2;
    	    if (arr[middle] < flag) {
    	        return binarySearchRecursion(arr, flag, middle + 1, hig);
    	    } else if (arr[middle] > flag) {
    	        return binarySearchRecursion(arr, flag, low, middle - 1);
    	    } else if (arr[middle] == flag) {
    	        return middle;
    	    }
	    }
	    return -1;
	}
}
```

```python
# encoding: utf-8
import random
# 归并排序
def mergerSort(list):
    leng = len(list)
    if leng < 2:
        return list
    modifi = leng // 2
    left = list[0:modifi]
    right = list[modifi:]
    return merger(mergerSort(left), mergerSort(right))

def merger(left, right):
    result = []
    while len(left) and len(right):
        if left[0] <= right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    while len(left):
        result.append(left.pop(0))
    while len(right):
        result.append(right.pop(0))
    return result
		

if __name__ == "__main__":
    L = []
    for _ in range(0, 100):
        L.append(random.randint(1, 100))
    print(L)
    print('=====================================================================')
    print(mergerSort(L))
```

```java
// 螺旋矩阵
public static int[][] spiralMatrix(int n) {
    int[][] arr = new int[n][n];
    for (int s=0,e=n-1,m=1; s<=e; s++, e--) {
        for (int j=s;j<=e;j++) arr[s][j] = m++;
        for (int j=s+1;j<=e;j++) arr[j][e] = m++;
        for (int j=e-1;j>=s;j--) arr[e][j] = m++;
        for (int j=e-1;j>s;j--) arr[j][s] = m++;
    }
    return arr;
}
```

