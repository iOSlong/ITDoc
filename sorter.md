-# //
//  sorter.c
//  arithmetic
//
//  Created by xw.long on 2019/6/23.
//  Copyright © 2019 fmylove. All rights reserved.
//

-#include "sorter.h"


```
void description(int a[], int len) {
    printf("\n");
    int i = 0;
    while (i < len) {
        printf("%d,",a[i]);
        i ++;
    }
    printf("\n");
}
```


//1.直接插入排序

```
void straightInsertSort(int a[], int len) {
    int i, j;
-#if SortTypeOne
    for (i = 1; i < len ; i ++) {
        int des = a[i];
        j = i - 1;
        while (a[j] > des && j >= 0) {
            a[j + 1] = a[j];
            j --;
        }
        a[j+1] = des;
    }
-#else
    for (i = 1; i < len; i ++) {
        for (j = i - 1; j >= 0; j --) {
            if (a[j] > a[i]) {
                a[j + 1] = a[j];
                a[j] = a[i];
            }
        }
    }
-#endif
}
```

//2.二分插入排序

```
void binaryInsertSort(int a[], int len) {
    int i,j,mid,low,top,tmp;
    for (i = 1; i < len ; i ++) {
        tmp = a[i];
        low = 0;top = i - 1;

        while (low <= top) {
            mid = (top + low) / 2;
            if (a[mid] > tmp) {
                top = mid - 1;
            }else if (a[mid] < tmp) {
                low = mid + 1;
            }
        }

        j = i;
        while (j >= top + 1) {
            a[j] = a[j - 1];
            j --;
        }
        a[top + 1] = tmp; //top+1 就是要插入数据的位置。
    }
}
```

//3.冒泡排序
void bubbleSort(int a[], int len) {
    int i,j,tem;
    for (i = 0; i < len; i ++) {
        for (j = len - 1; j > i; j --) {
            if (a[j] > a[j - 1]) { //注意冒泡排序是从后往前，将两两判断中最小的数据不断前移。所以这里全是j，并且j--。
                tem = a[j];
                a[j] = a[j-1];
                a[j-1] = tem;
            }
        }
    }
}


//4.快速排序

```
void quickSort(int a[], int start, int end) {
    if (start >= end) { return ;}
    int i,j,tmp,loc = start;
    for (i = start + 1; i <= end; i ++) {
        if (a[loc] > a[i]) {
            tmp = a[i];
            for (j = i; j > start; j --) {
                a[j] = a[j-1];
            }
            a[j] = tmp;
            loc ++;
        }
    }
    quickSort(a, start, loc - 1);
    quickSort(a, loc + 1, end);
}
```


//5.直接选择排序

```
void straightSelectionSort(int a[], int len) {
    int i,j,mi;
    for (i = 0; i < len; i ++) {
        mi = i;
        for (j = i + 1; j < len; j ++)
            if (a[j] < a[i])
                mi = j;

        if (mi != i) {
            int tmp = a[mi];
            a[mi] = a[i];
            a[i] = tmp;
        }
        description(a, len);
    }
}
```




void insertSortExcute(void) {
    int diso[10] = {10,5,29,88,23,154,32,100,94,90};
//    straightInsertSort(diso, 10);
//    binaryInsertSort(diso, 10);

//    bubbleSort(diso, 10);

//    quickSort(diso, 0, 9);

    straightSelectionSort(diso, 10);

//    int i = 0;
//    while (i < 10) {
//        printf("%d,",diso[i]);
//        i ++;
//    }

}


