# Changelog

## [1.10.2] - 2026-02-27

### Fixed

- 修复偶发的 `null is not an object (evaluating 'd$.content')` 错误。当代理无法连接上游 API（超时、断连等）时，返回的错误响应格式不符合 Anthropic API 规范，导致客户端无法正确解析。现在错误响应统一使用 Anthropic 标准格式 `{"type": "error", "error": {"type": "...", "message": "..."}}`。

## [1.10.1] - 2026-02-27

### Fixed

- 修复偶发的 `ZlibError` 错误。当上游 API 返回 gzip/deflate 压缩响应时，httpx 的 `aiter_bytes()` 会自动解压响应体，但代理原封不动透传了 `Content-Encoding` 头给客户端，导致客户端对已解压的数据尝试二次解压而报错。现在在响应头中剔除 `content-encoding`、`content-length`、`transfer-encoding` 三个头，避免客户端与代理之间的编码不一致。

## [1.10.0] - 2026-02-25

### Changed

- 基于 [guojinpeng/cli_proxy](https://github.com/guojinpeng/cli_proxy) v1.9.5 改造
- 规范化项目结构，采用标准 Python 打包方式（pyproject.toml）
- 适配最新版本 Claude Code，修复原项目兼容性问题
- 新增 Docker 部署支持
- 新增 Codex 代理支持
- 完善文档和使用说明
