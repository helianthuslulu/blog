gcc 4.6 加了两个warning 

当程序中出现已经赋值的但并未使用过的变量时，GCC会触发 -Wunused-but-set-variable 的警告；当程序中某个函数参数没有在函数中使用过时，GCC会触发 -Wunused-but-set-parameter 警告。这两个警告可以用 -Wall 和 -Wextra 触发。

有时候开发者需要在调试过程中定义一些虽已赋值，但并不使用的变量，或者定义一些在后续版本中要使用到的函数参数。可又不能不用 -Wall -Wextra 这两个选项来编译

使用 __attribute__ ((unused)) 避免上述__attribute__ ((unused)) a

例如   __attribute__ ((unused)) a  则a 可以定义但是不使用 或者 参数但是不使用
