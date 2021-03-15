### h5py学习
#### 一、基础知识
##### （一）安装
* 【Anaconda3安装】

```bash
conda install h5py
```
* 【Miniconda安装】

```bash
enpkg h5py
```

* 【pip安装】
```bash
pip install h5py
```

* 【MacOS】：使用brew 安装
* 【源码安装】
> 1. 安装组件：python的发行版
> 2. 安装组件：HDF5 版本1.8.4+
> 3. 安装组件：C编译器
> 4. 通过命令安装
```bash
# 方法一
python insatll --no-binary=h5py h5py
# 方法二
python insatll -v
# 方法三
python setup.py install
```

##### （二）核心概念
【hdf】
* HDF5是两种对象的容器：dataset、group
* 以字典的概念理解group
* 以numpy数组的概念理解dataset

【h5py】
* 操作过程
1. 读取文件
2. 通过类似字典的形式查看文件的keys
3. 通过keys访问文件的dataset
4. 支持通过对数组样式进行切片处理

#### 二、学习内容
##### （一）安装
##### （二）文件对象
* 文件对象是对hdf5文件操作的基本对象，其使用方式与`python`的文件方式类似
```python
import h5py
# 创建文件对象
# 不同的mode,其对文件的操作也不同
f = h5py.File('file_name','mode')
# 'r'模式，只读文件，要求文件必须存在
f = h5py.File('file_name','r')
# 'r+'模式，读写文件，要求文件必须存在
f = h5py.File('file_name','r+')
# 'w'模式，创建文件，若文件存在则截断
f = h5py.File('file_name','w')
# 'w-/x'模式，创建文件，若文件存在则失败
f = h5py.File('file_name','w-')
# 'a'模式，读写，若文件存在则读写，若文件不存在则创建
f = h5py.File('file_name','-')
```
* `f.close()`：关闭文件，所有文件打开的对象都将无效
* `f.flush()`：关闭文件，所有文件打开的对象都将无效
* `f.id`：关闭文件，所有文件打开的对象都将无效
* `f.filename`：关闭文件，所有文件打开的对象都将无效
* `f.mode`：关闭文件，所有文件打开的对象都将无效
* `f.driver`：关闭文件，所有文件打开的对象都将无效
* `f.libver`：关闭文件，所有文件打开的对象都将无效
* `f.userblock_size`：关闭文件，所有文件打开的对象都将无效
##### （三）group
* 若文件'file.hdf5'已存在，可以创建f下的group
* 可以将f视为最大的group,目录结构为`/`
* 使用`create_group()`添加子group
* 使用`del g['name']`通过`name`删除子group
```python
import h5py
f = h5py.File('name.hdf5','a')
# 创建单层group
g_1 = f.create_group('g1')
# 创建多层group
g_2 = f.create_group('g1/g2/g3')
# 删除单层group
del f['g_1']
# 删除多层group
del f['g_1/g_2/g_3']
```
* 使用`dict接口`访问

```python
import h5py
f = h5py.File('name.hdf5','a')
# 创建单层group
g_1 = f.create_group('grooup_name')
# 创建多层group
g_2 = f.create_group('grooup_name/1_name')
```
【属性】
* `attrs`
* `id`
* `ref`
* `regionref`
* `name`
* `file`
* `parent`
【方法】
* `g.keys()`
* `g.values()`
* `硬链接`
* `软链接`
* `外部链接`

##### （四）dataset
* 若`group`已存在，可以创建`group`下的`dataset`
* group使用`create_dataset()`创建dataset
```python
import h5py
f = h5py.File('name.hdf5','a')
g = f.create_group('grooup_name')
# 添加直接dataset
dataset_1 = g.create_dataset('dataset_name')
# 指定完整路径添加group
dataset_2 = g.create_dataset('dataset_name/1_name')
```
##### （五）属性
* 若`dataset`已存在，可以设置/创建`dataset`的`属性`
* dataset使用`.attrs['属性名']`设置/访问自身属性
* 对属性的访问均建立在d.attrs上
```python
import h5py
f = h5py.File('name.hdf5','a')
g = f.create_group('grooup_name')
d = g.create_dataset('dataset_name')
# 添加属性
d.attrs['1'] = 1
d.attrs['2'] = 5
d.attrs['3'] = 6
d.attrs['4'] = 7
# 验证属性
for i in range(5):
	print(str(i) in d.attrs)
# 其他操作
# 详见操作手册
```
##### （六）创建/查看/设置h5py文件实例