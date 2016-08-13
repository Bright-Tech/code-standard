基本编码规范 - PHP
=====================

制订编码规范的目的是在多人协作时，能够更好的共享代码，确保每个人在更新和集成代码时更加方便，同时使多人的代码在同一环境下表现一致。
我们使用通用的 [PSR][PSR] 规范来进行代码规范，如果本编码规范和[PSR][PSR]规范相冲突，请及时告知，谢谢。<br/>

* 文中使用“必须”说明的条目意味着此条目为绝对性要求，必须符合。
* 文中使用“应当”说明的条目意味着此条目为推荐性要求，特定的情况下有可能正当的理由忽略此条目，但当你选择另一种方式时必须经过了解和仔细权衡。

[PSR]: https://github.com/php-fig/fig-standards/tree/master/accepted
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[驼峰命名法]:http://baike.baidu.com/link?url=OTIuT_UfbS7mRun5wnkY2kvnBLQiLgmFXfun1TYgWn9TujDw1ot0TbkrpbUSVjBfZ232v9UpvsXADIvMe2XL0FmuvbuVNQIyrLry0C3oOr-UzV9EUTXCzRIJvUvl_q4EAvxeox6MmRVPt9MOubRvzjgQqmAD-XFFdkFEW7cpl2dVUpnF9zwUlab7F0DUCMjm

1. 总体要求
-----------
- 文件必须只能使用 `<?php` and `<?=` 标签, 不允许使用短标签 '<? ?>'。
- 文件必须只能使用 UTF-8 without BOM 编码。
- 文件应该进行声明（类、函数、常量等）或实现某些功能（例如生成，输出，改变ini设置等），但不应都做。
- 命名空间和类名必须遵守[PSR-4][PSR-4]。
- 类名必须使用[驼峰命名法][驼峰命名法]命名，每个单词首字母大写，例如 `StudlyCaps`。
- 类中的常量必须全部使用大写，并使用_(下划线)作为单词之间的分割符， 例如 'CONSTANTS_NAME'。
- 方法名必须使用[驼峰命名法][驼峰命名法]命名，第一个单词的首字母要小写，例如 `camelCase`。
- 使用4个空格代替Tab。
- 去掉行尾空格。

2. 文件
--------

### 2.1. PHP Tags

PHP代码必须使用长标记`<?php ?>` 或短标记 `<?= ?>`。必须不能使用其他的PHP标记

### 2.2. 字符编码

PHP代码必须只能使用 UTF-8 without BOM 编码.

### 2.3. 单功能原则

一个文件应当只声明新符号(类、函数、常量等), 不会产生副作用; 或者应当执行逻辑，产生副作用，但是不应当两者都做。

"产生副作用" 意味着执行逻辑并不直接关联到声明类、函数、常量等，


"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

    ~~~php
    <?php
    // side effect: change ini settings
    ini_set('error_reporting', E_ALL);

    // side effect: loads a file
    include "file.php";

    // side effect: generates output
    echo "<html>\n";

    // declaration
    function foo()
    {
        // function body
    }
    ~~~

    The following example is of a file that contains declarations without side
    effects; i.e., an example of what to emulate:

    ~~~php
    <?php
    // declaration
    function foo()
    {
        // function body
    }

    // conditional declaration is *not* a side effect
    if (! function_exists('bar')) {
        function bar()
        {
            // function body
        }
    }
    ~~~

- 对于只包含有 PHP 代码的文件，结束标志（"?>"）是不允许存在的，PHP自身不需要（"?>"）。
- PHP文件必须只使用 UTF-8 without BOM 编码。
- 只能在View层执行输出，不能在Controller和Model层执行输出。

3. 命名空间和类名
--------
- Namespaces and classes MUST follow [PSR-0][].
- 每个Class都定义在自己独立的文件中
- 类名必须使用驼峰命名法命名， 例如 `StudlyCaps`。
- 使用5.3及以上PHP编码必须使用正式的命名空间

4. Class Constants, Properties, and Methods
-------------------------------------------




命名约定 - 函数和方法

函数名只包含字母数字字符，下划线是不允许的。数字是允许的但大多数情况下不鼓励。
函数名总是以小写开头，当函数名包含多个单词，每个子的首字母必须大写，这就是所谓的 “驼峰” 格式。
我们一般鼓励使用冗长的名字，函数名应当长到足以说明函数的意图和行为。

这些是可接受的函数名的例子： 

