---
title: 《Java解惑》读书笔记
description: <blockquote class="blockquote-center">本片文章主要记录《Java解惑》的一些收获。</blockquote>
date: 2017-03-06 16:50:16
tags: [java解惑,表达式]
categories: Java解惑
keywords: java解惑,java表达式
---

## 表达式之谜

### 奇数性
奇数：被2整除余1的数。表达式i%2是计算i除以2时所产生的余数。这个表达式其实是错误的。
在所有的int数值中，有一半的值为负数，当值为负数时，无论该值为奇数还是偶数，结果都会返回false。
```java
package com.hx.test;
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println(isOdd(-5));
	}

	public static boolean isOdd(int i) {
//		return i % 2 == 1;  // 这个表达式是错误的。
//		return i % 2 != 0; // 正确
		return (i & 1) != 0; // 正确
	}
}
```

### 找零时刻
```java
package com.hx.test;

import java.math.BigDecimal;

public class HelloWorld {
	public static void main(String[] args) {
		System.out.println(2.00 - 1.10);  // 输出结果0.8999999999999999
		System.out.println((200-110)+"cents"); //输出结果 90 cents
		System.out.println(new BigDecimal("2.00").subtract(new BigDecimal("1.10"))); //输出结果0.9
	}
}
```
在需要使用精确数值的地方，要避免使用`float`和`double`，对于货币计算，要使用`int`,`long`,`BigDecimal`。

### 长整除
```java
package com.hx.test;

import java.math.BigDecimal;

public class HelloWorld {
	public static void main(String[] args) {
		
		final long MICROS_PRE_DAY = 24*60*60*1000*1000;
		final long MILLS_PRE_DAY = 24*60*60*1000;
		
		//final long MICROS_PRE_DAY = 24L*60*60*1000*1000;
		//final long MILLS_PRE_DAY = 24L*60*60*1000;
		
		System.out.println(MICROS_PRE_DAY/MILLS_PRE_DAY); // 为什么结果会打印5？？？
		
		// 
	}
}
```
当操作很大的数字时，千万要提防溢出。即便用来保存结果的变量足够大，也并不意味着要产生结果的计算具有正确的类型。当拿不准的时候，就使用`long`运算来执行整个计算。

### 十六进制的趣事
```java
package com.hx.test;

public class HelloWorld {
	public static void main(String[] args) {
		System.out.println(Long.toHexString(0x100000000L + 0xcafebabe));  // cafebabe
		System.out.println(Long.toHexString(0x100000000L + 0xcafebabeL)); // 1cafebabe
	}

}
```
混合类型的计算可能产生混淆，尤其需要注意的是十六进制和八进制字面常量无需显式的减号符号就可以表示负的数值，为了避免这种窘境，通常最好避免混合类型的计算。