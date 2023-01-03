- 👋 Hi, I’m @Kapok-chen
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Kapok-chen/Kapok-chen is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

### 一、数据结构与算法概述

<hr/>

#### 1.1 👀什么是数据结构

```
按照计算机的存储，将数据元素用一定关系表示的集合
```

#### 1.2 📫结构的分类

线性结构：

```
存在一对一的关系，线性结构的存储方式分为顺序存储（顺序表【数组、队列、栈】）和链式存储（链表【存储元素地址可以连续也可以不连续】）

顺序存储和链式存储的主要区别：就是地址连续与不连续
```

非线性结构

```
二位数组、多为数组、广义表、树、图
```



#### 1.3 👋数组

##### 稀疏数组

> 引例：一个棋盘，如何记载黑白两子的位置？
>
> 我想到的是二维数组，但是二维数组的默认值是0，就浪费了许多的存储空间

此时，可以采用稀疏数组

> 思路：用一个数组只记录几行几列，有多少个不同的值，把不同的值以及行列记录在一个小规模的数组中，从而达到压缩数组的目的

> 原始数组

![1672410674508](E:\学习\专业学习\数据结构\pic\1672410674508.png)

> 下标为0的 只记录了总行、总列，共计多少个不同元素
>
> 剩下的下标，记录了具体的行列，和具体的元素

![1672410285791](E:\学习\专业学习\数据结构\pic\1672410285791.png)

> 稀疏数组的应用场景，五子棋，地图
>
> 二维数组==>转稀疏数组
>
> 1.遍历整个二维数组，得到总有效个数 sum
>
> 2.根据sum 创建稀疏数组 sparseArr int [sum+1][3]
>
> 3.将二维数组的有效值，存入到稀疏数组中

代码实现

先把棋盘创建出来

```java
        // 创建一个原始的二维数组 11*11
        //0表示无子，1为黑子，2为白子
        int chessArra[][] = new int[11][11];
        //第一行，第二列为黑子
        chessArra[1][2] = 1;
        //第二行，第三列为白子
        chessArra[2][3] = 2;
        //输出数组
        for (int[] row:chessArra){
            for (int data:row){
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }
```

```java
0	0	0	0	0	0	0	0	0	0	0	
0	0	1	0	0	0	0	0	0	0	0	
0	0	0	2	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
```



```java
        // 创建一个原始的二维数组 11*11
        //0表示无子，1为黑子，2为白子
        int chessArra[][] = new int[11][11];
        //第一行，第二列为黑子
        chessArra[1][2] = 1;
        //第二行，第三列为白子
        chessArra[2][3] = 2;
        //输出数组
        for (int[] row:chessArra){
            for (int data:row){
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }

        //将二维数组 ===》 稀疏数组，遍历二维数组，得到非0的个数
        int sum = 0;
        for (int i = 0; i < chessArra.length; i++) {
            for (int j = 0; j < chessArra.length; j++) {
                if (chessArra[i][j] !=0){
                    sum++;
                }
            }
        }
        // 打印非0个数
        System.out.println(sum);

        //创建稀疏数组
        int sparseArr[][] = new int[sum+1][3];
        //给稀疏数组赋值
        sparseArr[0][0] = 11;
        sparseArr[0][1] = 11;
        sparseArr[0][2] = sum;

        //将二维数组非0值，存放到稀疏数组中
        //count 用于记录是第几个非0的数据
        int count = 0;
        for (int i = 0; i < chessArra.length; i++) {
            for (int j = 0; j < chessArra.length; j++) {
                if (chessArra[i][j] !=0){
                    //非0数据
//                    sparseArr[?][0] = i;
//                    sparseArr[?][1] = j;
//                    sparseArr[?][2] = chessArra[i][j]
                    count++;
                    sparseArr[count][0] = i;
                    sparseArr[count][1] = j;
                    sparseArr[count][2] = chessArra[i][j];
                }
            }
        }


        for (int[] row:sparseArr){
            for (int data:row){
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }
    }
```

```java
0	0	0	0	0	0	0	0	0	0	0	
0	0	1	0	0	0	0	0	0	0	0	
0	0	0	2	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	

11	11	2	
1	2	1	
2	3	2	
```



还原二维数组

