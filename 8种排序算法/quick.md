#### 6、快速排序

​		快速排序思路：不断的将待排序的元素按照与某个元素值比较划分成成两个一大一小的两个序列，将本来乱序的元素就行了一定的有序化。最终量变引起质变，每次一定的有序化最终汇成有序化。

```java
	
	public void quick(int[] array){
		int len=array.length;
        quickHelper(array,0,len-1);
        System.out.println(Arrays.toString(array));
	}

	// 1、选取首部作为哨兵
	private void quickHelper(int[] array,int L,int R){
        if(L>=R){
            return;
        }
        int i=L,j=R;
        int temp=array[L];  //选取待排序元素的头元素作为哨兵
        while(i<j){
            while(array[j]>=temp && j>i){  //由后向前扫，寻找比哨兵小的元素num1
                j--;
            }
            array[i]=array[j];	//将num1放入空缺的位置
            while(array[i]<=temp && i<j){	//由前往后扫，寻找比哨兵大的元素num2
                i++;
            }
            array[j]=array[i];	//将num2放入空缺的位置
        }
        array[i]=temp;  //哨兵回填空缺位置
        quickHelper(array,L,i); //递归小元素序列
        quickHelper(array,i+1,R);	//递归大元素序列
    }

	// 2、选取中间作为哨兵
	private void quickHelper(int[] array,int s,int e){
        int i=s,j=e;
        int temp=array[(i+j)/2]; //选取待排序元素的
        while(i<=j){
            while(array[i]<temp){ //由前向后扫，寻找比哨兵小的元素
                i++;
            }
            while(array[j]>temp){ //由后往后前，寻找比哨兵大的元素
                j--;
            }
            if(i<=j){   // 将发现小于/大于哨兵的元素交换位置  （其中i<=j 保证跳出循环）
                int num=array[i];
                array[i]=array[j];
                array[j]=num; 
                i++;    
                j--;
            } 
        }
        if(s<j){
            quickHelper(array,s,j); //递归小元素序列
        }
        if(i<e){
        	quickHepler(array,i,e);  //递归大元素序列
        }    
    }
```


