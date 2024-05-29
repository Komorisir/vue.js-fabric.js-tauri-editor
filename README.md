# 基于 vue.js + fabric.js + tauri 的图片编辑器

### Project setup

```
npm set registry https://registry.npmmirror.com
npm install
```

### Complies and hot-reloads for development

```
npm run dev
// 或者在tauri框架下开发
npm run tauri dev
```

### Complies and minifies for production

```
npm run build
// 打包成桌面应用
npm run tauri build
```

### lints and fixes files

```
npm run lint
```

## 代码提交规范

提交 commit 的类型：

- build: 影响构建系统或外部依赖关系的更改(示例范围:gulp、broccoli、npm、webpack)
- chore: 不修改 src 或测试文件的其他更改
- revert: 还原以前的提交
- feat: 新功能
- fix: 修复问题
- docs: 修改文档
- style: 修改代码格式(空格、换行、分号等)，不影响代码逻辑
- refactor: 重构代码（既不是修复 bug，也不是增加新特性），理论上不影响现有功能
- test: 增加修改测试用例
