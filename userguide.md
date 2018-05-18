# Jupyter用户指南
## 引言
笔记本扩展了基于命令行的方法以高品质来实现交互式计算，提供了一个基于网页应用适用于捕捉整个计算过程：开发，文档处理，执行代码，以及返回结果。jupyter笔记本结合了两个内容：

**一个网页应用**：一个用于包含说明文本，数学，计算以及相应的丰富的格式输出文档的基于浏览器的交互写作工具。

**笔记本文档**：所有内容在网页应用中可见表示，包括计算的输入，输出，解释文本，数学，和丰富的对象媒体表示。

>也见于:

>阅读[安装指南]()关于怎样安装笔记本和它的依赖项。

### 网页应用的主要特征

- 浏览器编辑代码，具备自动语法高亮，缩进和tab补全纠错。
- 从浏览器中执行代码,计算结果附加在产生它们的代码上。
- 计算结果用富媒体表示，例如HTML，LaTex,PNG,SVG等，例如，由matplotlib库支持的出版质量的图，可以被包含在行内。
- 浏览器内编辑富文本使用[Markdown](https://daringfireball.net/projects/markdown/syntax)标记语言，并且可以为代码提供注释，而不只是纯文本。
- 轻松地在markdown单元中使用LaTeX包含数学记号，自然地由[MathJax](https://www.mathjax.org/)。

### 笔记本文档
Notebook文档包含交互式会话的输入和输出以及代码附带的其他文本，但不适用于执行。通过这种方式，笔记本文件可以充当会话的完整计算记录，将可执行代码与解释性文本，数学和结果对象的丰富表示交织在一起。这些文档是内部的[JSON](https://en.wikipedia.org/wiki/JSON)文件，并以`.ipynb`扩展名保存。由于JSON是纯文本格式，因此可以通过版本控制并与同事共享。

可以通过[nbconvert](https://nbconvert.readthedocs.io/en/latest/)命令将笔记本导出为一系列静态格式，包括HTML（例如，博客文章），reStructuredText，LaTeX，PDF和幻灯片放映。

此外，可以通过Jupyter Notebook Viewer（nbviewer）共享可从公共URL获得的任何`.ipynb`笔记本文档。该服务从URL加载笔记本文档并将其呈现为静态网页。因此，结果可能会与同事共享，或作为公共博客帖子分享，而其他用户无需自行安装Jupyter笔记本。实际上，nbviewer只是nbconvert作为一个web服务，所以你可以用nbconvert做你自己的静态转换，而不依赖于nbviewer。

>同样见于：

>笔记本JSON文件格式的详情

### 笔记本和隐私

由于您在网络浏览器中使用Jupyter，因此有些人可以理解地将关心敏感数据的使用安全。 然而，如果您遵循标准安装说明，Jupyter实际上是在您自己的计算机上运行。 如果地址栏中的URL以
http:localhost： 或 http://127.0.0.1: 开头，则表示您的计算机充当服务器。 Jupyter不会将数据发送到其他任何地方 - 而且由于它是开源的，其他人可以检查我们对此是否诚实。

您也可以远程使用Jupyter：例如，您的公司或大学可能会为您运行服务器。 如果您想在这些情况下处理敏感数据，请咨询您的IT或数据保护人员。

我们的目标是确保浏览器中的其他页面或同一台计算机上的其他用户无法访问笔记本服务器。 有关更多信息，请参阅[Jupyter笔记本服务器中的安全性]()。
## 启动笔记本服务器
你可以从命令行里使用如下命令运行一个笔记本：

    jupyter notebook
这将在您的控制台中打印关于笔记本服务器的一些信息，并打开Web浏览器以访问Web应用程序的URL（默认为http://127.0.0.1:8888 ）。

Jupyter笔记本Web应用程序的登录页面（**仪表板**）显示当前笔记本目录中可用的笔记本（默认情况下，笔记本服务器从其启动的目录）。

您可以使用“新建笔记本”按钮从仪表板创建新笔记本，也可以通过单击其名称打开现有笔记本。您还可以将`.ipynb`笔记本和标准`.py` Python源代码文件拖放到笔记本列表区域。

从命令行启动笔记本服务器时，您也可以直接打开特定笔记本，绕过仪表板，使用`jupyter`笔记本my_notebook.ipynb。如果没有给出扩展名，则假定`.ipynb`扩展名。

当您在打开的笔记本中时，File |打开...菜单选项将在新浏览器选项卡中打开仪表板，以允许您从笔记本目录打开另一个笔记本或创建新的笔记本。

>注意
>
>如果你想在不同目录下的笔记本上工作，你可以同时启动多个笔记本服务器。 默认情况下，第一台笔记本服务器在端口8888上启动，随后笔记本服务器搜索该端口附近的端口。 您也可以使用`--port`选项手动指定端口。


### 创建一个新的笔记本文档

可以随时从仪表板创建新笔记本，或者使用活动笔记本中的“文件”→“新建”菜单选项创建新笔记本。 新笔记本在相同的目录中创建，并将在新的浏览器选项卡中打开。它也将在仪表板上的笔记本列表中映为新条目。![new-notebook](./fig/new-notebook.gif)
### 打开笔记本
一个打开的笔记本 **只有** 一个连接到内核的交互式会话，它将执行用户发送的代码并传回结果。 如果Web浏览器窗口关闭，此内核保持活动状态，并且从仪表板重新打开相同的笔记本，Web应用程序将连接到相同的内核。 在仪表板中，带有活动内核的笔记本在其旁边有一个`Shutdown`按钮，而没有活动内核的笔记本在其位置上有一个`Delete`按钮。

其他客户端可能连接到相同的内核。 当每个内核启动时，笔记本服务器会向终端输出如下消息:

```
[NotebookApp] Kernel started: 87f7d2c0-13e3-43df-8bb8-1bd37aaf3373
```
这个长字符串是内核的ID，用以获取连接内核所需的信息。如果笔记本使用IPython内核，则还可以通过运行`％connect_info magic`来查看此连接数据，它会显示相同的ID信息以及其他详细信息。

例如，您可以通过传递一部分ID，从命令行手动启动连接到同一内核的Qt控制台：
```
$ jupyter qtconsole - existing87f7d2c0
```
没有ID，--existing将连接到最近启动的内核。

使用IPython内核，您还可以在笔记本中运行`％qtconsole`[魔术](https://ipython.readthedocs.io/en/stable/interactive/tutorial.html#magics-explained)来打开连接到相同内核的Qt控制台。

也见于

[解耦双进程模型][解耦]

## 笔记本用户界面
当您创建新的笔记本文档时，您将看到 __笔记本名称__，__菜单栏__，__工具栏__ 和 __空白代码单元__。
![](./fig/blank-notebook-ui.png)

__笔记本名称__：显示在页面顶部Jupyter徽标旁边的名称反映了`.ipynb`文件的名称。 点击笔记本名称会弹出一个对话框，让您对其进行重命名。 因此，将笔记本从“未命名0”重命名为“我的第一个笔记本”在浏览器中，将`Untitled0.ipynb`文件重命名为我的第一个`notebook.ipynb`。

__`菜单栏`__：菜单栏提供了可用于操作笔记本功能的不同选项。

__`工具栏`__：通过点击图标，工具栏提供了在笔记本中执行最常用操作的快速方法。

__`代码单元格`__：单元格的默认类型; 阅读关于细胞的解释。


## 笔记本文件的结构
笔记本由一系列单元组成。单元格是一个多行文本输入字段，其内容可以通过使用_Shift-Enter_或单击工具栏上的“Play”按钮或菜单栏中的`Cell`，`Run`来执行。单元的执行行为由单元的类型决定。有三种类型的单元：__代码单元__，__Markdown单元__和__纯文本单元__。每个单元格都是一个代码单元格，但其类型可以通过使用工具栏上的下拉菜单（最初将为“代码”）或通过[键盘快捷键][short-cut]进行更改。

有关您可以在笔记本中执行的各种操作的更多信息，请参阅[示例集合](https://nbviewer.jupyter.org/github/jupyter/notebook/tree/master/docs/source/examples/Notebook/)。

### 代码单元格
__代码单元__允许您编辑和编写新代码，并提供完整的语法高亮和制表符完成。您使用的编程语言取决于 __内核__，而默认内核（IPython）运行Python代码。

当代码单元被执行时，它所包含的代码被发送到与笔记本相关的内核。从计算中返回的结果将作为单元的输出显示在笔记本中。输出不限于文本，还可以使用许多其他可能的输出形式，包括`matplotlib`图片和HTML表格（例如，用在`Pandas`数据分析包中）。这就是IPython丰富的显示功能。

也见于

[富文本输出](https://nbviewer.jupyter.org/github/ipython/ipython/blob/master/examples/IPython%20Kernel/Rich%20Output.ipynb)示例笔记本

### Markdown单元
您可以通过文字方式记录计算过程，使用`富文本`将描述性文本与代码交替使用。在IPython中，这是通过使用Markdown语言标记文本来完成的。相应的单元格称为Markdown单元格。 Markdown语言提供了一种简单的方法来执行该文本标记，即指定文本的哪些部分应该被强调（斜体），粗体，表单列表等。

如果您想为文档提供结构，则可以使用Markdown标题。 Markdown标题包含1到6个＃标记`＃`，后跟一个空格和章节的标题。Markdown标题将被转换为指向笔记本某个章节的可点击链接。在导出到其他文档格式（如PDF）时，它也用作提示。

当执行Markdown单元格时，Markdown代码将转换为相应的格式化富文本。 Markdown允许任意的HTML代码进行格式化。

在Markdown单元格中，您还可以使用标准的LaTeX符号以简单的方式包括数学：`$ ... $`用于内联数学，`$$ ... $$`用于表示单独的数学公式。当执行Markdown单元格时，LaTeX部分会自动以HTML输出格式呈现为具有高质量排版的方程式。 [MathJax](https://www.mathjax.org/)使得这成为可能，其支持LaTeX功能的一大部分。

由LaTeX和AMS-LaTeX（amsmath包）定义的标准数学环境也可以工作，如`\ begin {equation} ... \ end {equation}`和`\ begin {align} ... \ end {align}`。新的LaTeX宏可以使用标准方法定义，例如`\ newcommand`，通过将它们放置在Markdown单元格中的数学分隔符之间的任何位置。这些定义在整个IPython会话的其余部分都可用。

> 也见于

> [使用Markdown单元工作](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Working%20With%20Markdown%20Cells.ipynb)示例笔记本

### 纯文本单元
纯文本单元提供了一个可以直接编写输出的位置。纯文本单元不会被笔记本执行。当通过nbconvert传递时，原始单元格以未修改的目标格式传送。例如，您可以将完整的LaTeX输入到一个纯文本单元格中，该单元格仅在由nbconvert转换后才由LaTeX渲染。

## 基本工作流程
笔记本中的正常工作流程与标准的IPython会话非常相似，不同之处在于您可以多次就地编辑单元格，直到获得所需的结果，而不必使用`％run` 魔法命令重新运行不同的脚本。

通常情况下，您将计算问题分解，然后将相关想法组织到单元格中，并在前一部分正确工作时继续前进。交互式探索要比将计算分解为必须一起执行的多个脚本更为方便，后者在以前是必须的，特别是如果其中的一部分需要很长时间才能运行。

要中断耗时过长的计算，请使用`Kernel`，`Interrupt`菜单选项或i，i键盘快捷键。同样，要重新启动整个计算过程，请使用`Kernel`，`Restart`菜单选项或0,0快捷键。

笔记本可以作为`.ipynb`文件下载，也可以使用菜单选项`File`，`Download as`将其转换为多种其他格式。

> 也见于

> [在Jupyter Notebook运行代码](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Running%20Code.ipynb)实例笔记

> [笔记本基础](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)示例笔记本

### 键盘快捷键
笔记本中的所有操作都可以使用鼠标执行，但键盘快捷键也可用于最常见的操作。要记住的重要快捷键如下：

* Shift-Enter：运行单元格
    - 执行当前单元格，显示任何输出，然后跳转到下一个单元格。如果在最后一个单元格上调用Shift-Enter，它会在下面创建一个新单元格。这相当于单击工具栏中的“单元格”，“运行”菜单项或“播放”按钮。    
* Esc：命令模式 
    - 在命令模式下，您可以使用键盘快捷键浏览笔记本电脑。
* Enter：编辑模式
    - 在编辑模式下，您可以编辑单元格中的文本。有关可用快捷键的完整列表，请单击笔记本菜单中的`“帮助”`，`“键盘快捷键”`。

## 画图
Jupyter笔记本的一个主要特点是能够显示运行代码单元的输出图片。 IPython内核被设计为与matplotlib绘图库无缝协作以提供此功能。特定的绘图库集成是内核的一个特色。

## 安装内核
有关如何安装Python内核的信息，请参阅[IPython安装页面](https://ipython.org/install.html)。

Jupyter wiki有很多其他语言的[内核列表](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)。他们通常会附带说明如何在笔记本中配置内核。

## 信任笔记本
为防止在笔记本打开时，代表用户执行不可信代码，我们会存储每个可信任笔记本的签名。当笔记本打开时，笔记本服务器验证此签名。如果找不到匹配的签名，那么Javascript和HTML输出将不会显示，直到通过重新执行单元格重新生成。

您本人完全执行过的任何笔记本都将被视为受信任，并且其HTML和Javascript输出将在加载时显示。

如果您需要在不重新执行的情况下查看HTML或Javascript输出，并且您确定笔记本没有恶意，您可以通过命令行告诉Jupyter相信它：
```
$ jupyter信任mynotebook.ipynb
```
有关信任机制的更多详细信息，请参阅[笔记本文档安全性](https://jupyter-notebook.readthedocs.io/en/stable/security.html#notebook-security)

## 浏览器兼容性
Jupyter Notebook旨在支持这些浏览器的最新版本：

* Chorme
* Safari
* Firefox
Opera和Edge的最新版本也可以使用，但如果不使用，请使用其中一种支持的浏览器。

使用HTTPS和不可信证书的Safari不能工作（websocket将失败）。

[解耦]: 
[short-cut]: https://ipython.readthedocs.io/en/stable/interactive/tutorial.html#magics-explained
