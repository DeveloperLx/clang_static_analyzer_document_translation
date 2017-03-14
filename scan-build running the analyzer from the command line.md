# scan-build: 从命令行中运行分析器
---
#### [原文地址](http://clang-analyzer.llvm.org/scan-build.html) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div id="content">
    <table style="margin-top:0px" width="100%" cellpadding="0px" cellspacing="0">
        <tbody>
            <tr>
                <td>
                    <h3>
                        它是什么？
                    </h3>
                    <p>
                        <b>
                            scan-build
                        </b>
                        是一个命令行的工具，让用户能够在它们的代码库上运行静态分析，作为正常build的一部分（从命令行）。
                    </p>
                    <h3>
                        它怎么工作？
                    </h3>
                    <p>
                        在项目build期间，当源文件被编译的时候，也通过静态分析器串联了分析。
                    </p>
                    <p>
                        当build完成后，结果会在一个web浏览器中展示给用户。
                    </p>
                    <h3>
                        它在任何build系统下都能工作么？
                    </h3>
                    <p>
                        <b>
                            scan-build
                        </b>
                        对于你怎么build你的code了解得很少。它通过覆盖
                        <tt>
                            CC
                        </tt>
                        和
                        <tt>
                            CXX
                        </tt>
                        环境下的变量，来（有希望地）改变你的build去使用一个“假的”编译器，来替换那个能够正常build你的项目的以工作。这个假编译器执行
                        <tt>
                            clang
                        </tt>
                        或
                        <tt>
                            gcc
                        </tt>
                        （依赖于平台）来编译你的代码，然后执行静态分析去分析你的代码。
                    </p>
                    <p>
                        这个”穷人的干涉“的工作在很多的情况下令人惊奇得好，其它失败。请在这页查阅关于最好地使用
                        <b>
                            scan-build
                        </b>
                        的信息，它包含当前面提到的hack工作失败时该怎么办。
                    </p>
                </td>
                <td style="padding-left:10px; text-align:center">
                    <img src="http://clang-analyzer.llvm.org/images/scan_build_cmd.png" width="450px" alt="scan-build">
                    <br>
                    <a href="http://clang-analyzer.llvm.org/images/analyzer_html.png">
                        <img src="http://clang-analyzer.llvm.org/images/analyzer_html.png" width="450px" alt="analyzer in browser">
                    </a>
                    <br>
                    <b>
                        在web浏览器中查看静态分析的结果
                    </b>
                </td>
            </tr>
        </tbody>
    </table>
    <h2>
        内容
    </h2>
    <ul>
        <li>
            <a href="#scanbuild">
                Getting Started
            </a>
            <ul>
                <li>
                    <a href="#scanbuild_basicusage">
                        Basic Usage
                    </a>
                </li>
                <li>
                    <a href="#scanbuild_forwindowsusers">
                        For Windows Users
                    </a>
                </li>
                <li>
                    <a href="#scanbuild_otheroptions">
                        Other Options
                    </a>
                </li>
                <li>
                    <a href="#scanbuild_output">
                        Output of scan-build
                    </a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#recommendedguidelines">
                Recommended Usage Guidelines
            </a>
            <ul>
                <li>
                    <a href="#recommended_debug">
                        Always Analyze a Project in its "Debug" Configuration
                    </a>
                </li>
                <li>
                    <a href="#recommended_verbose">
                        Use Verbose Output when Debugging scan-build
                    </a>
                </li>
                <li>
                    <a href="#recommended_autoconf">
                        Run './configure' through scan-build
                    </a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#iphone">
                Analyzing iPhone Projects
            </a>
        </li>
    </ul>
    <h2 id="scanbuild">
        Getting Started
    </h2>
    <p>
        <tt>
            scan-build
        </tt>
        命令可以用来通过本质上地干预项目的build过程，来分析一个整个的项目。这意味着为了使用
        <tt>
            scan-build
        </tt>
        来执行分析器，你可以使用
        <tt>
            scan-build
        </tt>
        ，来分析在项目build期间由
        <tt>
            gcc
        </tt>
        /
        <tt>
            clang
        </tt>
        编译的源文件。同时这也意味着任何没有被编译的文件也不会被分析。
    </p>
    <h3 id="scanbuild_basicusage">
        Basic Usage
    </h3>
    <p>
        <tt>
            scan-build
        </tt>
        的基本用法是很简单的：只需将"scan-build"放到你build命令的前面：
    </p>
    <pre class="code_example">$ <span class="code_highlight">scan-build</span> make
