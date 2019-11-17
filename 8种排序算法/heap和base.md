#### 7、堆排序

​		大小顶堆：大顶堆就是每一个堆顶值都大于左右子堆的值，小顶堆的堆顶值都小于左右子堆的值。

​		堆排序思想：堆排序使用的是大顶堆的思路。每次将待排序的元素建成大顶堆，建成堆后，堆顶的元素便是

最大值，也就是待排序元素的首部为最大值。然后将排序元素的首尾元素交换。便排序好一个元素。如此重复上述

步骤。

```java
	public void heap(int[] array){

        int len=array.length-1;
        for(int i=0;i<=len;i++){ //确定排好序的元素个数
            int s=(len-i)>>1;
            int size=len-i;  //尾部倒数的i个数已排好序，不需要访问比较
            for(int j=s;j>=0;j--){  //建立大顶堆
                int left=(j<<1)+1;
                int right=left+1;
                if(right<=size && array[right]>array[left]){  //选取左右子堆的最大值
                    left=right;
                }
                int maxIndex=j;
                if(left<=size && array[maxIndex]<array[left]){  //子堆的最大值与堆顶比较
                    maxIndex=left;
                }
                if(maxIndex!=j && array[j]<array[left]){  //堆顶是否为最大值
                    int temp=array[left];
                    array[left]=array[j];
                    array[j]=temp;
                }
            }
            int num=array[0];		//然后将待排序元素的首尾值交换
            array[0]=array[len-i];
            array[len-i]=num;
        }
        System.out.println(Arrays.toString(array));
    }
```



#### 8、 基数排序（桶排序）

​		 基数排序思想：基数排序是基于分配与回收的思想，由低位向高位逐个获取位数的数值，按照位数的数值进行0~9分配，所有数值分配好，再进行回收。然后进行下一位的位数数值的分配与回收。如此返回知道最大数值的所有为分配与回收的操作。整个排序就完成了。其本质是将比较化为分配，其实在将分配的时候，就是关键字的比较。相同的位数数值时，最高位较大的数值肯定大的数。

```java
	public void base(int[] array){

        int len=array.length;
        int max=max(array);
        for(int i=1;(max/i)>0;i=i*10){	//控制循环次数

            int[][] bucket=new int[len][10];  //len：一个桶可能放多个数值 	10：为0~9基数（桶数）
            for(int j=0;j<len;j++){
                int num=(array[j]/i)%10; //获取位数的数值
                bucket[j][num]=array[j];  //放入到桶中（二维数组中，同一个桶不同的位置，行列不同）
            }
            //开始回收桶内的元素，也就是按照二维数组的每一列回收
            int k=0; //数组下标
            for(int c=0;c<10;c++){  //列数
                for(int r=0;r<len;r++){	//行数
                    if(bucket[r][c]!=0){
                        array[k++]=bucket[r][c];
                    }
                }
            }
        }
        System.out.println(Arrays.toString(array));
    }

    private int max(int[] array){
        int len=array.length;
        int index=0;
        for(int i=1;i<len;i++){
            if(array[index]<array[i]){
                index=i;
            }
        }
        return array[index];
    }
```



