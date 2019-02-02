## Tensor与tensor深入分析

在Pytorch官方文档中，对于 `Tensor`  与 `tensor` 是这样定义的：

> A [`torch.Tensor`](https://pytorch.org/docs/stable/tensors.html#torch.Tensor) is a multi-dimensional matrix containing elements of a single data type
>
> To create a tensor with pre-existing data, use `torch.tensor()`

`Tensor` 是多维矩阵，矩阵的元素都是同一种数据类型。

`tensor` 需要确切的数据对它进行赋值。

**对于变量，创建的方式有两种：创建变量的数据形状大小并初始化；直接赋值确切的数据值**

接下来，就讨论 `Tensor` 与 `tensor` 创建的特点：

**方式一：创建变量的数据形状大小并初始化**

指定形状的大小时，会发生这种情况：对于多维矩阵，（3，4）可以表示三行四列的矩阵，这是没有歧义的。对于 `Tensor` 会创建一个三行四列的矩阵，但是对于 `tensor` 却无法创建相应的变量。因为它需要却确定的数据值。

但当输入（5）时，`Tensor` 是一个矩阵，所以将这个5理解为是（1，5），一行五列的矩阵。

`tensor` 会将这个5认为是一个确定的数据。它会创建出一个值为5的变量。

代码：

输入为5时：

```python
Input:
	>>>x = torch.Tensor(3, 4)
	>>>y = torch.tensor(3, 4)	#这行是错误的，因为tensor需要确切的数据值
	>>>print(x)
Output:
tensor([[1.3733e-14, 6.4076e+07, 2.0706e-19, 7.3909e+22],
        [2.4176e-12, 1.1625e+33, 8.9605e-01, 1.1632e+33],
        [5.6003e-02, 7.0374e+22, 1.0284e+21, 1.0596e-38]])
```

输入为（5）时：

```python
Input:
    >>>x = torch.Tensor(5)
    >>>y = torch.tensor(5)
    >>>print(x.size())
	>>>print(y.size())
    >>>print(x.type())
    >>>print(y.type())
Output:
    torch.Size([5])		#这个表示，x是一个一维张量，就像数学中的向量
    torch.Size([])		#这个表示，y是一个标量，是一个0维度的张量
    torch.FloatTensor	#x在未指定数据类型的时候，默认是FloatTensor类型
    torch.LongTensor	#tensor在未指定数据类型的时候，会根据赋值数据的形式，选择相应的类型
```

**方式二：直接赋值确切的数据值**

`Tensor`与`tensor`都可以通过这种方式进行创建变量。但有一种特殊情况，就是 `torch.Tensor(5.6)` 是错误的。你可以这样理解，因为Tensor创建的是多维矩阵，从严格意义上说，标量（一个数字），不是矩阵。所以`Tensor`无法创建。而这种方式就是允许的，`torch.Tensor([5.6])`。

```Python
Input:
	>>>a = torch.Tensor([[5.6, 5.8],[2, 4]])
	>>>b = torch.tensor([[5.6, 5.8],[2, 4]])
	>>>print(a)
	>>>print(b)
	>>>print(a.size())
	>>>print(b.size())
	>>>print(a.type())
	>>>print(b.type())
Output:
tensor([[5.6000, 5.8000],
        [2.0000, 4.0000]])
tensor([[5.6000, 5.8000],
        [2.0000, 4.0000]])
torch.Size([2, 2])
torch.Size([2, 2])
torch.FloatTensor
torch.FloatTensor
```

**接下来示范下错误的一些方式**

```python
Error：
	>>>a = torch.tensor(3, 4)	#tensor是从已有数据中创建矩阵的，这种形式，tensor无法对矩阵中的元素进行初始化，所以无法进行创建。如果是Tensor时，Tensor默认的数据类型是FloatTensor，可以对其进行初始化
	>>>a = torch.Tensor(5.6)
```

---

总结：

`Tensor`主要是创建多维矩阵的，标量从某种意义上，不算矩阵。所以`Tensor`可以通过赋值多维矩阵的方式创建，但是无法指定标量值进行创建。如果想创建单个值，采用[5.6] 这种形式，指定一行一列的矩阵。

同时，`Tensor`可以指定多维矩阵形状的大小，并且默认的数据类型是`FloatTensor`。

`tensor`主要是根据确定的数据值进行创建，无法直接指定形状大小，需要根据数据的大小进行创建。但同时，`tensor`没有赋值数据值是矩阵的限制，可以直接使用`tensor(5.6)`

```Python
Input:
    a = torch.tensor(5.6)
    print(a)
    print(a.size())
Output:
    tensor(5.6000)
    torch.Size([])	#pytorch对标量（0维矩阵）的表示

```

<center>公众号：「土堆碎念」</center>
<center>一些不成熟的想法与碎念</center>
<center>一些无趣，精心打造的教程</center>

