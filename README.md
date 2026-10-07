# artop-java-bin

Java 版 **ARTOR** 运行时的预置二进制归档，供无需登录 artop.org 的环境直接取用。

## 内容

| 项 | 值 |
|---|---|
| 发行版 | ARTOR 4.13（`4.13.0.201912171516`） |
| 基底 | Eclipse 4.13（2019-09），Sphinx 0.11.2 |
| 构建时间 | 2019-12-17 |
| Java 要求 | **Java 8**（JavaSE-1.8） |
| 体积 | 约 270 MB，753 个文件（最大单文件约 25.6 MB） |

目录结构（Eclipse RCP 布局）：

- `plugins/` — 490 个 plugin jar，含全部 `org.artop.*`、`org.eclipse.emf.*`、`org.eclipse.sphinx.*`
- `features/` — 204 个 feature
- `p2/`、`configuration/`、`dropins/`、`readme/`
- `artop.ini`、`artifacts.xml`、`.eclipseproduct`、Windows 启动器 `artop.exe` / `eclipsec.exe`

## 用途

`artop-rust` 仓库用它做 **Rust ↔ Java ARTOR 互操作回归**与三方性能对比（Rust / C++ / Java）。
参见 `artop-rust/docs/PROGRESS.md` §10。

## 用法

不需要 OSGi/Eclipse 启动，直接把 `plugins/*.jar` 全部放进 classpath 即可：

```bash
# 编译 Java 基准/互操作入口（源码在 artop-cpp/benchmark/java/）
javac -cp "$ARTOR/plugins/*" -d classes ArxmlBenchmark.java

# 运行
java -Xmx3g -cp "classes:$ARTOR/plugins/*" artop.demo.ArxmlBenchmark in.arxml out.arxml 3
```

`$ARTOR` 指向本仓库 clone 下来的根目录。

## 来源

原为 artop.org 的注册用户下载包（Artop Technology Demonstrator，Java 8 版），
归档于此以便复现，无需再访问 artop.org。