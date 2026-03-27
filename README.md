# JDK Version Manager (JVMS)

## 项目概述
JVMS (JDK Version Manager) 是一个轻量级的命令行工具，用于在单个机器上管理多个 JDK (Java Development Kit) 版本。它允许开发者轻松地在不同的 Java 版本之间切换，特别适合需要测试项目在不同 JDK 版本下兼容性的场景。

## 主要功能

### 🔄 版本切换
- 快速切换不同 JDK 版本
- 持久化设置（无需每次打开终端都重新设置）
- 自动在所有打开的终端窗口中生效
- 重启系统后设置仍然保持

### 📦 版本管理
- **扫描添加**：自动扫描系统中已安装的 JDK 版本
- **手动添加**：添加本地已安装的 JDK 版本
- **删除版本**：移除不再需要的 JDK 版本
- **列表查看**：显示所有已配置的 JDK 版本及其安装路径

### 🛠️ 系统集成
- 自动修改 shell 配置文件（`.zshrc` 或 `.bash_profile`）
- 设置 `JAVA_HOME` 环境变量
- 更新 `PATH` 环境变量
- 创建符号链接指向当前选中的 JDK 版本

## 安装方法

### 自动安装
```bash
# 克隆项目
git clone https://github.com/pretent/jvms.git

# 进入项目目录
cd jvms

# 赋予执行权限
chmod +x jvms

# 添加到 PATH（可选）
sudo cp jvms /usr/local/bin/
```

### 初始化配置
```bash
# 运行初始化命令
jvms init
```

## 使用指南

### 基本命令
```bash
# 查看帮助
jvms -h

# 初始化配置
jvms init

# 扫描系统已安装的 JDK
jvms load

# 列出所有 JDK 版本
jvms ls

# 添加本地 JDK 版本
jvms add <版本名称> <JDK路径>

# 切换 JDK 版本
jvms set <版本名称>

# 删除 JDK 版本
jvms rm <版本名称>

# 查看当前 Java 版本信息
jvms version

# 查看工具信息
jvms info
```

### 使用示例
```bash
# 扫描并添加系统已安装的 JDK
jvms load

# 列出所有可用版本
jvms ls

# 切换到 Java 11
jvms set 11.0.1

# 验证切换结果
java -version
```

## 项目特点

### 🚀 轻量高效
- 纯 Bash 脚本实现，无外部依赖
- 快速执行，资源占用低
- 简单直观的命令行界面

### 🔧 灵活配置
- 支持手动添加任意本地 JDK 安装
- 自动扫描系统已安装的 JDK
- 可自定义版本命名

### 📋 信息完整
- 显示每个 JDK 版本的安装路径和时间
- 提供详细的错误信息和操作指导
- 支持版本验证和状态检查

### 🛡️ 安全可靠
- 操作前进行备份
- 提供确认提示防止误操作
- 兼容 macOS 和 Linux 系统

## 系统要求

- **操作系统**：macOS、Linux
- **Shell**：Zsh (macOS)、Bash (Linux)
- **依赖工具**：标准的 Unix 工具（sed、cut、grep 等）

## 技术实现

### 核心机制
1. **配置文件管理**：使用 `jvms.conf` 文件存储版本信息
2. **符号链接**：创建 `~/.jdk/Home` 符号链接指向当前选中的 JDK
3. **环境变量**：自动设置 `JAVA_HOME` 和更新 `PATH`
4. **版本扫描**：利用系统工具（如 `/usr/libexec/java_home`）发现已安装 JDK

### 文件结构
```
jvms/
├── jvms          # 主程序（Bash 脚本）
├── jvms.conf     # 版本配置文件
├── .jdk/         # 符号链接目录
└── README.md     # 项目说明文档
```

## 适用场景

### 🧪 多版本测试
- 测试项目在不同 Java 版本下的兼容性
- 验证新版本 JDK 的功能特性
- 确保向后兼容性

### 🎓 学习开发
- 同时学习多个 Java 版本
- 比较不同版本的行为差异
- 理解版本演进过程

### 🔧 生产环境
- 平滑升级 JDK 版本
- 临时回退到旧版本进行问题排查
- 维护多个需要不同 JDK 版本的项目

## 注意事项

1. **权限要求**：某些操作可能需要管理员权限
2. **备份机制**：修改 shell 配置文件前会自动创建备份
3. **兼容性**：主要针对 macOS 优化，Linux 支持可能有限
4. **错误处理**：提供详细的错误信息和解决建议

## 贡献与支持

### 问题反馈
如果您遇到任何问题或有改进建议，请通过以下方式反馈：
- 在 GitHub 项目页面提交 Issue
- 通过邮件联系项目维护者

### 开发贡献
欢迎提交 Pull Request 来改进项目：
- 修复 bug
- 添加新功能
- 改进文档
- 优化用户体验

---

**JVMS** - 让 JDK 版本管理变得简单高效！