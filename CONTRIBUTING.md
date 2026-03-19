# 贡献指南

感谢你对 OpenNovel 的兴趣！我们欢迎所有形式的贡献。

## 🤔 如何贡献

### 报告 Bug

如果你发现了 Bug，请通过 [GitHub Issues](https://github.com/jcy321/opennovel-hub/issues) 提交，并包含：

- 问题的详细描述
- 复现步骤
- 期望行为与实际行为
- 环境信息（操作系统、Rust 版本等）

### 提出新功能

我们欢迎功能建议！请在 Issue 中详细描述：

- 功能的使用场景
- 预期的实现方式
- 与现有功能的关联

### 提交代码

1. Fork 对应的仓库
2. 创建功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'feat: add amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 创建 Pull Request

## 📝 代码规范

### Rust 代码

- 使用 `cargo fmt` 格式化代码
- 使用 `cargo clippy` 检查代码质量
- 为公共 API 编写文档注释
- 新功能需要添加测试

### 提交信息

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

- `feat:` 新功能
- `fix:` Bug 修复
- `docs:` 文档更新
- `refactor:` 代码重构
- `test:` 测试相关
- `chore:` 构建/工具相关

## 🏗️ 开发环境设置

```bash
# 克隆仓库
git clone https://github.com/jcy321/opennovel-core.git
cd opennovel-core

# 安装依赖并构建
cargo build

# 运行测试
cargo test

# 运行服务
cargo run -p opennovel-web
```

## 📋 仓库说明

| 仓库 | 内容 | 贡献方式 |
|------|------|----------|
| opennovel-core | 后端服务 | 提交 PR 到私有仓库 |
| opennovel-web | Web 前端 | 提交 PR 到公开仓库 |
| opennovel-ide | IDE 客户端 | 提交 PR 到公开仓库 |
| opennovel-hub | 项目主页 | 提交 PR 到公开仓库 |

## 🙏 感谢

每一位贡献者都是 OpenNovel 大家庭的一员！