```java
        // 创建一个原始的二维数组 11*11
        //0表示无子，1为黑子，2为白子
        int chessArra[][] = new int[11][11];
        //第一行，第二列为黑子
        chessArra[1][2] = 1;
        //第二行，第三列为白子
        chessArra[2][3] = 2;
        //输出数组
        for (int[] row:chessArra){
            for (int data:row){
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }

        //将二维数组 ===》 稀疏数组，遍历二维数组，得到非0的个数
        int sum = 0;
        for (int i = 0; i < chessArra.length; i++) {
            for (int j = 0; j < chessArra.length; j++) {
                if (chessArra[i][j] !=0){
                    sum++;
                }
            }
        }
        // 打印非0个数
        System.out.println(sum);

        //创建稀疏数组
        int sparseArr[][] = new int[sum+1][3];
        //给稀疏数组赋值
        sparseArr[0][0] = 11;
        sparseArr[0][1] = 11;
        sparseArr[0][2] = sum;

        //将二维数组非0值，存放到稀疏数组中
        //count 用于记录是第几个非0的数据
        int count = 0;
        for (int i = 0; i < chessArra.length; i++) {
            for (int j = 0; j < chessArra.length; j++) {
                if (chessArra[i][j] !=0){
                    //非0数据
//                    sparseArr[?][0] = i;
//                    sparseArr[?][1] = j;
//                    sparseArr[?][2] = chessArra[i][j]
                    count++;
                    sparseArr[count][0] = i;
                    sparseArr[count][1] = j;
                    sparseArr[count][2] = chessArra[i][j];
                }
            }
        }


        for (int[] row:sparseArr){
            for (int data:row){
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }

        //将稀疏数组还原为二维数组
        //1.先读取稀疏数组
        int chessArr2[][] = new int[sparseArr[0][0]][sparseArr[0][1]];

        //读取稀疏数组 重新赋值给 二维数组
        for (int i = 1; i < sparseArr.length; i++) {
            chessArr2[sparseArr[i][0]][sparseArr[i][1]] = sparseArr[i][2];
        }

        for (int[] row:chessArr2){
            for (int data:row){
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }
```

```java
0	0	0	0	0	0	0	0	0	0	0	
0	0	1	0	0	0	0	0	0	0	0	
0	0	0	2	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
2
11	11	2	
1	2	1	
2	3	2	
0	0	0	0	0	0	0	0	0	0	0	
0	0	1	0	0	0	0	0	0	0	0	
0	0	0	2	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
```



##### 队列

> 队列的特点是先进先出，可以用**数组和链表实现**
>
> > 队列有队头【front】,队尾【rear】,出队是 front ；入队是在rear
>
> 实现思路：当入队时，rear+1，队空时需要判断 front == rear，每次入队时都需要判断是否队满
>
> ​				队满：需要 rear == maxSize-1
>
> 使用场景：银行的叫号系统

```java
// 用数组模拟队列，编写ArrayQueue类
class ArrayQueue{
    private int maxSize;//表示当前队列的最大容量
    private int front;//队头
    private int rear;//队尾
    private int[] arr;//该数组用于模拟队列，存放数据

    //创建队列的构造器
    public ArrayQueue(int arrMaxSize){
        maxSize = arrMaxSize;
        arr = new int[maxSize];

        //初始化队列时，front指向队列头部前一个位置。rear指向队尾的最后一个数据
        front = rear = -1;
    }

    //判断队是否满
    private boolean isFull(){
        return rear == maxSize - 1;
    }

    //判断队空
    private boolean isQueueEmpty(){
        return rear == front;
    }

    //入队
    public void addQueue(int n){
        //判断队满
        if (isFull()){
            System.out.println("队满");
            return;
        }

        //让rear的下标向后移，就实现队尾的指针向后移了
        rear++;
        arr[rear] = n;
    }

    //出队
    public <T> Object outQueue(){
        //出队判断队空
        if (isQueueEmpty()){
            //为空抛出异常
            return new RuntimeException("队列为空");
        }
        front++;//出队是在队头
        System.out.println("出队元素为："+arr[front]);
        return arr[front];
    }

    //获取队列中的所有数据
    public void getQueue(){
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```



```java
    public static void main(String[] args) {
        ArrayQueue arrayQueue = new ArrayQueue(3);
        arrayQueue.addQueue(1);
        arrayQueue.addQueue(2);
        arrayQueue.addQueue(3);
        arrayQueue.getQueue();
        //出队
        arrayQueue.outQueue();
        arrayQueue.outQueue();
        arrayQueue.outQueue();
    }
```

```java
1
2
3
出队元素为：1
出队元素为：2
出队元素为：3
```



##### 循环队列

> 让 front 指向队列的第一个元素，也就是数组的第一个元素 from = 0
>
> 让 rear 指向队列的最后一个元素的后一个位置【rear = 0】，希望空出一个空间，这个空间就是为了判断队列是否满了，在入队时看是否还有空间可以。在对 队容量取模
>
> 此时的队满条件为 （rear+1）% maxSize == front
>
> 队空：rear ==  front
>
> 队列的有效元素个数为：（rear + maxSize - front）% maxSize



