Python 虚拟环境（Virtual Environment）是一个用于隔离项目依赖的工具。它可以让你在同一台机器上为不同的项目创建独立的 Python 环境，这样每个项目可以有自己独立的库和依赖关系，而不影响全局的 Python 安装。

## 为什么需要 Python 虚拟环境？

Python 项目经常依赖于各种第三方库（如 `numpy`、`pandas`、`matplotlib` 等），这些库的不同版本之间可能存在不兼容的情况。虚拟环境的主要作用是解决以下问题：

1. **依赖隔离**：
   - 如果你有两个不同的项目，一个依赖于 `numpy` 1.18，另一个依赖于 `numpy` 1.20，直接在全局环境中安装它们会引起冲突。虚拟环境可以为每个项目隔离依赖，确保它们互不影响。
2. **保持项目的可移植性**：
   - 当你在某个项目中锁定了特定的依赖版本，虚拟环境确保在未来的某个时间，即使某些库发布了新版本，你的项目依然可以使用你最初指定的库版本。这对于项目的长期维护和开发非常重要。
3. **安全性**：
   - 使用虚拟环境时，安装的依赖包仅限于当前虚拟环境，而不会污染系统的全局 Python 环境。避免全局安装过多的包而导致系统变得混乱。
4. **多版本 Python 支持**：
   - 你可以在不同的虚拟环境中使用不同版本的 Python。例如，一个项目使用 Python 3.8，而另一个项目可能使用 Python 3.10。虚拟环境可以帮助你轻松管理这些不同的 Python 版本。

## 如何工作？

虚拟环境其实是一个包含独立 Python 解释器和库的目录。每当你创建一个虚拟环境时，Python 会为这个环境生成一个隔离的运行环境，其中包含：

- 一个 Python 解释器（通常和系统的全局 Python 解释器相同，但它是隔离的）。
- 一个空的 `site-packages` 目录，用于存放在该虚拟环境中安装的依赖包。

当虚拟环境被激活时，系统的 `PATH` 会被修改，使得 Python 命令和包管理工具 `pip` 只对这个虚拟环境有效。因此，所有的 Python 命令和依赖安装只在该虚拟环境内进行，而不会影响全局的 Python 设置。



## 配置 Python 虚拟环境

在 **Windows 11 系统** 上使用 **PowerShell** 配置 Python 虚拟环境，并使用 Python 3 自带的 `venv` 模块是一个非常常见的操作。下面是完整的步骤，帮助你在 PowerShell 中配置虚拟环境。

### 1. **检查 Python 是否已安装**

在开始之前，确保你已经安装了 Python 3.x，并且添加到了系统的 `PATH` 环境变量中。可以通过以下命令检查 Python 版本：

```powershell
python --version
```

如果显示了 Python 的版本号（如 `Python 3.9.x` 或 `Python 3.10.x`），说明 Python 已经正确安装。如果没有，可能需要先下载安装 Python，并确保勾选“Add Python to PATH”。

### 2. **进入项目目录**

首先，进入你希望创建虚拟环境的项目目录。你可以使用 PowerShell 的 `cd` 命令进入你想要创建虚拟环境的文件夹：

```powershell
cd C:\path\to\your\project
```

例如，你可以创建一个项目目录：

```powershell
mkdir my_project
cd my_project
```

### 3. **创建虚拟环境**

接下来，你可以使用 `venv` 模块创建虚拟环境。假设你希望将虚拟环境命名为 `venv`，可以运行以下命令：

```powershell
python -m venv venv
```

这会在当前目录下创建一个名为 `venv` 的虚拟环境目录，其中包含 Python 可执行文件和依赖包。

### 4. **激活虚拟环境**

创建好虚拟环境后，你需要激活它。PowerShell 有不同的激活方式，你可以通过以下命令激活虚拟环境：

```powershell
.\venv\Scripts\Activate
```

激活后，PowerShell 的提示符会发生变化，通常会在提示符的最左边显示虚拟环境的名称，例如：

```powershell
(venv) PS C:\path\to\your\project>
```

这表示虚拟环境已成功激活，你现在可以在其中安装 Python 包，并且这些包会仅限于该虚拟环境中。

### 5. **安装依赖**

在激活虚拟环境之后，你可以使用 `pip` 安装任何你需要的 Python 包，比如 `numpy`、`pandas` 等：

```powershell
pip install numpy pandas
```

这些包将被安装在虚拟环境中的 `Lib\site-packages` 目录中，而不会影响系统全局的 Python 环境。

### 6. **退出虚拟环境**

完成工作后，你可以通过以下命令退出虚拟环境：

```powershell
deactivate
```

此时，PowerShell 提示符将恢复到没有虚拟环境的状态。

### 7. **删除虚拟环境**

如果你想删除虚拟环境，首先确保虚拟环境已被停用，然后你可以直接删除虚拟环境所在的目录。使用以下命令在 PowerShell 中递归删除 `venv` 目录：

```powershell
Remove-Item -Recurse -Force .\venv
```

### 8. **设置执行策略（仅首次运行）**

