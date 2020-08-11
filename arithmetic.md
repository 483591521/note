```java
// 统计英文大写字符串中英文字符的个数
// 统计数字字符串中数字字符的个数
String str = "26982609981787347818289671823333331234";
int[] count = new int[10];
for (int i=0;i<str.length();i++) {
    char c = str.charAt(i);
    count[c-'0']++;
}
char ch = '0';
for (int i: count) {
    System.out.println((ch++) + ": " + i);
}
```

```java

/**
* 打乱数组
* @param args
*/
public static void main(String[] args) {
    int[] arr = {3, 5, 3, 7, 8, 1, 9};
    Random random = new Random();
    for (int i=arr.length-1;i>0;i--) {
        int j = random.nextInt(i);
        int t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
    }
    System.out.println(Arrays.toString(arr));
}
```

```java

// 进制转换
public static int parseInt(String str, int base) {
    int sum = 0;
    int weight = 1;
    for (int i=str.length()-1;i>=0;i--) {
        int n = str.charAt(i) - '0';
        if (n < 0 || n >= base) {
            throw new NumberFormatException("超范围");
        }
        sum += n * weight;
        weight *= base;
    }
    return sum;
}
```

```java

public static void main(String[] args) {
    int[] arr = new int[5];
    Random random = new Random();
    for (int j=0;j<100;j++) {
        int num = random.nextInt(1000);
        int index = Arrays.binarySearch(arr, num);
        if (index == -1 || index == 0) continue;
        if (index < 0) index = -(index+1);
        for (int i=1;i<index;i++) {
            arr[i-1] = arr[i];
        }
        arr[index-1] = num;
        System.out.println(Arrays.toString(arr));
    }
    System.out.println(Arrays.toString(arr));
}
```

