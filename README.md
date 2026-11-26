# PythonQuest · Python 学习实验室

一个可以上传 GitHub Pages 的纯静态 Python 学习网站。界面和交互沿用 JavaQuest 的结构：闯关、剧情、Python 主线、自由编程、经典题单、每日挑战、Boss Rush、成就和本地进度。

## 内容

| 模式 | 内容 |
| --- | --- |
| 闯关模式 | 10 章 × 5 关，共 50 个 Python 教程关卡 |
| 经典题单 | 20 道 Python 面试 / 算法题，单独成章 |
| 剧情模式 | 10 个分支故事，每个 6 个结局，共 60 个结局 |
| Python 主线 | 50 关单线剧情《蛇之书》，唯一好结局 |
| 自由编程 | 浏览器内 Python 工作台，支持标准输入 |
| 复习玩法 | 每日挑战、Boss Rush、支线小测、成就、宠物 |

所有课程、剧情和代码都打包在 `web/data.js` 中，断网也能打开课程。Python 代码由随站点打包的 **Skulpt** 在浏览器里执行，不使用 WasmGC、后端或第三方 CDN。

## 目录

```text
.
├─ .github/workflows/pages.yml   # GitHub Pages 自动部署
├─ web/
│  ├─ index.html
│  ├─ app.js
│  ├─ styles.css
│  ├─ data.js                    # 内嵌课程、故事、主线数据
│  ├─ data/                      # 同一份数据的 JSON，便于编辑
│  ├─ vendor/
│  │  ├─ skulpt/                 # Python 解释器（自托管）
│  │  └─ codemirror/             # 编辑器（自托管）
│  ├─ guide.html
│  └─ .nojekyll
└─ README.md
```

## 部署到 GitHub Pages

### 方式 A：上传整个目录（推荐）

1. 新建一个 GitHub 仓库。
2. 解压本包，把 `web/`、`.github/`、`README.md` 放到仓库根目录。
3. 打开 `Settings → Pages`，把 `Build and deployment → Source` 设为 **GitHub Actions**。
4. 打开 `Actions`，等待 `Deploy PythonQuest Web` 变绿。
5. 访问：
   ```text
   https://你的用户名.github.io/仓库名/
   ```

### 方式 B：只上传 zip

1. 把 `PythonQuest-Web.zip` 上传到仓库根目录。
2. 仍然需要把 `.github/workflows/pages.yml` 上传到仓库；工作流会自动解压 zip。
3. 同样在 `Settings → Pages` 选择 **GitHub Actions**。

> GitHub 网页上传多个带子目录的文件时，建议使用 GitHub Desktop、`git`，或先上传 zip 让 Actions 解压，避免把 `vendor/skulpt` 等目录压平。

## 本地预览

不要直接双击 `index.html`。用本地 HTTP 服务：

```bash
cd web
python -m http.server 8000
```

然后打开：

```text
http://localhost:8000/
```

## 运行环境说明

- **Skulpt 1.2.0**：浏览器内 Python 3 教学子集，不是完整 CPython。
- 支持：变量、字符串、列表、元组、字典、集合、条件、循环、函数、类、继承、异常、推导式、生成器、常用标准库。
- 不支持：`pip`、任意第三方包、完整文件系统、多线程、`asyncio`、网络库。
- `input()` 使用运行前填写的“标准输入”，不是真正的终端交互。
- 进度保存在浏览器 `localStorage`，换设备或清缓存会丢失。

## 修改课程

课程在 `web/data/lessons.json` 和 `web/data/stories.json`，主线在 `web/data/python_story.json`。修改后重新生成内嵌数据：

```bash
python build/gen_datajs.py
```

构建脚本和内容生成脚本放在 `build/`，不是网站运行所需文件。

## 第三方组件

- Skulpt — MIT License
- CodeMirror 5 — MIT License
- 字体使用系统字体，不额外下载。

## License

MIT
