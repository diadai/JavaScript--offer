**题目**：输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

我的方案：

```

//        function TreeNode(x) {
//            this.val = x;
//            this.left = null;
//            this.right = null;
//        }
        function reConstructBinaryTree(pre, vin)
        {
            if(pre.length===0||!pre){
                return;
            }
            var root = {
                val: pre[0]
            };
            var everyroot =vin.indexOf(pre[0]);
        root.left=reConstructBinaryTree(pre.slice(1,everyroot+1),vin.slice(0,everyroot));
            root.right=reConstructBinaryTree(pre.slice(everyroot+1),vin.slice(everyroot+1));

            return root;
        }
        console.log(reConstructBinaryTree('12473568','47215386'));
```
**分析**：此题关于二叉树和二叉树的遍历以及二叉树的输出

二叉树的一般结构为
```
      function TreeNode(x) {
            this.val = x;
            this.left = null;
            this.right = null;
        }
```
二叉树的遍历分为：前序遍历，中序遍历，后序遍历

前序遍历
```
function PreOrderTraverse(treeNode)
{
    if(treeNode.val== NULL)
        return;
    Visit(treeNode); // 访问根节点
    PreOrderTraverse(treeNode.left); // 前序遍历左子树
    PreOrderTraverse(treeNode.right); // 前序遍历右子树
}
```
后序遍历
```
function InOrderTraverse(treeNode)
{
    if(treeNode.val== NULL)
        return;
    InOrderTraverse(treeNode.left); // 中序遍历左子树
    Visit(treeNode.val); // 访问根节点
    InOrderTraverse(treeNode.right); // 中序遍历右子树
}
```
后序遍历
```
void PostOrderTraverse(treeNode)
{
    if(pRoot == NULL)
        return;
    PostOrderTraverse(treeNode.left); // 后序遍历左子树
    PostOrderTraverse(treeNode.right); // 后序遍历右子树
    Visit(treeNode.val); // 访问根节点
}
```
**知识点**：
（1）：二叉树的结构，遍历。
（2）：数组的一些方法，我用到的slice(),indexOf()。
（3）：递归函数的栈溢出问题，就要检查下自己的代码有没有出现死循环调用，或者大量的递归调用。。[Javascript中递归造成的堆栈溢出及解决方案](http://www.cnblogs.com/cuew1987/p/4122856.html")
（4）：字符串和数组的方法千万不要混用。
**别人代码**：

```
function reConstructBinaryTree(pre, vin)
{
    // write code here
    if(pre.length==0 || vin.length==0) return null;
    var index=vin.indexOf(pre[0]);
    var left=vin.slice(0,index);//中序左子树
    var right=vin.slice(index+1);//中序右子树
    return {
        val:pre[0],
        //递归左右子树的前序，中序
        left:reConstructBinaryTree(pre.slice(1,index+1),left),
        right:reConstructBinaryTree(pre.slice(index+1),right)
     };
}
```

[牛客网--《剑指offer》相关题目](https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6?tpId=13&tqId=11157&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking")