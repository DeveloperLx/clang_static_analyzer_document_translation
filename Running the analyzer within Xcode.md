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
        By default, Xcode uses the version of
        <tt>
            clang
        </tt>
        that came bundled with it to analyze your code. It is possible to change
        Xcode's behavior to use an alternate version of
        <tt>
            clang
        </tt>
        for this purpose while continuing to use the
        <tt>
            clang
        </tt>
        that came with Xcode for compiling projects.
    </p>
    <h3>
        Why try open source builds?
    </h3>
    <p>
        The advantage of using open source analyzer builds (provided on this website)
        is that they are often newer than the analyzer provided with Xcode, and
        thus can contain bug fixes, new checks, or simply better analysis.
    </p>
    <p>
        On the other hand, new checks can be experimental, with results of variable
        quality. Users are encouraged to
        <a href="http://clang-analyzer.llvm.org/filing_bugs.html">
            file bug reports
        </a>
        (for any version of the analyzer) where they encounter false positives
        or other issues.
    </p>
    <h3>
        set-xcode-analyzer
    </h3>
    <p>
        Starting with analyzer build checker-234, analyzer builds contain a command
        line utility called
        <tt>
            set-xcode-analyzer
        </tt>
        that allows users to change what copy of
        <tt>
            clang
        </tt>
        that Xcode uses for analysis:
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
        Operationally,
        <b>
            set-xcode-analyzer
        </b>
        edits Xcode's configuration files to point it to use the version of
        <tt>
            clang
        </tt>
        you specify for static analysis. Within this model it provides you two
        basic modes:
    </p>
    <ul>
        <li>
            <b>
                --use-xcode-clang
            </b>
            : Switch Xcode (back) to using the
            <tt>
                clang
            </tt>
            that came bundled with it for static analysis.
        </li>
        <li>
            <b>
                --use-checker-build
            </b>
            : Switch Xcode to using the
            <tt>
                clang
            </tt>
            provided by the specified analyzer build.
        </li>
    </ul>
    <h4>
        Things to keep in mind
    </h4>
    <ul>
        <li>
            You should quit Xcode prior to running
            <tt>
                set-xcode-analyzer
            </tt>
            .
        </li>
        <li>
            You will need to run
            <tt>
                set-xcode-analyzer
            </tt>
            under
            <b>
                <tt>
                    sudo
                </tt>
            </b>
            in order to have write privileges to modify the Xcode configuration files.
        </li>
    </ul>
    <h4>
        Examples
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
