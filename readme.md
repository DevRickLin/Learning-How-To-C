# 常见问题

### 如何提问

​	好的提问可以让他人在帮助和指导你的时候更加容易，这对你有帮助，也对试图要解决你的问题的人有帮助。

​	关于这方面，已经有了很好的[指南](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way)，而在这边只简单列出可能有帮助的几点:

1. ##### 在提问之前，尽可能靠自己去排除:

   靠自己Debug是一名码农的重要修养:

   1. 如果编译不过，先自己查看IDE的报错讯息。

   2. 如果在CSUOJ上无法通过，仔细考虑一下CSUOJ提供的回馈。多测试几次，尽可能去设想一些极端情形(以输入数值为例，考虑一下零、极大的数值、负值等)，如果老师已经提供了测试数据，可以多比对几下(之后会提一下如何方便的去比对自己的输出结果和文档)。

   3. 在代码中穿插printf()把一些运行中的变量、表达式的结果印出来，这通常对判断问题出在哪裡有帮助。以下为例:

      ```c
      #include <stdio.h>
      //输出n!
      int main(void)
      {
          int n;
        	int sum = 1;
          while(scanf("%d",&n)!=EOF)
          {
              for(int i=1;i=<n;i++)
              {
                  sum*=i;
              }
         		printf("%d",sum);
          }
          return 0;
      }
      ```

      在这个代码中，我们会发现他第一次输出的值是正确的，但第二次及以后都会出错，或许问题已经很明显了，但我们可以使用以上的方法来侦错:

      ```c
      #include <stdio.h>
      //输出n!
      int main(void)
      {
          int n;
        	int sum = 1;
          while(scanf("%d",&n)!=EOF)
          {
              printf("before here the sum is: %d",sum);
              for(int i=1;i=<n;i++)
              {
                  sum*=i;
              }
         		printf("%d",sum);
          }
          return 0;
      }
      ```

      在执行这个程序时，我们第一次输入2，输出是这样的:

      ```
      before here the sum is: 1
      2
      ```

      第二次输入2，输出是这样的:

      ```
      before here the sum is: 2
      4
      ```

      这时候，问题应该就看得出来了。(有些IDE的侦错模式会比这个更方便)
      
   4. **好好看一下这篇文档，你的问题可能就在其中**(没人看的话还是挺难过的QQ)

      

2. ##### 在提问时，把遇到的问题描述清楚

   1. 你本来想要做甚麽?

      假如能够在提问时，顺便**把你的代码旁边附上精美的注解，或是精要的把你的算法如何实现给描述一下**，都可以大大节省别人读懂你代码的时间，你也会更快得到回覆。(注解也通常在你以后要回来查看自己写过的程序的时候会有帮助，也能帮助当下的你理清思路)

   2. 你遇到了甚麽样的问题?

      假如在网站上运行，网站给出了甚麽样的回馈? 假如某些输出的结果很奇怪，那你本来的输入是甚麽?
      **尽可能地给出和问题有关的所有线索，通常在你釐清线索的同时，有些问题也自然就解决了。**

   3. 有图比没有图更好，有代码比有图更好

      有些贴上代码后跑几个测试就能解决的问题，光是看图的话就会多花上不少时间。若是连图都没有的话，就更没有人知道你到底遇到了甚麽问题了。

      

3. ##### 给出适当的回馈

   不一定要在别人回答完问题之后表现得感激万分，但作为同样在编程路上的同伴们，一定要记得**在问题解决了之后把结果回报给帮你解决问题的人**。因为你走过的坑别人也会需要避开，这些帮助你的人，可能心底依然很好奇:"这样改了就行了吗?"或是"对方到底是把问题解决了，还是没有解决，只是~~出车祸~~ 暂时搁置了?"

   解决完了问题，说一句:"果然是大佬，成了!"，让我们一起分享解决问题的喜悦吧。

   
   
### 关于在CSUOJ上运行的问题:

