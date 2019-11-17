#### 5、插入排序

插入排序的思想：每一步将一个待排序的元素，按其排序码的大小，插入到前面已经排好序的一组元素的适当位置上去，直到元素全部插入为止。

```java
	/*直接插入排序
	  将待插入的元素temp，逐个与已排好序的元素比较，将所有大于temp的元素分别往后移动一位。	
	*/
	public void  insert(int[] array){
       	    int len=array.length;
  	    for(int i=1;i<len;i++){
            int temp=array[i];
            int index=i;
            for(int j=i-1;j>=0 && temp<=array[j];j--){  //往前扫描，将大于temp的数值后移一位
                array[j+1]=array[j];
                index=j;
            }
            array[index]=temp;  //将空缺位放入temp
        }
        System.out.println(Arrays.toString(array));
    }

    /*折半插入排序
      使用二分法查找小于等于待插入元素temp的元素的下标index
      将index以及index之后的所有元素都后移一位
      然后将待插入元素放入到数组下标index的位置上。
    */
    public void bInsert(int[] array){
        int len=array.length;
        int temp,L,R,mid;
        for(int i=1;i<len;i++){
            temp=array[i];
            L=0;
            R=i-1;
            while(L<=R){
                mid=(L+R)/2;
                if(array[mid]<temp){
                    L=mid+1;
                }else{
                    R=mid-1;
                }
            }
            for(int j=i; j>L;j--){	//
                array[j]=array[j-1];
            }
            array[L]=temp;
        }
        System.out.println(Arrays.toString(array));
    }

    /*路插入排序法  空间换时间
      1. 开辟一个辅助数组
      2. 将原数组中的数值分成一大一小两个有序的队列，选原数组的中的第一个数值为两个队列的初始对比值，
    	 >=array[eIndex]的数值有序的从辅助数组的首部往后放，<=array[sIndex]的数值有序的从辅助
    	 数组的尾部往前放。
      3. 如果数值temp处于array[eIndex]<temp<array[sIndex]的情况时，则先将大队列中所有大于temp的
      	 数值往后一位，指针往后移一位。如果大队列的首部数值仍然大于temp，则将小队列的尾部数值补给大队列，			小队列的数值往后移一位填补空缺，最终当小队列中的数值<temp时，停止后移，temp填补小队列的空缺位。
	*/
    public void roadInsert(int[] array){
        int len=array.length;
        int[] a=new int[len];
        int sIndex=0,eIndex=0,temp; //大小指针，数值
       
        a[eIndex]=array[0];  
        for(int i=1;i<len;i++){
            temp=array[i];
            if(temp>=a[eIndex]){	//将>=array[eIndex]的数值放大其的后一位
                a[++eIndex]=temp;  
            }else if(temp<=array[sIndex]){	//<=array[sIndex]的数值放大其前一位
                sIndex=(sIndex-1+len)%len;
                a[sIndex]=temp;
            }else{   //temp 在array[eIndex] 和 array[sIndex]中
                int j=eIndex;
                while(temp<a[j]){  //将大于temp的数值向后移动一位
                    int k=(j+1)%len; 
                    a[k]=a[j];
                    j=(j-1+len)%len;
                }
                a[j+1]=temp;
                eIndex++;  //指针后移一位
            }
        }
        for(int i=0;i<len;i++){  //将辅助数组中的回填原数组
            array[i]=a[sIndex];
            sIndex=(sIndex+1)%len;
        }
        System.out.println(Arrays.toString(array));
    }
```

