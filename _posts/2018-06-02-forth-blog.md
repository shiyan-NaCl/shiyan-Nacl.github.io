---
layout: post
title:  "单行道问题"
date:   2018-06-02 19:47:00 +0800
categories: blog
---
节拍脉冲发生器时序电路实验
========================================  


实验目的：
---------
通过本实验观察死锁产生的现象，考虑解决死锁问题的方法。从而进一步加深对于死锁问题的理解。掌握解决死锁问题的几种算法的编程和调试技术。练习怎样构造管程和条件变量，利用管程机制来避免死锁和饥俄问题的发生。


实验要求：
--------
在两个城市南北方向之间存在一条铁路，多列火车可以分别从两个城市的车站排队等待进入车道向对方城市行驶，该铁路在同一时间，只能允许在同一方向上行车，如果同时有相向的火车行驶将会撞车。请模拟实现两个方向行车，而不会出现撞车或长时间等待的情况。您能构造一个管程来解决这个问题吗？

代码如下
------
**dp.h**

``

    class dp{
    public:
    dp(int rate, int max);
    ~dp();
    void Arrive(int direc);     // 车辆准备上单行道,direc 为行车方向

    void Cross(int direc);      // 车辆正在单行道上
    void Leave(int direc);      // 车辆通过了单行道
    int getNum();
    void addNum();
    void decNum();

    //建立或获取 ipc 信号量的一组函数的原型说明
    int get_ipc_id(char *proc_file,key_t key);

    int set_sem(key_t sem_key,int sem_val,int sem_flag);
    //创建共享内存,放哲学家状

    char *set_shm(key_t shm_key,int shm_num,int shm_flag);

    private:

    int rate;   //车速

    int maxCars;   //最大同向车数
    int numCars;   //当前正在通过的车辆数
    int currentDirec;  //当前方向
    Condition *con;  //通过单行道的条件变量
    Lock *lock;     //单行道管程锁
    //共享变量 
    int* curDire;//当前的方向

    int* isF;//是否为第一辆车

    int* irn;//反向等待的车辆的数量

    int* curn;//当前方向等待的车辆的数量

    int* crossing;  //当前正在通过的车辆的数量

    Sema *mutex;//互斥信号量

    };
``


**dp.c**

``
   
    //当车辆到达时
    void dp::Arrive(int direc)
    {
    int count;

    lock->close_lock();

    mutex->down();
    //获取是否为第一辆车
    count = *isF;
    mutex->up();

    //如果值为0说明是第一辆车
    if(count == 0)
    {       
        mutex->down();
        *curDire = direc;
        *isF = ++count;
        mutex->up();

    }

    if(direc==0)
    {
        printf("%d号车向东等待单行道......\n", getpid());
    }else{
        printf("%d号车向西等待单行道......\n", getpid());
    }


    mutex->down();
    currentDirec = *curDire;
    mutex->up();

    if(currentDirec != direc) {

        mutex->down();
        count = *irn;
        *irn = ++count;
    mutex->up();
        //等待
        con->Wait(lock, direc);

    }

    sleep(1);
    lock->open_lock();

    }


    //当车辆通过时
    void dp::Cross(int direc)
    {
    int count, i;
    lock->close_lock();

       //获得当前正在通过的车辆数
     while(1){
        numCars = getNum();
        if(numCars >= maxCars)
        {
            mutex->down();
            count = *curn;
            *curn = ++count;
            mutex->up();
          con->Wait(lock, direc);
       }else 
               break;
     }

    addNum();
    sleep(1);
    numCars = getNum();

    if(direc==0)
    {
        printf("%d号车向东通过单行道,道上车数:%d\n", getpid(), numCars);
    }else{
    printf("%d号车向西通过单行道,道上车数:%d\n", getpid(), numCars); 
    }

    //sleep(1);

    lock->open_lock();

     }

     void dp::Leave(int direc)
    {
    int count, num;
    lock->close_lock();
    if(direc==0)
    {
        printf("%d号车向东离开单行道\n", getpid(), direc);
    }else{
    printf("%d号车向西离开单行道\n", getpid(), direc);
    }
    //减少当前车的数量
    decNum();



    //正在通过道路的车辆的数量
    numCars = getNum();
    mutex->down();

    //反方向的车辆的数量
    count = *irn;
    //当前方向等待的车辆的数量    
    num = *curn;
    mutex->up();
     //避免饿死 
    //反方向的车辆的数量不为0的话，优先唤醒反方向的车辆的数量
    if(numCars == 0 && count != 0)
    {
        while(count--)
        {
            con->Signal(1 - direc);
        }

        mutex->down();

        *curDire = 1 - direc;
        *irn = *curn;
        *curn = 0;//剩下的还未做cross
        *crossing = 0;
      *isF=0;
        mutex->up();

    }
    //没有反方向的车的时候唤醒同方向的车
    else if(numCars == 0 && num != 0)
    {
        int i=0;
        while(num--)
        {
            con->Signal(direc);
            i++;
        }
        mutex->down();

        *curn = 0;//还是要等于0
        *crossing = 0;
        *isF=0;
        mutex->up();

    }

    lock->open_lock();

    }


``


实验结果
-----
![1](/styles/images/forth/01.png)