{% if os == 'linux' -%}
  {% assign unzip = 'tar xf' -%}
  {% assign file_ext = '.tar.xz' -%}
{% else -%}
  {% assign unzip = 'unzip' -%}
  {% assign file_ext = '.zip' -%}
{% endif -%}

## Get the Flutter SDK {#get-sdk}

## 获取 Flutter SDK {#get-sdk}


 1. Download the following installation bundle to get the latest
    {{site.sdk.channel}} release of the Flutter SDK:

    下载以下安装包来获取最新的 {{site.sdk.channel}} Flutter SDK：

    [(loading...)](#){:.download-latest-link-{{os}}.btn.btn-primary}

    For other release channels, and older builds,
    see the [SDK releases][] page.

    想要获取到其他版本的安装包，请参阅 [SDK 版本列表][SDK releases] 页面。

 1. Extract the file in the desired location, for example:

    将文件解压到目标路径, 比如:

    {% comment %}
      Our JS also updates the filename in this template, but it doesn't include the terminal formatting:

      {% prettify shell %}
      $ cd ~/development
      $ {{unzip}} ~/Downloads/[[download-latest-link-filename]]flutter_{{os}}_vX.X.X-{{site.sdk.channel}}{{file_ext}}[[/end]]
      {% endprettify %}
    {% endcomment -%}

    ```terminal
    $ cd ~/development
    $ {{unzip}} ~/Downloads/flutter_{{os}}_vX.X.X-{{site.sdk.channel}}{{file_ext}}
    ```
    
    If you don't want to install a fixed version of the installation bundle, 
    you can skip steps 1 and 2. 
    Instead, get the source code from the [Flutter repo][]
    on GitHub with the following command:
    
    如果你不想安装固定版本的安装包，你可以跳过步骤 1 和 2。
    或者是从 GitHub 上的 [Flutter repo][] 获取源代码，
    并根据需要更改分支或标签。
    
    ```terminal
    $ git clone https://github.com/flutter/flutter.git
    ```
    
    You can also change branches or tags as needed.
    For example, to get just the stable version:
    
    你也可以根据需要切换选择分支，比如用下面的参数获得稳定版本：
    
    ```terminal
    $ git clone https://github.com/flutter/flutter.git -b stable --depth 1
    ```

 1. Add the `flutter` tool to your path:

    配置 `flutter` 的 PATH 环境变量：

    ```terminal
    $ export PATH="$PATH:`pwd`/flutter/bin"
    ```

    This command sets your `PATH` variable for the
    _current_ terminal window only.
    To permanently add Flutter to your path, see
    [Update your path][].

    这个命令配置了 `PATH` 环境变量，且只会在你 **当前** 命令行窗口中生效。
    如果想让它永久生效，请查看 [更新 PATH 环境变量][Update your path]。
    
 4. Optionally, pre-download development binaries:
    
    开发二进制文件预下载（可选操作）

    The `flutter` tool downloads platform-specific development binaries as
    needed. For scenarios where pre-downloading these artifacts is preferable
    (for example, in hermetic build environments,
    or with intermittent network availability), iOS
    and Android binaries can be downloaded ahead of time by running:
    
    `flutter` 命令行工具会下载不同平台的开发二进制文件，
    如果需要一个封闭式的构建环境，
    或在网络可用性不稳定的情况下使用等情况，
    你可能需要通过下面这个命令预先下载
    iOS 和 Android 的开发二进制文件：


    ```terminal
    $ flutter precache
    ```

    For additional download options, see `flutter help precache`.
    
    更多使用方式，请使用 `flutter help precache` 命令查看。

You are now ready to run Flutter commands!

现在你可以愉快地运行 Flutter 的命令行啦！


{{site.alert.note}}

  To update an existing version of Flutter, see
  [Upgrading Flutter][].
  
  如果想要升级当前的 Flutter 版本，可以查看 [升级 Flutter][Upgrading Flutter]。

{{site.alert.end}}


### Run flutter doctor

### 运行 flutter doctor 命令


Run the following command to see if there are any dependencies you need to
install to complete the setup (for verbose output, add the `-v` flag):

通过运行以下命令来查看当前环境是否需要安装其他的依赖
（如果想查看更详细的输出，增加一个 `-v` 参数即可）：

```terminal
$ flutter doctor
```

This command checks your environment and displays a report to the terminal
window. The Dart SDK is bundled with Flutter; it is not necessary to install
Dart separately. Check the output carefully for other software you might
need to install or further tasks to perform (shown in **bold** text).

这个命令会检查你当前的配置环境，并在命令行窗口中生成一份报告。
安装 Flutter 会附带安装 Dart SDK，所以不需要再对 Dart 进行单独安装。
你需要仔细阅读上述命令生成的报告，看看别漏了一些需要安装的依赖，
或者需要之后执行的命令（这个会以 **加粗的文本** 显示出来）。

For example:

比如你可能会看到下面这样的输出：

<pre>
[-] Android toolchain - develop for Android devices
    • Android SDK at /Users/obiwan/Library/Android/sdk
    <strong>✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ</strong>
    • Try re-installing or updating your Android SDK,
      visit https://flutter.dev/setup/#android-setup for detailed instructions.
</pre>

The following sections describe how to perform these tasks and finish the setup
process.

之后的部分会向你描述如果执行这些命令来完成整体的配置过程。

Once you have installed any missing dependencies, run the `flutter doctor`
command again to verify that you’ve set everything up correctly.

当你安装了任一缺失部分的依赖后，
可以再次运行 `flutter doctor` 命令来确认是否成功安装。

### Downloading and installing with Homebrew

### 使用 Homebrew 下载和安装

If you have Homebrew installed on your machine,
you can install Flutter using the following command:

如果你的设备安装了 Homebrew，你可以使用下面的命令安装 Flutter：

```terminal
$ brew install --cask flutter
```

Then, run `flutter doctor`. That lets you know if there are
other dependencies you need to install to use Flutter, such as the Android SDK.

接着运行 `flutter doctor`，查看是否有其他 Flutter 依赖需要下载，
例如 Android SDK。

### Downloading straight from GitHub instead of using an archive

### 直接从 Github 上（而不是归档）下载

_This is only suggested for advanced use cases._

**该建议仅适用于高级用例**

You can also use git directly instead of downloading the prepared archive. For example,
to download the stable branch:

你也可以不从归档，而是用 Git 直接下载。
例如，可以运行下方的命令，以下载稳定分支的 SDK：
    
```terminal
$ git clone https://github.com/flutter/flutter.git -b stable
```

[Update your path][], and run `flutter doctor`. That will let you know if there are
other dependencies you need to install to use Flutter (e.g. the Android SDK).

[更新环境变量][Update your path]，并运行 `flutter doctor`。
这个命令将会告诉你，是否还缺少运行 Flutter 所需要安装的其他依赖项（例如 Android SDK）。

If you did not use the archive, Flutter will download necessary development binaries as they
are needed (if you used the archive, they are included in the download). You may wish to
pre-download these development binaries (for example, you may wish to do this when setting
up hermetic build environments, or if you only have intermittent network availability). To
do so, run the following command:

如果你不使用归档，Flutter 将会下载必要的开发二进制文件（如果你使用的归档，那么这些文件已经包含在内了）。
你也许会想要提前下载这些开发二进制文件（例如，您可能希望设置系统构建环境，或是您的网络可用性不佳）。
那么你可以运行以下命令：

```terminal
$ flutter precache
```

For additional download options, see `flutter help precache`.

更多额外下载选项，请参阅 `flutter help precache`。

{% include_relative _analytics.md %}

[Flutter repo]: {{site.github}}/flutter/flutter
[Installing snapd]: https://snapcraft.io/docs/installing-snapd
[SDK releases]: /docs/development/tools/sdk/releases
[Snap Store]: https://snapcraft.io/store
[snapd]: https://snapcraft.io/flutter
[Update your path]: #update-your-path
[Upgrading Flutter]: /docs/development/tools/sdk/upgrading