$ <span class="code_highlight">scan-build</span> xcodebuild
</pre>
    <p>
        第一种情况
        <tt>
            scan-build
        </tt>
        分析了使用
        <tt>
            make
        </tt>
        build的项目的代码，第二种情况
        <tt>
            scan-build
        </tt>
        分析了使用
        <tt>
            xcodebuild
        </tt>
        build的项目
    </p>
    <p>
    </p>
    <p>
        这个是调用
        <tt>
            scan-build
        </tt>
        的一般的格式：
    </p>
    <pre class="code_example">$ <span class="code_highlight">scan-build</span> <i>[scan-build options]</i> <span class="code_highlight">&lt;command&gt;</span> <i>[command options]</i>
</pre>
    <p>
        在操作上，
        <tt>
            scan-build
        </tt>
        用全部随后传给它的选项，照字面地运行了&lt;command&gt;。例如，可以传递
        <tt>
            -j4
        </tt>
        选项到
        <tt>
            make
        </tt>
        来获取4核的并行执行：
    </p>
    <pre class="code_example">$ scan-build make <span class="code_highlight">-j4</span>
</pre>
    <p>
        在大多情况下，
        <tt>
            scan-build
        </tt>
        不需要转换build命令后面的选项；一般来说，
        <tt>
            scan-build
        </tt>
        支持并行地build，
        <b>
            但不支持分布式的build
        </b>
        。
    </p>
    <p>
        使用
        <tt>
            scan-build
        </tt>
        去分析指定的文件也是可以的：
    </p>
    <pre class="code_example"> $ scan-build gcc -c <span class="code_highlight">t1.c t2.c</span>
</pre>
    <p>
        这个例子分析了
        <tt>
            t1.c
        </tt>
        和
        <tt>
            t2.c
        </tt>
        文件。
    </p>
    <h3 id="scanbuild_forwindowsusers">
        For Windows Users
    </h3>
    <p>
        Windows用户必须安装了Perl，才能使用scan-build。
    </p>
    <p>
        <tt>
            scan-build.bat
        </tt>
        脚本，让你可以以与上面基本用法描述一样的方式运行scan-build。为了从任意的位置调用scan-build，添加包含scan-build.bat的目录的路径到你的PATH环境变量中。
    </p>
    <p>
        当使用MinGW/MSYS运行scan-build时，如果你遇到了意外的compilation/make问题，下面的信息或许是有帮助的：
    </p>
    <ul>
        <li>
            当从Windows的cmd中，使用MSYS来build时，如果意外地得到了
            <tt>
                "fatal error: no input files"
            </tt>
            ，尝试以下解决方案中的一种：
        </li>
        <ul>
            <li>
                使用MinGW
                <tt>
                    mingw32-make
                </tt>
                替换MSYS
                <tt>
                    make
                </tt>
                ，并从PATH中排除到MSYS的路径，来避免
                <tt>
                    mingw32-make
                </tt>
                使用MSYS工具。MSYS依赖于MSYS的运行时，它并没有打算被Windows的cmd执行。特别地，当传入使用反引号的makefile命令，会严重地破坏执行。
            </li>
            <li>
                从sh shell运行
                <tt>
                    make
                </tt>
                ：
                <pre class="code_example">$ <span class="code_highlight">scan-build</span> <i>[scan-build options]</i> sh -c "make <i>[make options]</i>"
</pre>
            </li>
        </ul>
        <li>
            当使用GNU Make 3.81时，如果获得了
            <tt>
                "Error : *** target pattern contains no `%'"
            </tt>
            ，尝试使用另一个版本的make。
        </li>
    </ul>
    <h3 id="scanbuild_otheroptions">
        Other Options
    </h3>
    <p>
        正如上面提到的，额外的选项可以传递给
        As mentioned above, extra options can be passed to
        <tt>
            scan-build
        </tt>
        。这些选项给build命令添加了前缀。例如：
    </p>
    <pre class="code_example"> $ scan-build <span class="code_highlight">-k -V</span> make
 $ scan-build <span class="code_highlight">-k -V</span> xcodebuild