在 Windows 11 的 PowerShell 中，默认可能会限制脚本执行，导致激活虚拟环境的 `Activate` 脚本无法运行。如果遇到激活虚拟环境时报错，可以使用以下命令临时允许执行脚本：

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```

这条命令允许 PowerShell 运行本地的脚本，但不修改系统的全局设置，安全性较高。

### 完整步骤示例：

1. 进入项目目录：
   ```powershell
   cd C:\Users\your_user\my_project
   ```

2. 创建虚拟环境：
   ```powershell
   python -m venv venv
   ```

3. 激活虚拟环境：
   ```powershell
   .\venv\Scripts\Activate
   ```

4. 安装依赖（例如 `numpy` 和 `pandas`）：
   ```powershell
   pip install numpy pandas
   ```

5. 完成工作后退出虚拟环境：
   ```powershell
   deactivate
   ```

6. 删除虚拟环境：
   ```powershell
   Remove-Item -Recurse -Force .\venv
   ```

### 总结：

- **创建虚拟环境**：`python -m venv venv`
- **激活虚拟环境**：`.\venv\Scripts\Activate`
- **退出虚拟环境**：`deactivate`
- **删除虚拟环境**：`Remove-Item -Recurse -Force .\venv`

通过这些步骤，你可以在 Windows 11 上使用 PowerShell 轻松管理 Python 虚拟环境。



为了使用国内镜像（如清华大学的镜像 `https://pypi.tuna.tsinghua.edu.cn/simple`）来安装 `requirements.txt` 文件中的依赖包，你可以在安装时指定镜像源。具体做法如下：

### 使用命令行指定国内镜像源

在安装 `requirements.txt` 时，可以使用 `-i` 参数指定 PyPI 镜像源：

```bash
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

### 说明：
- `-r requirements.txt`：表示从 `requirements.txt` 文件中读取需要安装的包。
- `-i`：用于指定要使用的包源，这里指定了清华大学的 PyPI 镜像源。

这样，`pip` 会从清华大学的镜像站点安装所需的 Python 包，大大加速下载速度，尤其是在中国国内网络环境下。

### 如果需要长期使用国内镜像

如果你想避免每次都手动指定镜像源，可以通过配置 `pip` 的配置文件，使其默认使用国内镜像。

#### 在 Windows 系统上：
1. 打开或创建文件 `C:\Users\<你的用户名>\pip\pip.ini`。
2. 在文件中添加如下内容：

```ini
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

#### 在 Linux/macOS 系统上：
1. 打开或创建文件 `~/.pip/pip.conf`。
2. 在文件中添加如下内容：

```ini
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

通过这种方式，`pip` 将默认使用清华大学的 PyPI 镜像源来安装包，不需要每次都手动指定。

### 总结

- **临时使用镜像源**：`pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple`
- **永久使用镜像源**：通过配置 `pip.ini` 或 `pip.conf` 文件来默认使用国内镜像。

这样你就可以更加快捷、高效地从国内镜像安装 Python 依赖包了。



## 管理多个虚拟环境

你可以将多个虚拟环境放在同一个文件夹下进行集中管理，这样可以方便你在多个项目之间进行环境切换和管理。下面是如何实现这个结构的步骤与方法。

### 多个虚拟环境集中管理的目录结构

假设你有多个项目，并且希望将它们的虚拟环境集中放置在某个文件夹下（例如 `C:\venvs`），而不是每个项目的目录中。在这种情况下，你可以为每个项目创建一个单独的虚拟环境，目录结构可以类似于下面这样：

```
C:\venvs\
    ├── project1_env\
    ├── project2_env\
    └── project3_env\
C:\projects\
    ├── project1\
    ├── project2\
    └── project3\