1. #### 多样例测试

   1. ##### 循环

      在CSUOJ上大部分的题目都会进行多样例测试，这指的是你的输入和输出行为要循环不只一次，解决方案如下:

      ```c
      #include <stdio.h>
      int main(void)
      {
          //你需要设置在循环外的变量
          while(scanf(/*你的输入格式及变量*/)!=EOF)
          {
              //你的主程序
          }
          return 0;
      }
      ```

      > scanf()函式会在每次执行时回传它成功把多少对应的值给了变量，并在接受到EOF(文件结尾)时回传-1，因此检查scanf()!=-1的效果是一样的，更详细正确的内容可以参考如下:
      >
      > https://www.runoob.com/cprogramming/c-function-scanf.html

   2. ##### 换行

      在CSUOJ 上，通常要求每个样例输出只占一行，若是不换行就会过不了，记得修改为循环的格式后，每次样例输出也要换个行。
      
      **如果不同条件下写了不同的输出语句的话(例如有两个在不同条件下执行的scanf()，记得也都要换行。**
      
   3. ##### 判断EOF
   
      这和第一个循环的问题有著很大联繫，若是发现自己的程序在修改了之后，输入Ctrl+Z依然无法跳出，抑或是在CSUOJ提交后有**时间超限**等等类似的错误，先注意自己有没有犯以下问题:
   
      1. 错误的使用scanf("%c",&c)判断EOF
   
         scanf("%c",&c)接收到EOF之后，并不会将EOF交给字符变量c而是会**返回-1**，对于一些初学者来说，函数的返回值是一个比较难懂的概念，但只要注意以下以及类似的写法是错误的:
   
         ```c
         do{
             scanf("%c",&c);
             //循环内容
         }while(c!='\n'&&c!=EOF);
         ```
   
         根据前述，EOF是不会被交给c的，所以do迴圈去判断c!=EOF只会永远为真。
   
         以下有两种可以参考的正确写法，但注意不同的break时机点会对程序造成不同的影响，请挑选适合自己的方法使用:
   
         方法1:在迴圈内进行break:
   
         ```c
         do{
             if(scanf("%c",&c)==EOF)
             {
                 break;
             }
             //循环内容
         }while(//自己的条件)
         ```
   
         方法二:另外给一个变量接受EOF:
   
         ```c
         int f;
         do{
             f=scanf("%c",&c);
             //循环内容
         }while(f!=EOF//再加上一些自己的条件...)
         ```

### C语法格式问题

1. #### switch 

   在使用switch函数时常见以下问题:

   1. ##### 省略case和其后常量之间的空格:

      ```c
      switch(n)
      {
      	case0:
              break;
          case1:
              break;
          dafault:
      }
      ```

      这样写的话，switch会直接执行default，记得一定要有空格:

      ```c
      switch(n)
      {
      	case 0:
              break;
          case 1:
              break;
          default:
      }
      ```

   2. ##### 忘记break:

      这也是switch比较容易被忘记的特性，不在case执行完后break的话，程序会接著执行之后case的内容(不管你写的判断条件为何)，以下举例:

      ```c
      int n = 0;
      switch(n)
      {
          case 0:
             	n = 1;
          case 2:
              n = 2;
      }
      printf("%d",n);
      ```

      这个例子最后输出的是2。

2. #### while循环

   1. 省略大括号

      省略大括号一时爽，之后你就不会爽了，省略大括号会让你的while只循环其后;前的那一部分代码，大部分时候这都不是你想要的行为，以下满天星的代码为例:

      ```c
      while(true)/*只会循环这个部分*/;
      	printf("*");//不会在循环内执行
      ```

      修改如下就会正确运行了:

      ```c
      while(true)
      {
      	printf("*");
      }
      ```

3. #### main内的return

   1. 放错位置

      请参考以下案例:

      ```c
      int main(void)
      {
      	return 0;
          printf("test");
      }
      ```

      在这种情况下，"test"是不会被输出的，主函数(就是main那个东东)会在你return之后立刻结束执行，通常这种错误会犯在同学把程序修改成用while(scanf()!=EOF)的格式后，不小心把return包进了while循环裡。

4. #### scanf 函数

   1. 忘记在参数变量前加&

      你不该犯这个错误。(字符串例外，不需要加)

      ```c
      scanf("%d",n);//棒棒糖
      ```

   2. 忘记逗号

      ```c
      scanf("%d"n);//棒棒糖?
      ```

5. #### printf 函数

   1. 加了&

      ```c
      printf("%d",&n);
      ```

   2. 拼写错误

      ```c
      print("%d",n);
      ```


### C程序设计问题

1. #### 变量放错位置/需要在每次循环重置的变量没有重置

   这个问题通常发生在同学们将程序修改成while(scanf()!=EOF)的格式之后，提交太多次的话在排名上难免看起来不好看，记得上传之前都先在本地端多测试几组样例，看看是否有正确的重置。

   以下为例:

   ```c
   #include <stdio.h>
   //输出n!
   int main(void)
   {
       int n;
     	int sum = 1;
       scanf("%d",&n);
       for(int i=1;i=<n;i++)
       {
           sum*=i;
       }
       printf("%d",sum);
       return 0;
   }
   ```

   通常修改后会犯的错误:

   ```c
   #include <stdio.h>
   //输出n!
   int main(void)
   {
       int n;
     	int sum = 1;
       while(scanf("%d",&n)!=EOF)
       {
           for(int i=1;i=<n;i++)
           {
               sum*=i;
           }
      		printf("%d",sum);
       }
       return 0;
   }
   ```

   通常这种时候，同学就会到群裡面问:

   > 为什么第一次跑的时候是对的，之后都错了?

   我们观察一下这个程序的行为，会发现，在第一个while循环时，sum的确是我们想要的1，但当他进入下一次循环，sum已经是上一次的n!了，结果自然不会对。

   修改如下即可:

   ```c
   #include <stdio.h>
   //输出n!
   int main(void)
   {
       int n;
       while(scanf("%d",&n)!=EOF)
       {
        	int sum = 1;
           for(int i=1;i=<n;i++)
           {
               sum*=i;
           }
      		printf("%d",sum);
       }
       return 0;
   }
   ```

2. #### 下标溢位/指针指向了没有赋值的地址

   **假如你的输出是预期上不可能出现的值，或是乱码的话，看这裡**

   这种问题容易发生在循环遍历数组的时候，记得: 

   > 一个长度为2的数组，最后一位是1(因为是从0开始算的)。

   那么，如果下标超出了最大值会发生甚么事呢?

   操作数组下标等于是进行指针操作，输入下标n等于是从数组的第一个地址往后位移n位，以下为例:

   ```c
   int a[2] = {0,1};
   printf("%d\n",a[1]);
   printf("%d",*(a+1));
   ```

   输出会是:

   ```
   1
   1
   ```

   因此，当下标超过最后一位的时候，他就会指向更后面的一个地址，而那个地址保存了甚么是未知的，如果对这个地址进行赋值的话，也会修改掉一个未知地址内的值(所以会发生甚么很难预期)。
   因此，如果在循环中对数组进行遍历的话，多注意循环会循环几次，还有对数组使用的局部变量究竟是1,2,3,...,n还是0,1,2,...,n-1。

3. #### 接收到空格

   **gets函数会在接收到换行符之后立刻跳出，因此也要注意这个问题。**

   c=getchar()函数和scanf("%c",&c)的行为类似，会接收换行符这个字符并传递到c里。这通常会导致一些不如预期的行为，以下程序为例:

   ```c
   //超级计算机
   #include<stdio.h>
   int main()
   {
   	int M1,M2,R1,R2,R3;
       char c;
       while(scanf("%d %d",&M1,&M2)!=EOF)
       {
       	R1=0,R2=0,R3=0;
   		int f;
   		do
   		{
   	    	f = scanf("%c",&c);
   	    	switch(c)
   			{
   				case 65:R1=M1;break;
   				case 66:R2=M2;break;
   				case 67:M1=R3;break;
   				case 68:M2=R3;break;
   				case 69:R3=R1+R2;break;
   				case 70:R3=R1-R2;break;
   			}
   		}while(f!=-1&&c!='\n');
   		printf("%d,%d\n",M1,M2);
   	}
   	return 0;
   }
   ```

   我做一个输入:

   ```
   100 288
   ABECED
   ```

   预期的输出会是:

   ```
   388 388
   ```

   实际上的输出是:

   ```
   100 288
   ```

   (而且没有等待你输入指令)
   
    这其实就是底下的scanf("%c",&c)将'\n'给了c之后，在do循环的判断中使得c!='\n'的判断为假，便直接跳出循环执行了printf()。
   
     一个常见的办法便是在进入迴圈之前，先把上一个输入的换行符利用一个getchar()或是scanf("%c")接收掉，再进入do循环。
   
   
   
     底下是修改好的例子:
   
   ```c
   //超级计算机
     #include<stdio.h>
     int main()
     {
     	int M1,M2,R1,R2,R3;
         char c;
         while(scanf("%d %d",&M1,&M2)!=EOF)
         {
             scanf("%c");//接收掉换行
         	R1=0,R2=0,R3=0;
     		int f;
     		do
     		{
     	    	f = scanf("%c",&c);
     	    	switch(c)
     			{
     				case 65:R1=M1;break;
     				case 66:R2=M2;break;
     				case 67:M1=R3;break;
     				case 68:M2=R3;break;
     				case 69:R3=R1+R2;break;
     				case 70:R3=R1-R2;break;
     			}
     		}while(f!=-1&&c!='\n');
     		printf("%d,%d\n",M1,M2);
     	}
     	return 0;
     }
   ```
   
   



### 如何共同编辑

1. #### 直接和我联繫:

   由于底下的操作对于没有接触过git或Github的人可能比较複杂，各位可以直接将自己编写好的内容用任何形式发给我，再由我进行彙整，本人的邮箱:

   >  8208200137@csu.edu.cn

   或是可以直接在QQ群裡发布文件，注明要提交到这裡就行了:

2. #### 使用Github的Fork功能:

   由于本人力有未逮，底下的教学可能并不是非常有帮助，建议初学者可以多参考这边给出的几个教学连结了解如何操作Github和git，还有如何使用Markdown:

   **git和Github的操作:**

   [知乎](https://www.zhihu.com/topic/19566035/index#module-2749)

   [github漫游指南](https://github.phodal.com/)

   **Markdown相关:**

   [Markdown 基本语法](https://github.com/younghz/Markdown)

   [Typora编辑器](https://typora.io/)

   

   **以下教学正文:**

   首先，你需要创建一个Github帐号，只要到[Github首页](https://github.com/)就可以注册。注册完毕后，回到此文件的页面，点击右上角的Fork:

   ![fork1](image/fork1.png)

   这会在你的帐号创建一个和我这个一模一样的文件，你便可以点击**铅笔图样**对此文件进行编辑，如果熟悉如何操作git的话，也可以先把这个文件clone到本地端去再用自己的编辑器打开。或者，直接打开自己的编辑器複製贴上，编辑完再回去github上的编辑页面进行贴上也可以。

   编辑完成后，回到此文件的页面，点击Pull request，再点击new pull request:

   ![fork2](image/fork2.png)

   之后点击compare across forks、在底下选择自己的版本，然后点选create pull request。

   ![fork3](image/fork3.png)

   

   之后再点击create pull request一次就成功将你的版本交出了。点击前建议把具体修改了哪些部分留在底下的评论栏裡，但不输入一样可以提交。

   ![fork4](image/fork4.png)