```java
//模拟循环队列
class CircleQueue{
    private int maxSize;//表示队列的最大容量
    private int front;//队头
    private int rear;//队尾
    private int[] arr;//数组模拟循环队列

    //初始化队列
    public CircleQueue(int arrMaxSize){
        maxSize = arrMaxSize;
        arr = new int[maxSize];
        //初始换队头，队尾元素
        front = 0;
        rear = 0;
    }

    //判断队满
    public boolean isFull(){
        return (rear + 1) % maxSize == front;
    }

    //判断队空
    public boolean isQueueEmpty(){
        return front == rear;
    }

    //入队
    public void addQueue(int n){
        //判断队满
        if (isFull()){
            return;
        }
        //队列没有满就入队,因为队尾本身就指向数组的第一个元素，所以不需要++操作
        arr[rear] = n;
        // 将指针向后移
        rear = (rear + 1) % maxSize;
    }

    //出队
    public <T> Object outQueue(){
        //判断队列是否为空
        if (isQueueEmpty()) {
            return new RuntimeException("队满");
        }
        //出队在队头出，因为队头指针指向的也是数组的第一元素，先将队头元素保存到一个临时变量中，再将队头指针后移
        int temp = arr[front];
        front = (front + 1) % maxSize;
        System.out.println("出队"+temp);
        return temp;
    }

    //打印队列
    public void getQueue(){
        // 遍历队列中的有效元素
        int effectiveEle = (rear + maxSize - front) % maxSize;
        for (int i = front; i < front+effectiveEle; i++) {
            System.out.println(arr[i]);
        }
    }
}
```



此时的有效数据为2，因为预留一个空间位置

```java
    public static void main(String[] args) {
        CircleQueue circleQueue = new CircleQueue(4);
        circleQueue.addQueue(1);
        circleQueue.addQueue(2);
        circleQueue.addQueue(3);
        circleQueue.getQueue();

        circleQueue.outQueue();
        circleQueue.addQueue(4);
        circleQueue.getQueue();

    }
```

```
1
2
3
出队1
2
3
4
```



#### 1.4 👋链表

> 分为是否带 头节点
>
> > 链表带有头节点的有三个部分组成：头节点【存放的是地址】、data域、next域【存放下一个元素地址】
> >
> > 不带头节点的有两个部分组成：data域、next域
>
> > 头节点不存放数据

物理结构【也是在内存中的实际存储结构不连续】                               逻辑结构【连续】

![1672624723190](E:\学习\专业学习\数据结构\pic\1672624723190.png)![image-20230102100726967](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230102100726967.png)

```java
//节点对象，每一个HeroNode都是一个节点对象
class HeroNode{
    public int hno;//编号
    public String name;//名字
    public String nickeName;//昵称
    public HeroNode next;//下一个节点

    //构造器
    public HeroNode(int hno,String name,String nickeName){
        this.hno = hno;
        this.name = name;
        this.nickeName=nickeName;
    }

    //打印
    @Override
    public String toString() {
        return "HeroNode{" +
                "hno=" + hno +
                ", name='" + name + '\'' +
                ", nickeName='" + nickeName + '\'' +
                '}';
    }
}

//定义一个 SingleLikedList 来管理英雄
class SingleLikedList{
    //1.初始化一个头节点,只是代表头节点，不存放任何数据
    private HeroNode headNode = new HeroNode(0,"","");

    //添加节点到单向链表
    //实现思路：当不考虑当前链表编号的顺序时
    //1. 找到当前链表的最后一个节点
    //2. 将最后这个节点的 next 指向新的节点
    public void addNode(HeroNode node){
        // headNode 不能懂，所以需要一个临时变量，保持头节点不能动
        HeroNode temp = headNode;

        //遍历找到最后
        while (true){
            //找到链表的最后了
            if (temp.next == null){
                break;
            }

            //如果没有找到最后，就将temp往后移
            temp = temp.next;
        }

        //当退出while循环时，此时的temp就指向了链表的最后, 让temp指向下一个节点
        temp.next = node;
    }

    //显示链表【遍历】
    public void showInfo(){
        //先判断链表是否为空
        if (headNode.next == null){
            System.out.println("链表为空");
            return;
        }

        //遍历链表时，需要不停的指向下一个节点，头节点又不能动
        HeroNode temp = headNode.next;
        while (true){
            //先判断是否到链表最后
            if(temp == null){
                break;
            }
            //如果不为空，就打印节点信息
            System.out.println(temp);
            //temp后移，找到下一个节点
            temp = temp.next;
        }
    }
}
```

```java
    public static void main(String[] args) {
        HeroNode heroNode1 = new HeroNode(1,"宋江","及时雨");
        HeroNode heroNode2 = new HeroNode(2,"卢俊义","玉麒麟");
        HeroNode heroNode3 = new HeroNode(3,"吴用","智多星");
        HeroNode heroNode4 = new HeroNode(4,"林冲","豹子头");

        SingleLikedList singleLikedList = new SingleLikedList();
        singleLikedList.addNode(heroNode1);
        singleLikedList.addNode(heroNode4);
        singleLikedList.addNode(heroNode3);
        singleLikedList.addNode(heroNode2);

        singleLikedList.showInfo();
    }
```

```java
HeroNode{hno=1, name='宋江', nickeName='及时雨'}
HeroNode{hno=4, name='林冲', nickeName='豹子头'}
HeroNode{hno=3, name='吴用', nickeName='智多星'}
HeroNode{hno=2, name='卢俊义', nickeName='玉麒麟'}
```

