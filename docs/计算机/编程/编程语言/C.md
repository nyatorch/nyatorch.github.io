# C

> 来源 [Learn X in Y minutes](https://learnxinyminutes.com/docs/c/)

```
// 单行注释以 // 开始，仅适用于C99及以后。

/*
多行注释看起来像这样，对于 C89 也适用
*/

/*
多行注释不能被嵌套 /* 务必小心 */  // 这条注释在这一行就终止了
*/ // 而不是这一行！

// 常量： #define <关键字>
// 常量完全写成大写字母是惯例，不是必须的要求
#define DAYS_IN_YEAR 365

// 枚举常量也是声明常量的方法。
// 所有的语句必须以分号结束。
enum days {SUN, MON, TUE, WED, THU, FRI, SAT};
// SUN 被赋值为 0, MON 被赋值为 1, TUE 被赋值为 2, 以此类推.

// 枚举的值是可以被指定的
enum days {SUN = 1, MON, TUE, WED = 99, THU, FRI, SAT};
// MON 被自动赋值为 2, TUE 被赋值为 3, 以此类推.
// WED 被赋值为 99, THU 被赋值为 100, FRI 被赋值为 101, 以此类推.

// 使用 #include 导入头文件
#include <stdlib.h>
#include <stdio.h>
#include <string.h>

// 在<尖括号>之间的文件名告诉编译器要在你的系统中寻找
// 库或者头文件
// 对于你自己的头文件，应该使用双引号而不是尖括号，且
// 应该提供路径
#include "my_header.h"      // 本地文件
#include "../my_lib/my_lib_header.h" //相对路径

// 在 .h 文件中提前声明函数签名i或者
// 在你 .c 文件的上方
void function_1();
int function_2(void);

// 至少，你必须在任何函数中使用 "函数原型 "之前声明它。
// 通常情况下，原型被放置在文件的顶部，在任何函数定义之前。
int add_two_ints(int x1, int x2); // function prototype
// 尽管`int add_two_ints(int, int);`也是有效的（不需要给参数命名）。
// 建议在原型中也为参数命名，从而方便检查。

// 如果函数定义在调用该函数的任何其他函数之前
// 那么函数原型就不是必须的。然而，标准的做法是
// 始终将函数原型添加到头文件(*.h)中，然后在头文件中#include该文件。
// 这可以防止在编译器知道一个函数的名字之前，该函数就被调用的问题。
// 除此之外，它为开发者提供了一个干净的头文件
// 从而可以和项目的其他部分共享

// 你的程序的入口是一个 main 函数，它的返回类型可以为任意类型
// 然而，多数操作系统希望它的返回值为 int 类型，从而
// 用于处理错误代码
int main(void) {
  // your program
}

// 用于运行你的程序的命令行参数也被传递给 main 
// argc是参数的数量--你的程序名称算作 1 
// argv是一个字符数组--包含参数本身 
// argv[0] = 你的程序名称，argv[1] = 第一个参数，以此类推
int main (int argc, char** argv)
{
  // 打印输出使用 printf 意思是"格式化打印"
  // %d 代表整数, \n 代表换行
  printf("%d\n", 0); // => 打印 0

  ///////////////////////////////////////
  // 类型
  ///////////////////////////////////////
  // 不符合 C99 标准的编译器要求变量必须在当前块范围的顶部声明
  // 符合 C99 标准的编译器允许在使用数值的地方进行声明
  // 在本教程中，变量在符合 C99 标准的情况下是动态声明的。

  // int型（整型）变量一般占用 4 个字节 (使用`sizeof`运算符可以检查)
  int x_int = 0;

  // short型（短整型）变量一般占用 2 个字节 (使用`sizeof`运算符可以检查)
  short x_short = 0;

  // 字符类型被定义为一个处理器的最小可寻址单位。
  // 通常是 1 个字节, 但在某些系统中它可以更多 (例如，在德州仪器的 TMS320 中它是 2 个字节).
  char x_char = 0;
  char y_char = 'y'; // 字符变量的字面值需要用单引号包住

  // long型（长整型）一般需要 4 个字节到 8 个字节; 而long long型则至少需要保证有 8 个字节（64 位）
  long x_long = 0;
  long long x_long_long = 0;

  // float一般是用 32 位表示的浮点数字
  float x_float = 0.0f; // 'f' suffix here denotes floating point literal

  // double一般是用 64 位表示的浮点数字
  double x_double = 0.0; // real numbers without any suffix are doubles

 // 整数类型也可以有无符号的类型表示。这样这些变量就无法表示负数
// 但是无符号整数所能表示的范围就可以比原来的整数大一些
  unsigned short ux_short;
  unsigned int ux_int;
  unsigned long long ux_long_long;

  // 单引号内的字符是机器的字符集中的整数。
  '0' // => 在 ASCII 字符集中是 48
  'A' // => 在 ASCII 字符集中是 65

  // sizeof(T) 给出了类型为T的变量的大小，单位为字节。
  // sizeof(obj) 产生表达式（变量、字面意义等）的大小。
  printf("%zu\n", sizeof(int)); // => 4 (在多数 4 字节字长的机器上)

  // 如果`sizeof`的参数是一个表达式，那么这个参数不会被演算（VLA例外，见下）
  // 它产生的值是编译时的常量
  int a = 1;
  // size_t是一个无符号整型，表示对象的尺寸，至少 2 个字节
  size_t size = sizeof(a++); // a++ 不会被演算
  printf("sizeof(a++) = %zu where a = %d\n", size, a);
  // 打印 "sizeof(a++) = 4 where a = 1" （在32位架构上）

  // 数组必须被初始化为具体的长度
  char my_char_array[20]; // 这个数组占据 1 * 20 = 20 字节
  int my_int_array[20]; // 这个数组占据 4 * 20 = 80 字节
  // (假设为 4 字节字长)

  // 你可以将一个数组初始化为零:
  char my_array[20] = {0};
  // 其中"{0}"部分被称为 "数组初始化器"。
  // 注意，如果你在同一行中初始化数组
  // 你就可以不明确地声明数组的大小。
  // 所以，下面的声明也是合法的。
  char my_array[] = {0};
  // 但是，然后你必须在运行时评估数组的大小，像这样:
  size_t my_array_size = sizeof(my_array) / sizeof(my_array[0]);
  // 警告 如果你采用这种方法，你应该在开始将数组传给函数之前*评估其大小。
  //你开始将数组传递给函数（见后面的讨论），因为
  // 当数组被传递给函数时，它们会被 "降级 "为原始指针。
  // 所以上面的语句会在函数中产生错误的结果）。
  // 索引数组和其他语言类似 -- 好吧，其实是其他的语言像C
  my_array[0]; // => 0

  // 数组是可变的，其实就是内存的映射！
  my_array[1] = 2;
  printf("%d\n", my_array[1]); // => 2

  // 在C99 （C11中是可选特性），变长数组（VLA）也可以声明长度。
  // 其长度不需要是编译时常量。
  printf("Enter the array size: "); // 询问用户数组长度
  int array_size;
  fscanf(stdin, "%d", &array_size);
  int var_length_array[array_size]; // 声明 VLA
  printf("sizeof array = %zu\n", sizeof var_length_array);

  // 例子。
  // > 输入数组大小：10
  // > sizeof array = 40

  // 字符串只是一个以NULL（0x00）字节为结尾的字符数组。
  // 在字符串中表示为特殊字符'\0'。
  // （我们不需要在字符串字面值中包括 NULL 字节；
  // 编译器会把它插入到数组的末尾）。
  char a_string[20] = "This is a string";
  printf("%s\n", a_string); // %s 可以对字符串进行格式化

  printf("%d\n", a_string[16]); // => 0
  // 即，17号字节为0（18、19和20也是如此）

 // 单引号间的字符是字符字面量
// 它的类型是`int`，而 *不是* `char`
// （由于历史原因）
  int cha = 'a'; // 合法
  char chb = 'a'; // 同样合法 (从 int 到 char 进行了隐式类型转换)

  // 多维数组:
  int multi_array[2][5] = {
    {1, 2, 3, 4, 5},
    {6, 7, 8, 9, 0}
  };
  // 访问元素:
  int array_int = multi_array[0][2]; // => 3

  ///////////////////////////////////////
  // 运算符
  ///////////////////////////////////////

  // 多个变量声明的简写:
  int i1 = 1, i2 = 2;
  float f1 = 1.0, f2 = 2.0;

  int b, c;
  b = c = 0;

  // 算数运算直接了当
  i1 + i2; // => 3
  i2 - i1; // => 1
  i2 * i1; // => 2
  i1 / i2; // => 0 (0.5, 但是截断为 0)

  // 你需要将至少一个整数转换成浮点数，才能得到一个浮点数的结果
  (float)i1 / i2; // => 0.5f
  i1 / (double)i2; // => 0.5 // 双精度浮点也一样
  f1 / f2; // => 0.5, 加上或减去 epsilon

  // 浮点数是由 IEEE 754 标准定义的, 因此无法很好的存储
  // 例如，以下内容不会产生预期的结果 
  //因为0.1在计算机内部可能实际上是0.0999999999，
  //而0.3 可能被存储为0.300000000001。 
  (0.1 + 0.1 + 0.1) != 0.3; // => 1 (true)
  // 并且由于上述原因，它是不符合结合律的
  1 + (1e123 - 1e123) != (1 + 1e123) - 1e123; // => 1 (true)
  // 这种计数法是数字的科学计数法: 1e123 = 1*10^123

  // 值得注意的是，大多数系统都使用IEEE 754来表示浮点。
  // 来表示浮点。即使是用于科学计算的python，也是如此。
  //最终也会调用使用IEEE 754的C语言。这样说并不是为了
  // 表明这是个糟糕的实现，而是作为一个警告
  // 当进行浮点比较时，必须要考虑一点误差（epsilon）。

  // 求余（取模）也在那里，但是如果参数是负的，要小心。
  11 % 3;    // => 2 as 11 = 2 + 3*x (x=3)
  (-11) % 3; // => -2, as one would expect
  11 % (-3); // => 2 and not -2, and it's quite counter intuitive
 
  // 比较运算符或许比较熟悉, 但是
  // C 语言当中没有布尔类型. 我们用整型替代.
  // （C99 引入了 stdbool.h 中提供的_Bool类型）
  // 0 为假，其他任何内容都是真的. 
  //比较运算符的返回值总是为 0 或 1
  3 == 2; // => 0 (false)
  3 != 2; // => 1 (true)
  3 > 2;  // => 1
  3 < 2;  // => 0
  2 <= 2; // => 1
  2 >= 2; // => 1

  // C 不是 Python，连续比较不合法
  // 警告： 下面这一行可以被编译, 但是它表示的是 `(0 < a) < 2`.
  // 该表达式永远为真, 因为 (0 < a) 可能是 1 或 0 中的一个
  // 在本例中为 1，因为 0 小于 1
  int between_0_and_2 = 0 < a < 2;
  // 改用：
  int between_0_and_2 = 0 < a && a < 2;

  // 逻辑运算符适用于整数
  !3; // => 0 (逻辑非)
  !0; // => 1
  1 && 1; // => 1 (逻辑与)
  0 && 1; // => 0
  0 || 1; // => 1 (逻辑或)
  0 || 0; // => 0

  // 三元条件表达式 ( ? : )
  int e = 5;
  int f = 10;
  int z;
  z = (e > f) ? e : f; // => 10 "若 e > f 返回 e, 否则返回 f."

  // 增、减运算符:
  int j = 0;
  int s = j++; // 返回 j 然后增加 j. (s = 0, j = 1)
  s = ++j; // 增加 j 然后返回 j. (s = 2, j = 2)
  // 对于 j-- 和 --j 也一样

  // 位运算符!
  ~0x0F; // => 0xFFFFFFF0 (按位取反, "1 的补码",32 位整数的示例结果)
  0x0F & 0xF0; // => 0x00 (按位与)
  0x0F | 0xF0; // => 0xFF (按位或)
  0x04 ^ 0x0F; // => 0x0B (按位异或)
  0x01 << 1; // => 0x02 (按位左移一位)
  0x02 >> 1; // => 0x01 (按位右移一位)

  // 移动有符号整数时要小心 - 下面这些内容时未定义的:
  // - shifting into the sign bit of a signed integer (int a = 1 << 31)
  // - left-shifting a negative number (int a = -1 << 2)
  // - shifting by an offset which is >= the width of the type of the LHS:
  //   int a = 1 << 32; // UB if int is 32 bits wide

  ///////////////////////////////////////
  // 控制结构
  ///////////////////////////////////////

  if (0) {
    printf("I am never run\n");
  } else if (0) {
    printf("I am also never run\n");
  } else {
    printf("I print\n");
  }

  // While 循环是存在的
  
  int ii = 0;
  while (ii < 10) { //任何小于 10 的值都为真
    printf("%d, ", ii++); // ii++ 在使用其当前值后增加ii
  } // => prints "0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "

  printf("\n");

  int kk = 0;
  do {
    printf("%d, ", kk);
  } while (++kk < 10); // ++kk 在使用其当前值之前增加ii
  // => prints "0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "

  printf("\n");

  // For 循环也一样
  int jj;
  for (jj=0; jj < 10; jj++) {
    printf("%d, ", jj);
  } // => prints "0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "

  printf("\n");

  // *****NOTES*****:
  // 循环和函数必须有一个主体。如果不需要主体。
  int i;
  for (i = 0; i <= 5; i++) {
    ; // 用分号作为主体（空语句）。
  }
  // Or
  for (i = 0; i <= 5; i++);

  // 多选择分支: switch()
  switch (a) {
  case 0: // 标签需要是完整的*常量*表达式（如枚举）。
    printf("Hey, 'a' equals 0!\n");
    break; // if you don't break, control flow falls over labels
  case 1:
    printf("Huh, 'a' equals 1!\n");
    break;
    // Be careful - without a "break", execution continues until the
    // next "break" is reached.
  case 3:
  case 4:
    printf("Look at that.. 'a' is either 3, or 4\n");
    break;
  default:
    // if `some_integral_expression` didn't match any of the labels
    fputs("Error!\n", stderr);
    exit(-1);
    break;
  }
  /*
    在 C 语言中使用 goto
  */
  typedef enum { false, true } bool;
  // 因为在C99以前，布尔类型是不存在的，哭哭 :(
  bool disaster = false;
  int i, j;
  for(i=0; i<100; ++i)
  for(j=0; j<100; ++j)
  {
    if((i + j) >= 150)
        disaster = true;
    if(disaster)
        goto error;  // 两个循环都会被直接跳出
  }
  error: // 这是一个标签（label）你可以通过"goto error;" 跳转到这里
  printf("Error occurred at i = %d & j = %d.\n", i, j);
  /*
    https://ideone.com/GuPhd6
    this will print out "Error occurred at i = 51 & j = 99."
  */
  /*
    一般认为这样做是不好的，除非你真的知道你在做什么。
    见 
    https://en.wikipedia.org/wiki/Spaghetti_code#Meaning
  */

  ///////////////////////////////////////
  // 类型转换
  ///////////////////////////////////////

  // C语言中的每一个值都有其自己的类型，但是你可以把一个值转换为另一个类型
  // 如果你乐意的话 (有一些限制条件).

  int x_hex = 0x01; // 你可以给变量赋值16进制的字面值
                    // 二进制并不在标准中, 但被某些编译器所允许
                    //  (x_bin = 0b0010010110) 

  // 类型之间的转换将试图保持它们的数字值
  printf("%d\n", x_hex); // => Prints 1
  printf("%d\n", (short) x_hex); // => Prints 1
  printf("%d\n", (char) x_hex); // => Prints 1

  // If you assign a value greater than a types max val, it will rollover
  // without warning.
  printf("%d\n", (unsigned char) 257); // => 1 (Max char = 255 if char is 8 bits long)

  // For determining the max value of a `char`, a `signed char` and an `unsigned char`,
  // respectively, use the CHAR_MAX, SCHAR_MAX and UCHAR_MAX macros from <limits.h>

  // Integral types can be cast to floating-point types, and vice-versa.
  printf("%f\n", (double) 100); // %f always formats a double...
  printf("%f\n", (float)  100); // ...even with a float.
  printf("%d\n", (char)100.0);

  ///////////////////////////////////////
  // Pointers
  ///////////////////////////////////////

  // A pointer is a variable declared to store a memory address. Its declaration will
  // also tell you the type of data it points to. You can retrieve the memory address
  // of your variables, then mess with them.

  int x = 0;
  printf("%p\n", (void *)&x); // Use & to retrieve the address of a variable
  // (%p formats an object pointer of type void *)
  // => Prints some address in memory;

  // Pointers start with * in their declaration
  int *px, not_a_pointer; // px is a pointer to an int
  px = &x; // Stores the address of x in px
  printf("%p\n", (void *)px); // => Prints some address in memory
  printf("%zu, %zu\n", sizeof(px), sizeof(not_a_pointer));
  // => Prints "8, 4" on a typical 64-bit system

  // To retrieve the value at the address a pointer is pointing to,
  // put * in front to dereference it.
  // Note: yes, it may be confusing that '*' is used for _both_ declaring a
  // pointer and dereferencing it.
  printf("%d\n", *px); // => Prints 0, the value of x

  // You can also change the value the pointer is pointing to.
  // We'll have to wrap the dereference in parenthesis because
  // ++ has a higher precedence than *.
  (*px)++; // Increment the value px is pointing to by 1
  printf("%d\n", *px); // => Prints 1
  printf("%d\n", x); // => Prints 1

  // Arrays are a good way to allocate a contiguous block of memory
  int x_array[20]; //declares array of size 20 (cannot change size)
  int xx;
  for (xx = 0; xx < 20; xx++) {
    x_array[xx] = 20 - xx;
  } // Initialize x_array to 20, 19, 18,... 2, 1

  // Declare a pointer of type int and initialize it to point to x_array
  int* x_ptr = x_array;
  // x_ptr now points to the first element in the array (the integer 20).
  // This works because arrays often decay into pointers to their first element.
  // For example, when an array is passed to a function or is assigned to a pointer,
  // it decays into (implicitly converted to) a pointer.
  // Exceptions: when the array is the argument of the `&` (address-of) operator:
  int arr[10];
  int (*ptr_to_arr)[10] = &arr; // &arr is NOT of type `int *`!
  // It's of type "pointer to array" (of ten `int`s).
  // or when the array is a string literal used for initializing a char array:
  char otherarr[] = "foobarbazquirk";
  // or when it's the argument of the `sizeof` or `alignof` operator:
  int arraythethird[10];
  int *ptr = arraythethird; // equivalent with int *ptr = &arr[0];
  printf("%zu, %zu\n", sizeof(arraythethird), sizeof(ptr));
  // probably prints "40, 4" or "40, 8"

  // Pointers are incremented and decremented based on their type
  // (this is called pointer arithmetic)
  printf("%d\n", *(x_ptr + 1)); // => Prints 19
  printf("%d\n", x_array[1]); // => Prints 19

  // You can also dynamically allocate contiguous blocks of memory with the
  // standard library function malloc, which takes one argument of type size_t
  // representing the number of bytes to allocate (usually from the heap, although this
  // may not be true on e.g. embedded systems - the C standard says nothing about it).
  int *my_ptr = malloc(sizeof(*my_ptr) * 20);
  for (xx = 0; xx < 20; xx++) {
    *(my_ptr + xx) = 20 - xx; // my_ptr[xx] = 20-xx
  } // Initialize memory to 20, 19, 18, 17... 2, 1 (as ints)

  // Be careful passing user-provided values to malloc! If you want
  // to be safe, you can use calloc instead (which, unlike malloc, also zeros out the memory)
  int* my_other_ptr = calloc(20, sizeof(int));

  // Note that there is no standard way to get the length of a
  // dynamically allocated array in C. Because of this, if your arrays are
  // going to be passed around your program a lot, you need another variable
  // to keep track of the number of elements (size) of an array. See the
  // functions section for more info.
  size_t size = 10;
  int *my_arr = calloc(size, sizeof(int));
  // Add an element to the array
  size++;
  my_arr = realloc(my_arr, sizeof(int) * size);
  if (my_arr == NULL) {
    //Remember to check for realloc failure!
    return
  }
  my_arr[10] = 5;

  // Dereferencing memory that you haven't allocated gives
  // "unpredictable results" - the program is said to invoke "undefined behavior"
  printf("%d\n", *(my_ptr + 21)); // => Prints who-knows-what? It may even crash.

  // When you're done with a malloc'd block of memory, you need to free it,
  // or else no one else can use it until your program terminates
  // (this is called a "memory leak"):
  free(my_ptr);

  // Strings are arrays of char, but they are usually represented as a
  // pointer-to-char (which is a pointer to the first element of the array).
  // It's good practice to use `const char *' when referring to a string literal,
  // since string literals shall not be modified (i.e. "foo"[0] = 'a' is ILLEGAL.)
  const char *my_str = "This is my very own string literal";
  printf("%c\n", *my_str); // => 'T'

  // This is not the case if the string is an array
  // (potentially initialized with a string literal)
  // that resides in writable memory, as in:
  char foo[] = "foo";
  foo[0] = 'a'; // this is legal, foo now contains "aoo"

  function_1();
} // end main function

