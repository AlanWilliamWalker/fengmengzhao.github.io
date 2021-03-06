---
layout: post
title: 计算机字符编码
---

UTF-8字符编码

1. ASCII(American Standard Code for Information Interchange，美国标准信息交换代码),上个世纪六十年代，美国制定了一套字符编码，对英语字符和二进制之间的关系，做了统一的规定，称为ASCII码，一直沿用至今。
ASCII是单字节编码，字节的首位规定是0，只是用后面7位表示，共有128个字符编码，0~31是控制字符(如换行、回车等)，32~127是打印字符，可以通过键盘输出并且能够显示出来
2. ISO-8859-1,是ASCII的扩展，它仍然是单字节编码，涵盖了大多数西欧语言字符，使用8位表示，共有256个字符
3. GB2312，它的全称是《信息交换用汉字编码字符集 基本集》，它是双字节编码，总的编码范围是 A1-F7，其中从 A1-A9 是符号区，总共包含 682 个符号，从 B0-F7 是汉字区，包含 6763 个汉字
4. GBK，全称叫《汉字内码扩展规范》，是国家技术监督局为 windows95 所制定的新的汉字内码规范，它的出现是为了扩展 GB2312，加入更多的汉字，它的编码范围是 8140~FEFE（去掉 XX7F）总共有 23940 个码位，它能表示 21003 个汉字，它的编码是和 GB2312 兼容的，也就是说用 GB2312 编码的汉字可以用 GBK 来解码，并且不会有乱码
5. utf-16,说到 UTF 必须要提到 Unicode（Universal Code 统一码），ISO 试图想创建一个全新的超语言字典，世界上所有的语言都可以通过这本字典来相互翻译。可想而知这个字典是多么的复杂，关于 Unicode 的详细规范可以参考相应文档。Unicode 是 Java 和 XML 的基础，下面详细介绍 Unicode 在计算机中的存储形式。UTF-16 具体定义了 Unicode 字符在计算机中存取方法。UTF-16 用两个字节来表示 Unicode 转化格式，这个是定长的表示方法，不论什么字符都可以用两个字节表示，两个字节是 16 个 bit，所以叫 UTF-16。UTF-16 表示字符非常方便，每两个字节表示一个字符，这个在字符串操作时就大大简化了操作，这也是 Java 以 UTF-16 作为内存的字符存储格式的一个很重要的原因。
6. utf-8, UTF-16 统一采用两个字节表示一个字符，虽然在表示上非常简单方便，但是也有其缺点，有很大一部分字符用一个字节就可以表示的现在要两个字节表示，存储空间放大了一倍，在现在的网络带宽还非常有限的今天，这样会增大网络传输的流量，而且也没必要。而 UTF-8 采用了一种变长技术，每个编码区域有不同的字码长度。不同类型的字符可以是由 1~6 个字节组成。
7. ANSI编码一般指Windows-1252编码，是一个256个字符的字集的编码，每个字符由一个字节表示。其中前128个字符(00-7F)和ASCII的7bits编码一样，后128个字符中有一些欧洲国家用的有重音的字符。ANSI编码在不同语言的Windows下也指此语言下的Windows编码页，比如中文环境下指Windows-936(也就是GB2312)，日文环境下是Windows-932(JIS)编码等等，也是前128个字符(00-7F)和ASCII的7bits编码一样，其他字符则由2个字节表示。

UTF-8是针对Unicode的可变长度字符编码，一个字符可以由1到4个字节表示，其中由一个字节表示的字符和ASCII的7bits编码一样，而包括中文在内的大部分字符则由3个字节表示。

所以如果文本里只有ASCII的7bits编码的那些，这两种编码是互相兼容没有区别的，但是对其他字符，编码就不同了，而且Windows-1252编码无法表达除了256个字符外的比如中文字符，其他的ANSI编码如Windows-936也只能表示一部分Unicode中的字符。编码格式的不同导致程序无法运行很容易理解，因为同样的字集在不同的编码方式下表达的字符是不同的或者是不能被表示的，除非是ASCII的7bits编码中的那些字符。

> UTF-8 有以下编码规则：<br>
- 如果一个字节，最高位（第 8 位）为 0，表示这是一个 ASCII 字符（00 - 7F）。可见，所有 ASCII 编码已经是 UTF-8 了。
- 如果一个字节，以 11 开头，连续的 1 的个数暗示这个字符的字节数，例如：110xxxxx 代表它是双字节 UTF-8 字符的首字节。
- 如果一个字节，以 10 开始，表示它不是首字节，需要向前查找才能得到当前字符的首字节。
