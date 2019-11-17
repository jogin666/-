#### 1、选择排序

​		选择排序的思想：每次从待排序的数组中确定该段中的最小/大值的数组下标，然后将待排序数组段的首/尾位与确定的最小/大值交换数值。

```java
	public void select(int[] array){
		int len=aray.length;
		int index,temp;
		for(int i=0;i<len-1;i++){
			index=i;
			for(int j=i+1;j<len;j++){
				if(array[index]>array[j])	//选择最小值的下标
					index=j;
			}
			temp=array[i];
			array[i]=array[index];
			array[index]=temp;
		}
	}
```



#### 2、交换排序

​		交换排序的思想：每次将待排序的元素中，选取第一个数值temp与后面的元素比较，如果temp大于比较元素

，则两个元素交换，再用交换后的元素与下一个元素比较，循环。最终确定了待排序元素中的首部为最小值。

```java
	public void compareSwap(int[] array){
	
		int len=array.length;
		for(int i=0;i<len-1;i++){
			for(int j=i+1;j<len;j++){
				if(array[i]>array[j]){		//大于交换
					int temp=array[i];
					array[i]=array[j];
					array[j]=temp;
				}
			}
		}
	}
```