```

在这个结构中：
- **C:\venvs** 是你放置虚拟环境的目录，每个项目的虚拟环境都存放在其中。
- **C:\projects** 是你存放项目代码的目录，每个项目的代码和虚拟环境是分开的。

### 如何实现这种结构

#### 1. 创建一个存放虚拟环境的目录

你可以选择创建一个专门用于存放虚拟环境的目录，例如 `C:\venvs`：

```powershell
mkdir C:\venvs
```

这个目录将用于存放你所有的虚拟环境。

#### 2. 在该目录下创建虚拟环境

然后，为每个项目在 `C:\venvs` 中创建一个虚拟环境。例如，你有两个项目 `project1` 和 `project2`，可以分别为它们创建虚拟环境：

```powershell
python -m venv C:\venvs\project1_env
python -m venv C:\venvs\project2_env
```

这将在 `C:\venvs` 下分别创建名为 `project1_env` 和 `project2_env` 的虚拟环境。

#### 3. 激活对应的虚拟环境

每次需要激活某个项目的虚拟环境时，你可以通过指定虚拟环境路径来激活它：

- **激活 `project1_env`**：

  ```powershell
  C:\venvs\project1_env\Scripts\Activate
  ```

- **激活 `project2_env`**：

  ```powershell
  C:\venvs\project2_env\Scripts\Activate
  ```

激活成功后，PowerShell 提示符会显示相应虚拟环境的名称，例如 `(project1_env)`。

#### 4. 进入项目目录并运行代码

在激活虚拟环境后，你可以转到项目的代码目录并运行 Python 代码或安装依赖。例如：

```powershell
cd C:\projects\project1
python main.py
```

或者安装依赖：

```powershell
pip install numpy pandas
```

### 优点

将多个虚拟环境集中管理在一个目录下有以下几个优点：

1. **结构清晰**：项目代码和虚拟环境分开管理，项目目录保持干净整洁。
2. **集中管理**：所有虚拟环境都放在同一个地方，便于你进行备份、切换和管理。
3. **灵活性**：你可以为每个项目创建独立的虚拟环境，且不同项目间的环境不会相互干扰。

### 缺点

1. **切换复杂性**：每次激活虚拟环境时需要输入虚拟环境的完整路径，稍微增加了一些复杂性。不过你可以通过脚本或别名简化操作。
2. **项目目录中无法直接看到虚拟环境**：如果你习惯将虚拟环境放在项目目录中进行管理，那么这种方式将虚拟环境和项目分离，可能会不太习惯。

### 简化激活虚拟环境的过程

你可以创建一个批处理文件或 PowerShell 脚本，用于快速激活对应项目的虚拟环境并进入项目目录。以下是一个示例脚本：

#### PowerShell 脚本示例（`activate_project1.ps1`）

```powershell
# 激活 project1_env 虚拟环境并进入项目1目录
C:\venvs\project1_env\Scripts\Activate
cd C:\projects\project1
```

你可以为每个项目创建一个类似的脚本，然后只需运行脚本即可同时激活虚拟环境并切换到项目目录，方便快速启动工作。

#### 批处理文件示例（Windows 下 `.bat` 文件）

```batch
@echo off
call C:\venvs\project1_env\Scripts\Activate
cd C:\projects\project1
```

### 总结

- **将多个虚拟环境集中存放在一个目录下**（如 `C:\venvs`）是完全可行的。
- 项目代码和虚拟环境可以分开存放，这样有助于保持项目代码目录的简洁。
- 每次工作时，只需激活相应的虚拟环境并进入项目目录即可。
- 通过脚本简化激活虚拟环境的过程可以提高效率。

这种方法可以帮助你更好地管理多个项目的虚拟环境，使得项目环境更清晰且易于维护。



一个 Python 虚拟环境占用的硬盘空间取决于以下几个因素：

1. **Python 解释器的大小**：虚拟环境中包含一个独立的 Python 解释器副本。
2. **标准库的大小**：Python 自带的标准库会被复制到虚拟环境中。
3. **已安装的第三方包**：安装的依赖包越多，占用的空间也就越大。



## 虚拟环境空间占用的问题

在你刚创建一个虚拟环境时（例如使用 `venv` 或 `virtualenv`），没有安装任何第三方包的情况下，虚拟环境的大小主要由以下几个部分构成：

1. **Python 解释器**：大约 20 - 50 MB，视 Python 版本不同而略有差异。
2. **标准库**：Python 的标准库大约在 40 - 100 MB 左右，具体大小依赖于 Python 的版本。
3. **一些基础的依赖**（例如 `pip` 和 `setuptools`）：通常几 MB。

因此，**一个空的虚拟环境**（没有安装额外包的情况下）大概占用 **100 MB - 200 MB** 的硬盘空间。

### 虚拟环境随包的增加而变化

随着你向虚拟环境中安装第三方库（如 `numpy`、`pandas`、`scikit-learn` 等），虚拟环境的大小会显著增加：

- **轻量级的包**（如 `requests`）：通常大小不到 1 MB。
- **科学计算库**（如 `numpy`）：大约 10 - 50 MB。
- **数据分析库**（如 `pandas`）：大约 20 - 100 MB，具体取决于依赖项的版本。
- **机器学习库**（如 `scikit-learn`）：大约 50 - 100 MB。

如果你安装了大量的第三方包（例如用于数据分析或机器学习的完整环境），虚拟环境的大小可能会增加到 **几百 MB** 甚至 **1 GB 以上**。

### 影响虚拟环境大小的因素

1. **Python 版本**：较新版本的 Python 可能会包含更多的标准库，虚拟环境也会略大一些。
2. **操作系统**：在 Windows 上，Python 解释器和虚拟环境通常会稍大一些，因为 Windows 的 Python 可执行文件通常比 Linux/macOS 上的要大。
3. **安装的第三方包**：依赖库（特别是科学计算和机器学习库）的大小会显著影响虚拟环境的大小。

### 如何减少虚拟环境的大小

1. **安装必要的包**：避免安装过多不需要的第三方库，以减少占用的空间。
2. **清理缓存**：安装包后，`pip` 会缓存一些安装文件，使用以下命令可以清理这些缓存，释放空间：
   ```bash
   pip cache purge
   ```

### 总结

- 一个全新的、空的 Python 虚拟环境大约占用 **100 MB - 200 MB** 的硬盘空间。
- 如果你安装了大量的依赖，虚拟环境的大小可能增加到 **几百 MB** 到 **1 GB 以上**。
- 虚拟环境的大小主要取决于安装的第三方库和具体的 Python 版本。