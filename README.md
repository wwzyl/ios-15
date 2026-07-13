# CBrain iOS

这是 CBrain 的 iOS 原生 SwiftUI 工程。GitHub 网页端不能直接上传文件夹时，推荐使用源码 zip 输入、Actions artifact 输出的构建方式。

## GitHub 网页端构建

1. 在电脑上压缩整个源码文件夹。
2. 建议把压缩包命名为 `cbrain-ios-source.zip`。
3. 也可以使用 `cbrain ios.zip`，workflow 会自动识别。
4. 把这个源码 zip 上传到 GitHub 仓库根目录。
5. 打开 `Actions`，运行 `Build iOS IPA`。
6. 下载 artifact：`UNZIP-FIRST-CBrainIOS-installables`。
7. 先解压 GitHub 下载下来的 artifact zip。
8. 用 TrollStore 安装解压后里面的 `CBrainIOS.tipa`。

不要安装这些文件：

- 源码 zip，例如 `cbrain-ios-source.zip` 或 `cbrain ios.zip`
- GitHub 下载下来的 artifact 外层 zip
- 解压出来的 `Payload` 文件夹
- 旧的本地 `CBrainIOS.ipa` 或 `CBrainIOS.tipa`

workflow 上传前会验证安装包里有这些路径：

```text
Payload/CBrainIOS.app/Info.plist
Payload/CBrainIOS.app/CBrainIOS
Payload/CBrainIOS.app/_CodeSignature/CodeResources
```

如果这些路径缺失，构建会失败，而不是上传一个 TrollStore 解析不了的包。

## 知识库格式

选择的知识库文件夹需要直接包含：

- `graph.json`
- `notes`
- 可选：`modifys` 或 `modifys.json`

iOS 版会把选中的知识库复制到 App 的 Documents 目录：

```text
CBrain Library
```

编辑保存会写入这个 App 内部副本。从 S3 全量下载时，也会写入同一个 App 内部目录。