///////////////////////////////////////
// Functions
///////////////////////////////////////

// Function declaration syntax:
// <return type> <function name>(<args>)

int add_two_ints(int x1, int x2)
{
  return x1 + x2; // Use return to return a value
}

/*
Functions are call by value. When a function is called, the arguments passed to
the function are copies of the original arguments (except arrays). Anything you
do to the arguments in the function do not change the value of the original
argument where the function was called.

Use pointers if you need to edit the original argument values.

Example: in-place string reversal
*/

// A void function returns no value
void str_reverse(char *str_in)
{
  char tmp;
  size_t ii = 0;
  size_t len = strlen(str_in); // `strlen()` is part of the c standard library
                               // NOTE: length returned by `strlen` DOESN'T include the
                               //       terminating NULL byte ('\0')
  for (ii = 0; ii < len / 2; ii++) { // in C99 you can directly declare type of `ii` here
    tmp = str_in[ii];
    str_in[ii] = str_in[len - ii - 1]; // ii-th char from end
    str_in[len - ii - 1] = tmp;
  }
}
//NOTE: string.h header file needs to be included to use strlen()

/*
char c[] = "This is a test.";
str_reverse(c);
printf("%s\n", c); // => ".tset a si sihT"
*/
/*
as we can return only one variable
to change values of more than one variables we use call by reference
*/
void swapTwoNumbers(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
/*
int first = 10;
int second = 20;
printf("first: %d\nsecond: %d\n", first, second);
swapTwoNumbers(&first, &second);
printf("first: %d\nsecond: %d\n", first, second);
// values will be swapped
*/

// Return multiple values. 
// C does not allow for returning multiple values with the return statement. If
// you would like to return multiple values, then the caller must pass in the
// variables where they would like the returned values to go. These variables must
// be passed in as pointers such that the function can modify them.
int return_multiple( int *array_of_3, int *ret1, int *ret2, int *ret3)
{
    if(array_of_3 == NULL)
        return 0; //return error code (false)

    //de-reference the pointer so we modify its value
   *ret1 = array_of_3[0]; 
   *ret2 = array_of_3[1]; 
   *ret3 = array_of_3[2]; 

   return 1; //return error code (true)
}

/*
With regards to arrays, they will always be passed to functions
as pointers. Even if you statically allocate an array like `arr[10]`,
it still gets passed as a pointer to the first element in any function calls.
Again, there is no standard way to get the size of a dynamically allocated
array in C.
*/
// Size must be passed!
// Otherwise, this function has no way of knowing how big the array is.
void printIntArray(int *arr, size_t size) {
    int i;
    for (i = 0; i < size; i++) {
        printf("arr[%d] is: %d\n", i, arr[i]);
    }
}
/*
int my_arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
int size = 10;
printIntArray(my_arr, size);
// will print "arr[0] is: 1" etc
*/

// if referring to external variables outside function, you should use the extern keyword.
int i = 0;
void testFunc() {
  extern int i; //i here is now using external variable i
}

// make external variables private to source file with static:
static int j = 0; //other files using testFunc2() cannot access variable j
void testFunc2() {
  extern int j;
}
// The static keyword makes a variable inaccessible to code outside the
// compilation unit. (On almost all systems, a "compilation unit" is a .c
// file.) static can apply both to global (to the compilation unit) variables,
// functions, and function-local variables. When using static with
// function-local variables, the variable is effectively global and retains its
// value across function calls, but is only accessible within the function it
// is declared in. Additionally, static variables are initialized to 0 if not
// declared with some other starting value.
//**You may also declare functions as static to make them private**

///////////////////////////////////////
// User-defined types and structs
///////////////////////////////////////

// Typedefs can be used to create type aliases
typedef int my_type;
my_type my_type_var = 0;

// Structs are just collections of data, the members are allocated sequentially,
// in the order they are written:
struct rectangle {
  int width;
  int height;
};

// It's not generally true that
// sizeof(struct rectangle) == sizeof(int) + sizeof(int)
// due to potential padding between the structure members (this is for alignment
// reasons). [1]

void function_1()
{
  struct rectangle my_rec;

  // Access struct members with .
  my_rec.width = 10;
  my_rec.height = 20;

  // You can declare pointers to structs
  struct rectangle *my_rec_ptr = &my_rec;

  // Use dereferencing to set struct pointer members...
  (*my_rec_ptr).width = 30;

  // ... or even better: prefer the -> shorthand for the sake of readability
  my_rec_ptr->height = 10; // Same as (*my_rec_ptr).height = 10;
}

// You can apply a typedef to a struct for convenience
typedef struct rectangle rect;

int area(rect r)
{
  return r.width * r.height;
}

// if you have large structs, you can pass them "by pointer" to avoid copying
// the whole struct:
int areaptr(const rect *r)
{
  return r->width * r->height;
}

///////////////////////////////////////
// Function pointers
///////////////////////////////////////
/*
At run time, functions are located at known memory addresses. Function pointers are
much like any other pointer (they just store a memory address), but can be used
to invoke functions directly, and to pass handlers (or callback functions) around.
However, definition syntax may be initially confusing.

Example: use str_reverse from a pointer
*/
void str_reverse_through_pointer(char *str_in) {
  // Define a function pointer variable, named f.
  void (*f)(char *); // Signature should exactly match the target function.
  f = &str_reverse; // Assign the address for the actual function (determined at run time)
  // f = str_reverse; would work as well - functions decay into pointers, similar to arrays
  (*f)(str_in); // Just calling the function through the pointer
  // f(str_in); // That's an alternative but equally valid syntax for calling it.
}

/*
As long as function signatures match, you can assign any function to the same pointer.
Function pointers are usually typedef'd for simplicity and readability, as follows:
*/

typedef void (*my_fnp_type)(char *);

// Then used when declaring the actual pointer variable:
// ...
// my_fnp_type f;


/////////////////////////////
// Printing characters with printf()
/////////////////////////////

//Special characters:
/*
'\a'; // alert (bell) character
'\n'; // newline character
'\t'; // tab character (left justifies text)
'\v'; // vertical tab
'\f'; // new page (form feed)
'\r'; // carriage return
'\b'; // backspace character
'\0'; // NULL character. Usually put at end of strings in C.
//   hello\n\0. \0 used by convention to mark end of string.
'\\'; // backslash
'\?'; // question mark
'\''; // single quote
'\"'; // double quote
'\xhh'; // hexadecimal number. Example: '\xb' = vertical tab character
'\0oo'; // octal number. Example: '\013' = vertical tab character

//print formatting:
"%d";    // integer
"%3d";   // integer with minimum of length 3 digits (right justifies text)
"%s";    // string
"%f";    // float
"%ld";   // long
"%3.2f"; // minimum 3 digits left and 2 digits right decimal float
"%7.4s"; // (can do with strings too)
"%c";    // char
"%p";    // pointer. NOTE: need to (void *)-cast the pointer, before passing
         //                it as an argument to `printf`.
"%x";    // hexadecimal
"%o";    // octal
"%%";    // prints %
*/

///////////////////////////////////////
// Order of Evaluation
///////////////////////////////////////

// From top to bottom, top has higher precedence
//---------------------------------------------------//
//        Operators                  | Associativity //
//---------------------------------------------------//
// () [] -> .                        | left to right //
// ! ~ ++ -- + = *(type) sizeof      | right to left //
// * / %                             | left to right //
// + -                               | left to right //
// << >>                             | left to right //
// < <= > >=                         | left to right //
// == !=                             | left to right //
// &                                 | left to right //
// ^                                 | left to right //
// |                                 | left to right //
// &&                                | left to right //
// ||                                | left to right //
// ?:                                | right to left //
// = += -= *= /= %= &= ^= |= <<= >>= | right to left //
// ,                                 | left to right //
//---------------------------------------------------//

/******************************* Header Files **********************************

Header files are an important part of C as they allow for the connection of C
source files and can simplify code and definitions by separating them into
separate files.

Header files are syntactically similar to C source files but reside in ".h"
files. They can be included in your C source file by using the precompiler
command #include "example.h", given that example.h exists in the same directory
as the C file.
*/

/* A safe guard to prevent the header from being defined too many times. This */
/* happens in the case of circle dependency, the contents of the header is    */
/* already defined.                                                           */
#ifndef EXAMPLE_H /* if EXAMPLE_H is not yet defined. */
#define EXAMPLE_H /* Define the macro EXAMPLE_H. */

/* Other headers can be included in headers and therefore transitively */
/* included into files that include this header.                       */
#include <string.h>

/* Like for c source files, macros can be defined in headers */
/* and used in files that include this header file.          */
#define EXAMPLE_NAME "Dennis Ritchie"

/* Function macros can also be defined.  */
#define ADD(a, b) ((a) + (b))

/* Notice the parenthesis surrounding the arguments -- this is important to   */
/* ensure that a and b don't get expanded in an unexpected way (e.g. consider */
/* MUL(x, y) (x * y); MUL(1 + 2, 3) would expand to (1 + 2 * 3), yielding an  */
/* incorrect result)                                                          */

/* Structs and typedefs can be used for consistency between files. */
typedef struct Node
{
    int val;
    struct Node *next;
} Node;

/* So can enumerations. */
enum traffic_light_state {GREEN, YELLOW, RED};

/* Function prototypes can also be defined here for use in multiple files,  */
/* but it is bad practice to define the function in the header. Definitions */
/* should instead be put in a C file.                                       */
Node createLinkedList(int *vals, int len);

/* Beyond the above elements, other definitions should be left to a C source */
/* file. Excessive includes or definitions should, also not be contained in */
/* a header file but instead put into separate headers or a C file.          */

#endif /* End of the if precompiler directive. */


```