filterInput()
getElementById()
widgetFactory()
 

对于面向对象编程，实例或静态变量的访问器总是以 "get" 或 "set" 为前缀。
在设计模式实现方面，如单态模式（singleton）或工厂模式（factory）， 方法的名字应当包含模式的名字，这样名字更能描述整个行为。
在对象中的方法，声明为 "private" 或 "protected" 的， 名称的首字符必须是一个单个的下划线，这是唯一的下划线在方法名字中的用法。
声明为 "public" 的从不包含下划线。
全局函数 (如："floating functions") 允许但不鼓励，建议把这类函数封装到静态类里。


命名约定 - 变量
变量只包含数字字母字符，大多数情况下不鼓励使用数字，下划线不接受。
声明为 "private" 或 "protected" 的实例变量名必须以一个单个下划线开头，这是唯一的下划线在程序中的用法，声明为 "public" 的不应当以下划线开头。
对函数名（见上面 3.3 节）一样，变量名总以小写字母开头并遵循“驼峰式”命名约定。
我们一般鼓励使用冗长的名字，这样容易理解代码，开发者知道把数据存到哪里。除非在小循环里，不鼓励使用简洁的名字如 "$i" 和 "$n" 。如果一个循环超过 20 行代码，索引的变量名必须有个具有描述意义的名字。



命名约定 - 常量
常量包含数字字母字符和下划线，数字允许作为常量名。
常量名的所有字母必须大写。
常量中的单词必须以下划线分隔，例如可以这样 EMBED_SUPPRESS_EMBED_EXCEPTION 但不许这样 EMBED_SUPPRESSEMBEDEXCEPTION。
常量必须通过 "const" 定义为类的成员，强烈不鼓励使用 "define" 定义的全局常量。



编码风格 - PHP 代码划分
PHP 代码总是用完整的标准的 PHP 标签定界：
<?php

?>


短标签

<? 
?>


是不允许的，只包含 PHP 代码的文件，不要结束标签。


编码风格 - 字符串文字
当字符串是文字(不包含变量)，应当用单引号（ apostrophe ）来括起来：

$a = 'Example String';


编码风格 - 包含单引号（'）的字符串文字
当文字字符串包含单引号（apostrophe ）就用双引号括起来，特别在 SQL 语句中有用：

$sql = "SELECT `id`, `name` from `people` WHERE `name`='Fred' OR `name`='Susan'";


在转义单引号时，上述语法是首选的，因为很容易阅读。 


编码风格 - 变量替换
变量替换有下面这些形式：
$greeting = "Hello $name, welcome back!";

$greeting = "Hello {$name}, welcome back!";
                    
为保持一致，这个形式不允许：
$greeting = "Hello ${name}, welcome back!";
                    
编码风格 - 字符串连接
字符串必需用 "." 操作符连接，在它的前后加上空格以提高可读性：
$company = 'Zend' . ' ' . 'Technologies';
                    
当用 "." 操作符连接字符串，鼓励把代码可以分成多个行，也是为提高可读性。在这些例子中，每个连续的行应当由 whitespace 来填补，例如 "." 和 "=" 对齐：
$sql = "SELECT `id`, `name` FROM `people` "
     . "WHERE `name` = 'Susan' "
     . "ORDER BY `name` ASC ";
编码风格 - 数字索引数组
索引不能为负数
建议数组索引从 0 开始


编码风格 - 类的声明
用命名约定来命名类。
每个类必须有一个符合 PHPDocumentor 标准 的文档块。
每个 PHP 文件中只有一个类。

下面是个可接受的类的例子：

/**
 * Documentation Block Here
 */
class SampleClass
{
    // 类的所有内容
    // 必需缩进四个空格
}
                    

编码风格 - 类成员变量
必须用变量名约定来命名类成员变量。                     
变量的声明必须在类的顶部，在方法的上方声明。                     
不允许使用 var ，要用 private、 protected 或 public。
编码风格 - 函数和方法声明
必须用函数名约定来命名函数。
在类中的函数必须用 private、 protected 或 public 声明它们的可见性。
象类一样，花括号从函数名的下一行开始。
函数名和括参数的圆括号中间没有空格。
强烈反对使用全局函数。
下面是可接受的在类中的函数声明的例子：
/**
 * Documentation Block Here
 */
class Foo
{
    /**
     * Documentation Block Here
     */
    public function bar()
    {
        // 函数的所有内容
        // 必需缩进四个空格
    }
}
                    