</pre>
    <p>
        这里是部分可用的选项：
    </p>
    <table class="options">
        <colgroup>
            <col class="option">
                <col class="description">
        </colgroup>
        <thead>
            <tr>
                <td>
                    选项
                </td>
                <td>
                    描述
                </td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>
                    <b>
                        -o
                    </b>
                </td>
                <td>
                	HTML报告文件的目标目录。当需要表示分析的单独的“执行”时，会创建子目录。如果没有指定这个选项，目录将创建在
                    <tt>
                        /tmp
                    </tt>
                    来保存报告。
                </td>
            </tr>
            <tr>
                <td>
                    <b>
                        -h
                    </b>
                    <br>
                    <i>
                        (或没有参数时)
                    </i>
                </td>
                <td>
                	展示全部的
                    <tt>
                        scan-build
                    </tt>
                    选项。
                </td>
            </tr>
            <tr>
                <td>
                    <b>
                        -k
                    </b>
                    <br>
                    <b>
                        --keep-going
                    </b>
                </td>
                <td>
                	添加一个“保持继续”（keep on going）选项到指定的build目录。
                    <p>
                    	这个选项当前支持
                        <tt>
                            make
                        </tt>
                        和
                        <tt>
                            xcodebuild
                        </tt>
                        。
                    </p>
                    <p>
                    	它是一个便利选项；可以直接使用build选项来指定这个行为。
                    </p>
                </td>
            </tr>
            <tr>
                <td>
                    <b>
                        -v
                    </b>
                </td>
                <td>
                	从scan-build何分析器详细地输出。
                    <b>
                    	第二和第三个“-v”会增加详细程度
                    </b>
                    ，这对于给分析器归档bug报告是非常有用的。
                </td>
            </tr>
            <tr>
                <td>
                    <b>
                        -V
                    </b>
                </td>
                <td>
                	当build命令完成后，在web浏览器中查看分析结果。
                </td>
            </tr>
            <tr>
                <td>
                    <b>
                        --use-analyzer Xcode
                    </b>
                    <br>
                    <i>
                        或
                    </i>
                    <br>
                    <b>
                        --use-analyzer [path to clang]
                    </b>
                </td>
                <td>
                    <tt>
                        scan-build
                    </tt>
                    为静态分析使用相对于它自己可执行的'clang' 。可以通过这个选项来覆盖这个行为，通过使用这个由Xcode打包，或从PATH而来的'clang'。
                    <p>
                    </p>
                </td>
            </tr>
        </tbody>
    </table>
    <p>
        不带任何参数地运行
        <tt>
            scan-build
        </tt>
        可以获得完整的选项列表。
    </p>
    <h3 id="scanbuild_output">
        Output of scan-build
    </h3>
    <p>
    	scan-build的输出是一整套的HTML文件，每个都代表一个单独的bug报告。一个单独的
        <tt>
            index.html
        </tt>
        文件是用来考察全部的bug的。你可以在浏览器中只打开
        <tt>
            index.html
        </tt>
        来查看bug报告。
    </p>
    <p>
    	<tt>
            scan-build
        </tt>
        在哪里生成HTML文件可以由        
        <b>
            -o
        </b>
        选项来确定。如果未指定
        <b>
            -o
        </b>
        选项，则会在
        <tt>
            /tmp
        </tt>
        中创建一个目录来储存文件（
        <tt>
            scan-build
        </tt>
        会打印一条信息来告诉你这个路径）。如果你想在build完成后直接查看报告，传递
        <b>
            -V
        </b>
        选项给
        <tt>
            scan-build
        </tt>
        。
    </p>
    <h2 id="recommendedguidelines">
        Recommended Usage Guidelines
    </h2>
    <p>
        This section describes a few recommendations with running the analyzer.
    </p>
    <h3 id="recommended_debug">
        ALWAYS analyze a project in its "debug" configuration
    </h3>
    <p>
        Most projects can be built in a "debug" mode that enables assertions.
        Assertions are picked up by the static analyzer to prune infeasible paths,
        which in some cases can greatly reduce the number of false positives (bogus
        error reports) emitted by the tool.
    </p>
    <p>
        Another option is to use
        <tt>
            --force-analyze-debug-code
        </tt>
        flag of
        <b>
            scan-build
        </b>
        tool which would enable assertions automatically.
    </p>
    <h3 id="recommend_verbose">
        Use verbose output when debugging scan-build
    </h3>
    <p>
        <tt>
            scan-build
        </tt>
        takes a
        <b>
            -v
        </b>
        option to emit verbose output about what it's doing; two
        <b>
            -v
        </b>
        options emit more information. Redirecting the output of
        <tt>
            scan-build
        </tt>
        to a text file (make sure to redirect standard error) is useful for filing
        bug reports against
        <tt>
            scan-build
        </tt>
        or the analyzer, as we can see the exact options (and files) passed to
        the analyzer. For more comprehensible logs, don't perform a parallel build.
    </p>
    <h3 id="recommended_autoconf">
        Run './configure' through scan-build
    </h3>
    <p>
        If an analyzed project uses an autoconf generated
        <tt>
            configure
        </tt>
        script, you will probably need to run
        <tt>
            configure
        </tt>
        script through
        <tt>
            scan-build
        </tt>
        in order to analyze the project.
    </p>
    <p>
        <b>
            Example
        </b>
    </p>
    <pre class="code_example">
        $ scan-build ./configure $ scan-build make
    </pre>
    <p>
        The reason
        <tt>
            configure
        </tt>
        also needs to be run through
        <tt>
            scan-build
        </tt>
        is because
        <tt>
            scan-build
        </tt>
        scans your source files by
        <i>
            interposing
        </i>
        on the compiler. This interposition is currently done by
        <tt>
            scan-build
        </tt>
        temporarily setting the environment variable
        <tt>
            CC
        </tt>
        to
        <tt>
            ccc-analyzer
        </tt>
        . The program
        <tt>
            ccc-analyzer
        </tt>
        acts like a fake compiler, forwarding its command line arguments over
        to the compiler to perform regular compilation and
        <tt>
            clang
        </tt>
        to perform static analysis.
    </p>
    <p>
        Running
        <tt>
            configure
        </tt>
        typically generates makefiles that have hardwired paths to the compiler,
        and by running
        <tt>
            configure
        </tt>
        through
        <tt>
            scan-build
        </tt>
        that path is set to
        <tt>
            ccc-analyzer
        </tt>
        .
    </p>
    <!-- <h2 id="Debugging">Debugging the Analyzer</h2>
    <p>This section provides information on debugging the analyzer, and troubleshooting
    it when you have problems analyzing a particular project.</p>
    <h3>How it Works</h3>
    <p>To analyze a project, <tt>scan-build</tt> simply sets the environment variable
    <tt>CC</tt> to the full path to <tt>ccc-analyzer</tt>. It also sets a few other
    environment variables to communicate to <tt>ccc-analyzer</tt> where to dump HTML
    report files.</p>
    <p>Some Makefiles (or equivalent project files) hardcode the compiler; for such
    projects simply overriding <tt>CC</tt> won't cause <tt>ccc-analyzer</tt> to be
    called. This will cause the compiled code <b>to not be analyzed.</b></p> If you
    find that your code isn't being analyzed, check to see if <tt>CC</tt> is
    hardcoded. If this is the case, you can hardcode it instead to the <b>full
    path</b> to <tt>ccc-analyzer</tt>.</p>
    <p>When applicable, you can also run <tt>./configure</tt> for a project through
    <tt>scan-build</tt> so that configure sets up the location of <tt>CC</tt> based
    on the environment passed in from <tt>scan-build</tt>:
    <pre>
    $ scan-build <b>./configure</b>
    </pre>
    <p><tt>scan-build</tt> has special knowledge about <tt>configure</tt>, so it in
    most cases will not actually analyze the configure tests run by
    <tt>configure</tt>.</p>
    <p>Under the hood, <tt>ccc-analyzer</tt> directly invokes <tt>gcc</tt> to
    compile the actual code in addition to running the analyzer (which occurs by it
    calling <tt>clang</tt>). <tt>ccc-analyzer</tt> tries to correctly forward all
    the arguments over to <tt>gcc</tt>, but this may not work perfectly (please
    report bugs of this kind).
    -->
    <h2 id="iphone">
        Analyzing iPhone Projects
    </h2>
    <p>
        Conceptually Xcode projects for iPhone applications are nearly the same
        as their cousins for desktop applications.
        <b>
            scan-build
        </b>
        can analyze these projects as well, but users often encounter problems
        with just building their iPhone projects from the command line because
        there are a few extra preparative steps they need to take (e.g., setup
        code signing).
    </p>
    <h3>
        Recommendation: use "Build and Analyze"
    </h3>
    <p>
        The absolute easiest way to analyze iPhone projects is to use the
        <a href="https://developer.apple.com/library/ios/recipes/xcode_help-source_editor/chapters/Analyze.html#//apple_ref/doc/uid/TP40009975-CH4-SW1">
            <i>
                Analyze
            </i>
            feature in Xcode
        </a>
        (which is based on the Clang Static Analyzer). There a user can analyze
        their project right from a menu without most of the setup described later.
    </p>
    <p>
        <a href="http://clang-analyzer.llvm.org/xcode.html">
            Instructions are available
        </a>
        on this website on how to use open source builds of the analyzer as a
        replacement for the one bundled with Xcode.
    </p>
    <h3>
        Using scan-build directly
    </h3>
    <p>
        If you wish to use
        <b>
            scan-build
        </b>
        with your iPhone project, keep the following things in mind:
    </p>
    <ul>
        <li>
            Analyze your project in the
            <tt>
                Debug
            </tt>
            configuration, either by setting this as your configuration with Xcode
            or by passing
            <tt>
                -configuration Debug
            </tt>
            to
            <tt>
                xcodebuild
            </tt>
            .
        </li>
        <li>
            Analyze your project using the
            <tt>
                Simulator
            </tt>
            as your base SDK. It is possible to analyze your code when targeting the
            device, but this is much easier to do when using Xcode's
            <i>
                Build and Analyze
            </i>
            feature.
        </li>
        <li>
            Check that your code signing SDK is set to the simulator SDK as well,
            and make sure this option is set to
            <tt>
                Don't Code Sign
            </tt>
            .
        </li>
    </ul>
    <p>
        Note that you can most of this without actually modifying your project.
        For example, if your application targets iPhoneOS 2.2, you could run
        <b>
            scan-build
        </b>
        in the following manner from the command line:
    </p>
    <pre class="code_example">
        $ scan-build xcodebuild -configuration Debug -sdk iphonesimulator2.2
    </pre>
    Alternatively, if your application targets iPhoneOS 3.0:
    <pre class="code_example">
        $ scan-build xcodebuild -configuration Debug -sdk iphonesimulator3.0
    </pre>
    <h3>
        Gotcha: using the right compiler
    </h3>
    <p>
        Recall that
        <b>
            scan-build
        </b>
        analyzes your project by using a compiler to compile the project and
        <tt>
            clang
        </tt>
        to analyze your project. The script uses simple heuristics to determine
        which compiler should be used (it defaults to
        <tt>
            clang
        </tt>
        on Darwin and
        <tt>
            gcc
        </tt>
        on other platforms). When analyzing iPhone projects,
        <b>
            scan-build
        </b>
        may pick the wrong compiler than the one Xcode would use to build your
        project. For example, this could be because multiple versions of a compiler
        may be installed on your system, especially if you are developing for the
        iPhone.
    </p>
    <p>
        When compiling your application to run on the simulator, it is important
        that
        <b>
            scan-build
        </b>
        finds the correct version of
        <tt>
            gcc/clang
        </tt>
        . Otherwise, you may see strange build errors that only happen when you
        run
        <tt>
            scan-build
        </tt>
        .
    </p>
    <p>
        <b>
            scan-build
        </b>
        provides the
        <tt>
            --use-cc
        </tt>
        and
        <tt>
            --use-c++
        </tt>
        options to hardwire which compiler scan-build should use for building
        your code. Note that although you are chiefly interested in analyzing your
        project, keep in mind that running the analyzer is intimately tied to the
        build, and not being able to compile your code means it won't get fully
        analyzed (if at all).
    </p>
    <p>
        If you aren't certain which compiler Xcode uses to build your project,
        try just running
        <tt>
            xcodebuild
        </tt>
        (without
        <b>
            scan-build
        </b>
        ). You should see the full path to the compiler that Xcode is using, and
        use that as an argument to
        <tt>
            --use-cc
        </tt>
        .
    </p>
</div>
