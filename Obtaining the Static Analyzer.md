#### [原文地址](http://clang-analyzer.llvm.org/installation) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)


<div id="content">
    <h1>
        获取静态分析器
    </h1>
    <p>
        这页描述了怎么去下载和安装分析器。一旦分析器安装上了，跟随
        <a href="http://clang-analyzer.llvm.org/scan-build.html">
            说明
        </a>
        来使用
        <tt>
            scan-build
        </tt>
        去启动分析你的代码。
    </p>
    <h2>
        打包build（Mac OS X）
    </h2>
    <p>
        这个分析器半正则（Semi-regular）、预建的（pre-built）二进制文件（binaries）在Mac OS上可用。这些被build去执行在OS X 10.7和之后的版本上。
    </p>
    <p>
        Build会频繁地发布。通常在不同的build号之间会有一些bug的修复或小幅的特性提升。当使用分析器的时候，我们推荐你偶尔地回来检查一下新的build，尤其你使用的build已经过了有几周的时间。
    </p>
    <p>
        最近一次的build是：
        <!--#include virtual="latest_checker.html.incl"-->
    </p>
    <p>
        对于其它平台的打包builds可能会在最后提供，但我们需要有意愿提供这样常规的build的志愿者。如果你希望帮助提供在其它平台上的分析器的常规的的build，请发邮件到
        <a href="http://lists.llvm.org/mailman/listinfo/cfe-dev">
            Clang Developers' mailing list
        </a>
        。
    </p>
    <h3>
        使用打包builds
    </h3>
    <p>
        为了使用打包的build，在任意位置解包它即可。如果这个build存档的名字为
        <b>
            <tt>
                checker-XXX.tar.bz2
            </tt>
        </b>
        ，之后这个归档将扩展为一个名叫
        <b>
            <tt>
                checker-XXX
            </tt>
        </b>
        的目录。你不需要放置这个目录或目录中的内容到特定的地方。卸载这个分析器就像删除这个目录一样地简单。
    </p>
    <p>
        在
        Most of the files in the
        <b>
            <tt>
                checker-XXX
            </tt>
        </b>
        目录中的大多数文件将是分析器的支持文件，你可以简单地忽略掉它们。大多数用户只需关心两个文件，它们在
        <b>
            <tt>
                checker-XXX
            </tt>
        </b>
        目录的顶层位置下：
    </p>
    <ul>
        <li>
            <b>
                scan-build
            </b>
            ：
            <tt>
                scan-build
            </tt>
            是一个执行分析器的高级的命令行工具
        </li>
        <li>
            <b>
                scan-view
            </b>
            ：
            <tt>
                scan-view
            </tt>
            是一个陪伴
            <tt>
                scan-build
            </tt>
            的命令行工具，用来查看
            <tt>
                scan-build
            </tt>
            生成的分析结果。这里有一个可以传递给
            <tt>
                scan-build
            </tt>
            的选项，它使得当一个build的分析完成时，立刻执行
            <tt>
                scan-view
            </tt>
            。
        </li>
    </ul>
    <h4>
        执行scan-build
    </h4>
    <p>
        对于使用
        <tt>
            scan-build
        </tt>
        的特定细节，请查看
        <tt>
            scan-build
        </tt>
        的
        <a href="http://clang-analyzer.llvm.org/scan-build">
            文档
        </a>
        。
    </p>
    <p>
        To run
        <tt>
            scan-build
        </tt>
        , either add the
        <b>
            <tt>
                checker-XXX
            </tt>
        </b>
        directory to your path or specify a complete path for
        <tt>
            scan-build
        </tt>
        when running it. It is also possible to use a symbolic link to
        <tt>
            scan-build
        </tt>
        , such one located in a directory in your path. When
        <tt>
            scan-build
        </tt>
        runs it will automatically determine where to find its accompanying files.
    </p>
    <h2 id="OtherPlatforms">
        Other Platforms (Building the Analyzer from Source)
    </h2>
    <p>
        For other platforms, you must build Clang and LLVM manually. To do so,
        please follow the instructions for
        <a href="http://clang.llvm.org/get_started.html#build">
            building Clang from source code
        </a>
        .
    </p>
    <p>
    </p>
    <p>
        Once the Clang is built, you need to add the following to your path:
    </p>
    <ul>
        <li>
            The location of the
            <tt>
                clang
            </tt>
            binary.
            <p>
                For example, if you built a
                <em>
                    Debug+Asserts
                </em>
                build of LLVM/Clang (the default), the resultant
                <tt>
                    clang
                </tt>
                binary will be in
                <tt>
                    $(OBJDIR)/Debug+Asserts/bin
                </tt>
                (where
                <tt>
                    $(OBJDIR)
                </tt>
                is often the same as the root source directory). You can also do
                <tt>
                    make install
                </tt>
                to install the LLVM/Clang libraries and binaries to the installation directory
                of your choice (specified when you run
                <tt>
                    configure
                </tt>
                ).
            </p>
        </li>
        <li>
            The locations of the
            <tt>
                scan-build
            </tt>
            and
            <tt>
                scan-view
            </tt>
            programs.
            <p>
                These are installed via
                <tt>
                    make install
                </tt>
                into the bin directory when clang is built.
            </p>
        </li>
    </ul>
</div>
