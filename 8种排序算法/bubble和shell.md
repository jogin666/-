#### 3 、冒泡排序

​		冒泡排序的思想：每一次在待排序的元素中，相邻的两个元素作比较，将较小的元素往前一位，大的元素后

一位。每一次比较完，便可以确定待排序元素中的最大/小值。最大/小值放到待排序的尾/首部。

```java
	public void bubble(int[] array){
        
	   int len=array.length;
	   for(int i=0;i<len;i++){
              for(int j=0;j<len-1-i;j++){
                 if(array[j]>array[j+1]){	//两两比较，小的前移，大的后移
                     int temp=array[j];
                     array[j]=array[j+1];
                     array[j+1]=temp;
                 }
             }
          }
	}
```





#### 4、希尔排序 

​		希尔排序的思想：在开始排序的时候选定一个步长。在按照步长间隔将待排序的元素虚拟分为几个序列 ，然

后交替使用插入排序的思想将每一个序列中元素进行排序。访问完序列之后，每一个间隔距离为步长的虚拟序列

都是有序的了。重复尚须步骤。对于步长，在初始选定后，之后的循环中步长都是自减半，最终步长为0时，排序

结束。

```java
	public void shell(int[] array){

        int len=array.length;
        while(len>0){
            len=len/2; //控制步长
            for(int i=len;i<array.length;i++){  //交替访问分组内数据（如步长为2时 ，1 3 5  2,4，6）
                for(int j=i-len;j>=0 && array[j]>array[j+len];j=j-len){  //组内往前扫描
                    int temp=array[j];
                    array[j]=array[j+len];
                    array[j+len]=temp;
                }
            }
        }
        System.out.println(Arrays.toString(array));
    }

	public void shell(int[] array){

        int len=array.length;
        //设置步长 每次步长减半）
        for(int step=len/2;step>0;step=step/2){
            //交替访问每组内的元素
            for(int i=step;i<array.length;i++){
                int temp=array[i];
                int index=i;
                //组内往前扫面比较，小于则交换，前一个数往后移动
                while(index-step>=0 && array[index-step]>temp){
                    array[index]=array[index-step];
                    index=index-step;
                }
                //填补该组内的空缺
                array[index]=temp;
            }
        }
        System.out.println(Arrays.toString(array));
    }
```





