.. highlight:: cl
   :linenothreshold: 0

Chapter 12 结构 (Structure)
**************************************************

3.3 节中介绍了 Lisp 如何使用指针允许我们将任何值放到任何地方。这种说法是完全有可能的，但这并不一定都是好事。

例如，一个对象可以是自身的元素。这样是好还是坏，要看它是程序员有意设计的还是无心这样写的。

12.1 共享结构 (Shared Structure)
==================================

多个列表可以共享 conse 。在最简单的情况下，一个列表可能是另一个列表的一部分。如

::

	> (setf part (list 'b 'c))
	(B C)
	> (setf whole (cons 'a part))
	(A B C) 

其中，第一个 ``cons`` 是第二个 ``cons`` 的一部分（事实上，是的第二个 ``cons`` 的 ``cdr`` ）。在这样的情况下，我们说，这两个列表共享结构。这两个列表的基本结构见图 12.1 所示。

用 ``tailp`` 函数来检测这种情况。将两个列表作为它的输入参数，如果第一个列表是第二个列表的一部分时，则返回T ：

::

	> (tailp part whole)
	T

我们可以想像它写成：

::

	(defun our-tailp (x y )
	(or (eql x  y )
	(and (consp y)
	(our-tailp x (cdr y)))))

定义表明，每个列表本身是一个尾巴， ``nil`` 是每一个适当的列表的尾部。

在更复杂的情况下，两个列表可以共享没有任何一个其他的尾巴结构。这种情况发生时，他们都有一个共同的尾巴，如图 12.2 所示。我们可以构建这种情况如下：

::

	(setf part (list 'b 'c)
	whole1 (cons 1 part )
	whole2 (cons 2 part)) 

现在 ``whole1`` 和 ``whole2`` 共享结构，但是它们彼此都不是对方的一部分。 

12.2 Modification
==================================================

12.3 Example: Queues
================================

12.4 Destructive Functions
===================================================

12.5 Example: Binary Search
=======================================

12.6 Example: Doubly-Linked Lists
=======================================

12.7 Circular Structure
==================================================

12.8 Constant Structure
=======================================

Chapter 12 总结 (Summary)
============================

Chapter 12 练习 (Exercises)
==================================
