---
layout: post
title:  "Tree Traversal by Guava"
date:   2016-02-17 23:07:00 +0800
categories: algorithms
tags: [algorithms,tree-traversal,guava]
---

非本科的關係 , 對於演算法並沒有那麼熟悉 , 但電腦科學的東西寫久了 , 總是會遇到演算法的問題 , 因為是基礎.
工作or現實的關係 , 常在處理樹狀結構資料 , 但每當要針對樹狀資料進行迭代處理時 , 常常都是透過遞迴處理.

用遞迴寫的缺點.

* 迭代處理如果過程稍微不一樣的話 , 就需要另寫遞迴 , 之後就常常見到一堆很像但細節不太一樣的遞迴.

工作過程一直覺得展出資料及組回樹狀資料應該可以更normalize.後來就在Guava上看到有現成的Tree Traversal Library, 試用了一下覺得很不錯.

----

下面為範例

使用Guava進行迭代的話 , 需要先在Class宣告一個TreeTraverser物件

~~~ java

private static final TreeTraverser<Tree> ADAPTER = new TreeTraverser<Tree>() {
        @Override
        public Iterable<Tree> children(Tree node) {
            return node.getChildren();
        }
    };

~~~

實際迭代的時候只有一行即可將樹狀物件轉成List結構.
Guava提供三種的迭代方式 , 下面用的是preOrder.

~~~ java

Tree root = new Tree('h');
Tree d = new Tree('d', root);
Tree a = new Tree('a', d);
Tree b = new Tree('b', d);
Tree c = new Tree('c', d);
Tree e = new Tree('e', root);
Tree g = new Tree('g', root);
Tree f = new Tree('f', g);

List<Tree> treeList = ADAPTER.preOrderTraversal(root).toList();

~~~

Tree Class

~~~ java
@Data
@ToString(of = "value")
public final class Tree {

    private char value;
    private List<Tree> children = new ArrayList<>();
    private Tree parent;

    public Tree(char value, Tree parent) {
        this.value = value;
        setParent(parent);
    }

    public Tree(char value) {
        this.value = value;
    }

    public void setParent(Tree parent) {
        parent.setChildren(FluentIterable.from(parent.getChildren()).append(this).toList());
        this.parent = parent;
    }

}
~~~

UnitTest  , 大部分都都是參考Guava原生的UnitTest

~~~ java

@Slf4j
public class TestTreeTraversing {

    private static final TreeTraverser<Tree> ADAPTER = new TreeTraverser<Tree>() {
        @Override
        public Iterable<Tree> children(Tree node) {
            return node.getChildren();
        }
    };


    //        root
    //      / | \
    //     /  e  \
    //    d       g
    //   /|\      |
    //  / | \     f
    // a  b  c
    static final Tree root = new Tree('h');
    static final Tree d = new Tree('d', root);
    static final Tree a = new Tree('a', d);
    static final Tree b = new Tree('b', d);
    static final Tree c = new Tree('c', d);
    static final Tree e = new Tree('e', root);
    static final Tree g = new Tree('g', root);
    static final Tree f = new Tree('f', g);


    static String iterationOrder(Iterable<Tree> iterable) {
        StringBuilder builder = new StringBuilder();
        for (Tree t : iterable) {
            builder.append(t.getValue());
        }
        return builder.toString();
    }

    @Test
    public void testPreOrder() {
        Assert.assertEquals(iterationOrder(ADAPTER.preOrderTraversal(root).toList()), "hdabcegf");
    }

    @Test
    public void testPostOrder() {
        Assert.assertEquals(iterationOrder(ADAPTER.postOrderTraversal(root)), "abcdefgh");
    }

    @Test
    public void testBreadthOrder() {
        Assert.assertEquals(iterationOrder(ADAPTER.breadthFirstTraversal(root)), "hdegabcf");
    }

    @Test
    public void testReBuild() {
        Iterator<Tree> iterator = ADAPTER.preOrderTraversal(root).iterator();
        Tree tempRoot = new Tree(iterator.next().getValue());
        buildChildren(root, tempRoot, iterator);
        log.info("buildRoot finish");
    }

    private void buildChildren(Tree sourceParent, Tree parent, Iterator<Tree> iterator) {
        int count = 0;
        while (sourceParent.getChildren().size() - count != 0) {
            Tree source = iterator.next();
            Tree next = new Tree(source.getValue(), parent);
            if (source.getChildren().size() > 0) {
                buildChildren(source, next, iterator);
            }
            count++;
        }
    }

}

~~~

----

心得 : Guava真的很好用.

----
參考資料

* [小殘的程式光廊](http://emn178.pixnet.net/blog/post/95499086)
* [Wikipedia](https://en.wikipedia.org/wiki/Tree_traversal)
* [RosettaCode-Tree_traversal](https://rosettacode.org/wiki/Tree_traversal)