返回值不能在圆括号中。
/**
 * Documentation Block Here
 */
class Foo
{
    /**
     * WRONG
     */
    public function bar()
    {
        return($this->bar);
    }

    /**
     * RIGHT
     */
    public function bar()
    {
        return $this->bar;
    }
}
                    
编码风格 - 函数和方法的用法
严格禁止对没有被声明为 static 的方法， 使用  类似 $foo::bar() 的调用方式。
编码风格 - 控制语句 - if/Else/Elseif
使用 if and elseif 的控制语句在条件语句的圆括号前后都必须有一个空格。
在圆括号里的条件语句，操作符必须用空格分开，鼓励使用多重圆括号以提高在复杂的条件中划分逻辑组合。
前花括号必须和条件语句在同一行，后花括号单独在最后一行，其中的内容用四个空格缩进。
if ($a != 2) {
    $a = 2;
}
                    
对包括"elseif" 或 "else"的 "if" 语句，和 "if" 结构的格式类似， 下面的例子示例 "if" 语句， 包括 "elseif" 或 "else" 的格式约定：
if ($a != 2) {
    $a = 2;
} else {
    $a = 7;
}


if ($a != 2) {
    $a = 2;
} elseif ($a == 3) {
    $a = 4;
} else {
    $a = 7;
}
                    
在有些情况下， PHP 允许这些语句不用花括号，但在代码标准里，它们（"if"、 "elseif" 或 "else" 语句）必须使用花括号。"elseif" 是允许的但强烈不鼓励，我们支持 "else if" 组合。
编码风格 - 控制语句 - Switch
在 "switch" 结构里的控制语句在条件语句的圆括号前后必须都有一个单个的空格。
"switch" 里的代码必须有四个空格缩进，在"case"里的代码再缩进四个空格。
switch ($numPeople) {
    case 1:
        break;

    case 2:
        break;

    default:
        break;
}
                
switch 语句应当有 default。
注： 有时候，在 falls through 到下个 case 的 case 语句中不写 break or return 很有用。 为了区别于 bug，任何 case 语句中，所有不写 break or return 的地方应当有一个 "// break intentionally omitted" 这样的注释来表明 break 是故意忽略的。

编码风格 - 注释文档格式
代码中不能出现中文注释。


所有文档块 ("docblocks") 必须和 phpDocumentor 格式兼容，phpDocumentor 格式的描述超出了本文档的范围，关于它的详情，参考：» http://phpdoc.org/。
在每个类的顶部放置一个 "class-level" 的 docblock。下面是一些例子：
类
每个类必须至少包含这些 phpDocumentor 标签：
/**
 * 类的简述
 *
 * 类的详细描述 （如果有的话）... ...
 *
 * @version    Release: @package_version@
 * @since      Class available since Release 1.5.0
 * @deprecated Class deprecated in Release 2.0.0
 */
                    
函数
每个函数，包括对象方法，必须有最少包含下列内容的文档块（docblock）：

    * 函数的描述

    * 所有参数

    * 所有可能的返回值

    * 制作人

    * 版本


因为访问级已经通过 "public"、 "private" 或 "protected" 声明， 不需要使用 "@access"。

/**
 * 函数的描述
 *
 * @param      参数的描述
 * @return     返回值的描述
 * @author     Sam Xiao
 * @since      1.5.0
 * @deprecated 2.0.0
 */
如果函数/方法抛出一个异常，使用 @throws 于所有已知的异常类：
@throws exceptionclass [description]
                    
如果 函数/方法 代码量超过25行,也要写明注释。
函数/方法 内的注释要求写明目的，即为什么需要下面这段代码，而不是代码逻辑的简单复述
/**
 *   GOOD
 *   Refoud User's Order
 **/



/**
 *   BAD
 *   Update data into database
 **/

IDE
---------------
强烈推荐使用 Zend Studio 的 Code Format 功能格式化代码。 快捷键为 ( Ctrl + Shift + F );<br>
导入方式 ( 在 Window -> Preferences -> PHP -> Code Style -> Formatter 中点击 Import)

Zend Studio 中的 文件编码格式 需要被设定为 UTF-8( 在 Window -> Preferences -> General -> Workspace 修改 Text File Encoding 为 UTF-8 );<br>
Zend Studio中增加自动删除行尾空格的方法为Window -> Preferences -> PHP -> Editor ->Save Actions
