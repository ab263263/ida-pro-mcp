# Augment插件配置IDA Pro MCP指南

## 📋 配置步骤

### 1. 在Augment中添加MCP服务器

将以下配置添加到您的Augment MCP设置中：

```json
{
  "mcpServers": {
    "ida-pro-mcp": {
      "command": "/mnt/persist/workspace/.venv/bin/python3",
      "args": [
        "/mnt/persist/workspace/src/ida_pro_mcp/server.py"
      ],
      "timeout": 1800,
      "disabled": false
    }
  }
}
```

### 2. 配置说明

- **服务器名称**: `ida-pro-mcp`
- **命令路径**: 使用项目虚拟环境中的Python
- **脚本路径**: IDA Pro MCP服务器脚本
- **超时时间**: 30分钟（1800秒）
- **状态**: 启用

### 3. 前置条件

在使用IDA Pro MCP之前，请确保：

1. **IDA Pro已安装并运行**
   ```bash
   # 启动IDA Pro并加载二进制文件
   ```

2. **MCP插件已安装**
   ```bash
   ida-pro-mcp --install
   ```

3. **IDA插件正在运行**
   - 在IDA Pro中：Edit -> Plugins -> MCP
   - 确保插件在端口13337上监听

### 4. 可用功能 (50个工具函数)

#### 🔗 连接与元数据
- `get_metadata` - 获取二进制文件信息

#### 🔍 函数分析 (9个)
- `get_function_by_name` - 按名称查找函数
- `get_function_by_address` - 按地址获取函数
- `decompile_function` - 反编译函数
- `disassemble_function` - 反汇编函数
- `list_functions` - 列出所有函数
- 等等...

#### 💾 内存操作 (6个)
- `read_memory_bytes` - 读取内存字节
- `data_read_byte/word/dword/qword` - 读取不同大小数据
- `data_read_string` - 读取字符串

#### 🔧 变量管理 (11个)
- `rename_local_variable` - 重命名局部变量
- `set_global_variable_type` - 设置全局变量类型
- `get_stack_frame_variables` - 获取栈变量
- 等等...

#### 📋 数据列表 (6个)
- `list_strings` - 列出字符串
- `list_imports` - 列出导入函数
- `list_globals` - 列出全局变量
- 等等...

#### ⚠️ 调试功能 (10个，需要--unsafe标志)
- `dbg_get_registers` - 获取寄存器值
- `dbg_set_breakpoint` - 设置断点
- 等等...

### 5. 使用示例

配置完成后，您可以在Augment中使用这些工具：

```
请分析当前IDA中加载的二进制文件的主要函数
```

```
帮我反编译地址0x401000处的函数
```

```
列出所有包含"password"的字符串
```

### 6. 故障排除

如果连接失败：

1. **检查IDA Pro是否运行**
2. **确认MCP插件已加载**
3. **验证端口13337是否可用**
4. **检查防火墙设置**

### 7. 高级配置

如果需要使用不安全功能（调试），可以修改配置：

```json
{
  "mcpServers": {
    "ida-pro-mcp-unsafe": {
      "command": "/mnt/persist/workspace/.venv/bin/python3",
      "args": [
        "/mnt/persist/workspace/src/ida_pro_mcp/server.py",
        "--unsafe"
      ],
      "timeout": 1800,
      "disabled": false
    }
  }
}
```

## 🎯 配置完成

配置完成后，您将拥有50个强大的逆向工程工具，可以通过Augment AI助手进行智能化的二进制分析！
