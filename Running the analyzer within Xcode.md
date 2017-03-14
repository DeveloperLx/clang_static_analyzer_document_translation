#### [原文地址](http://clang-analyzer.llvm.org/xcode.html) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div id="content">
    <h1>
    	在Xcode中运行分析
    </h1>
    <table style="margin-top:0px" width="100%" border="0" cellpadding="0px"
    cellspacing="0">
        <tbody>
            <tr>
                <td>
                    <h3>
                        这是什么？
                    </h3>
                    <p>
                        从Xcode3.2起，用户就可以直接在Xcode中运行Clang静态分析器了（
                        <a href="https://developer.apple.com/library/ios/recipes/xcode_help-source_editor/chapters/Analyze.html#//apple_ref/doc/uid/TP40009975-CH4-SW1">
                            官方文档
                        </a>
                        ）。
                    </p>
                    <p>
                        它直接与Xcode的build系统整合，并直接在Xcode的编辑器中展示分析结果。
                    </p>
                    <h3>
                        我是否可以在Xcode中使用开源的分析器build？
                    </h3>
                    <p>
                        <b>
                            是的
                        </b>
                        。说明就包含在下面。
                    </p>
                </td>
                <td style="padding-left:10px; text-align:center">
                    <a href="http://clang-analyzer.llvm.org/images/analyzer_xcode.png">
                        <img src="http://clang-analyzer.llvm.org/images/analyzer_xcode.png" width="620px" alt="analyzer in xcode">
                    </a>
                    <br>
                    <b>
                        在Xcode中查看静态分析的结果
                    </b>
                </td>
            </tr>
        </tbody>
    </table>
    <h3>
        关键特性：
    </h3>
    <ul>
        <li>
            <b>
                整合工作流：
            </b>
            结果被整合在Xcode中。这里没有使用单独的工具的经验，并且激活分析器需要一个单一的按键或鼠标点击。
        </li>
        <li>
            <b>
                透明度：
            </b>
            轻松地（effortlessly）与Xcode项目工作（包括iPhone项目）。
        </li>
        <li>
            <b>
                缺点（Cons）：
            </b>
            不能在非Xcode的项目上很好地工作。对于那些，考虑使用
            <a href="http://clang-analyzer.llvm.org/scan-build.html">
                <b>
                    scan-build
                </b>
            </a>
            .
        </li>
    </ul>
    <h2>
        开始吧！
    </h2>
    <p>
        Xcode可以从苹果的
        <a href="https://itunes.apple.com/us/app/xcode/id497799835?mt=12">
            Mac App Store
        </a>
        免费下载，参考
        <a href="https://developer.apple.com/library/ios/recipes/xcode_help-source_editor/chapters/Analyze.html#//apple_ref/doc/uid/TP40009975-CH4-SW1">
            可用的说明
        </a>
        来使用分析器。
    </p>
    <h2>
        在Xcode中使用开源的分析器build
    </h2>
    <p>
        默认地，Xcode使用绑定的
        <tt>
            clang
        </tt>
        的版本来分析你的代码。当为了编译项目，继续使用Xcode绑定的
        <tt>
            clang
        </tt>
        ，是有可能通过替换
        <tt>
            clang
        </tt>
        的版本来改变Xcode的行为的。
    </p>
    <h3>
        为什么要尝试开源的build？
    </h3>
    <p>
        使用开源分析器（这个网站提供的）build的优点，是它总是可以比Xcode自身提供的更新，因此，可以包含修复bug，新的检测，或简单更好的分析。
    </p>
    <p>
        另一方面，新的检测可以用易变的质量的结果来进行实验。用户是被鼓励去
        <a href="http://clang-analyzer.llvm.org/filing_bugs.html">
            归档bug报告
        </a>
        （对于任何版本的分析器），无论他们遇到了错误的报告还是其它的问题。
    </p>
    <h3>
        set-xcode-analyzer
    </h3>
    <p>
        从分析器build checker-234开始，分析器的build包含一个叫做
        <tt>
            set-xcode-analyzer
        </tt>
        的命令行工具，让用户可以改变Xcode用来分析的
        <tt>
            clang
        </tt>
        的副本：
    </p>
    <pre class="code_example">$ <b>set-xcode-analyzer -h</b>
用法：set-xcode-analyzer [options]

选项：
  -h, --help            展示这个的帮助信息并退出
  --use-checker-build=PATH
                        使用位于提供的绝对路径的Clang
                        Use the Clang located at the provided absolute path,
                        例如：/Users/foo/checker-1
  --use-xcode-clang     使用打包在Xcode中的Clang
</pre>
    <p>
        在操作上，
        <b>
            set-xcode-analyzer
        </b>
        编辑了Xcode的配置文件，来让它使用你指定的用来进行静态分析的
        <tt>
            clang
        </tt>
        的版本。在这个模型中，它提供给你两种基本的模式：
    </p>
    <ul>
        <li>
            <b>
                --use-xcode-clang
            </b>
            ：切换Xcode（回）去使用
            <tt>
                clang
            </tt>
            捆绑的用来静态分析的
            <tt>
                clang
            </tt>
            。
        </li>
        <li>
            <b>
                --use-checker-build
            </b>
            ：切换为通过由指定的分析器build提供的
            <tt>
                clang
            </tt>
            。
        </li>
    </ul>
    <h4>
        要记住的事
    </h4>
    <ul>
        <li>
            你应当优先运行
            <tt>
                set-xcode-analyzer
            </tt>
            来退出Xcode。
        </li>
        <li>
            为了获取写的权利来修改Xcode配置文件，你要在
            <b>
                <tt>
                    sudo
                </tt>
            </b>
            下运行
            <tt>
                set-xcode-analyzer
            </tt>
            。
        </li>
    </ul>
    <h4>
        例子
    </h4>
    <p>
        <b>
            Example 1
        </b>
        : Telling Xcode to use checker-235:
    </p>
    <pre class="code_example">$ <b>set-xcode-analyzer -h</b>
Usage: set-xcode-analyzer [options]

Options:
  -h, --help            show this help message and exit
  --use-checker-build=PATH
                        Use the Clang located at the provided absolute path,
                        e.g. /Users/foo/checker-1
  --use-xcode-clang     Use the Clang bundled with Xcode
</pre>
    <p>
        Note that you typically won't install an analyzer build in
        <tt>
            /tmp
        </tt>
        , but the point of this example is that
        <tt>
            set-xcode-analyzer
        </tt>
        just wants a full path to an untarred analyzer build.
    </p>
    <p>
        <b>
            Example 2
        </b>
        : Telling Xcode to use a very specific version of
        <tt>
            clang
        </tt>
        :
    </p>
    <pre class="code_example">$ sudo set-xcode-analyzer --use-checker-build=~/mycrazyclangbuild/bin/clang
</pre>
    <p>
        <b>
            Example 3
        </b>
        : Resetting Xcode to its default behavior:
    </p>
    <pre class="code_example">$ sudo set-xcode-analyzer --use-xcode-clang</pre>
</div>
