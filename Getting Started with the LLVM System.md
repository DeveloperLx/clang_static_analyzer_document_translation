#### [原文地址](http://llvm.org/docs/GettingStarted.html) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<h1>
    从LLVM系统开始吧！
    <a class="headerlink" href="#getting-started-with-the-llvm-system" title="Permalink to this headline">
        ¶
    </a>
</h1>
<div class="contents local topic" id="contents">
    <ul class="simple">
        <li>
            <a class="reference internal" href="#overview" id="id4">
                概述
            </a>
        </li>
        <li>
            <a class="reference internal" href="#getting-started-quickly-a-summary"
            id="id5">
                快速入门（摘要）
            </a>
        </li>
        <li>
            <a class="reference internal" href="#requirements" id="id6">
                需求条件
            </a>
            <ul>
                <li>
                    <a class="reference internal" href="#hardware" id="id7">
                        硬件
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#software" id="id8">
                        软件
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#host-c-toolchain-both-compiler-and-standard-library"
                    id="id9">
                        Host C++工具链，编译器和标准库
                    </a>
                    <ul>
                        <li>
                            <a class="reference internal" href="#getting-a-modern-host-c-toolchain"
                            id="id10">
                                获取现代的Host C++ Toolchain
                            </a>
                        </li>
                    </ul>
                </li>
            </ul>
        </li>
        <li>
            <a class="reference internal" href="#getting-started-with-llvm" id="id11">
                从LLVM开始
            </a>
            <ul>
                <li>
                    <a class="reference internal" href="#terminology-and-notation" id="id12">
                        术语和记号
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#unpacking-the-llvm-archives" id="id13">
                        打开LLVM的归档
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#checkout-llvm-from-subversion" id="id14">
                        从Subversion获取LLVM
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#git-mirror" id="id15">
                        Git镜像
                    </a>
                    <ul>
                        <li>
                            <a class="reference internal" href="#sending-patches-with-git" id="id16">
                                使用Git发送patch
                            </a>
                        </li>
                        <li>
                            <a class="reference internal" href="#for-developers-to-work-with-git-svn"
                            id="id17">
                                开发者使用git-svn
                            </a>
                        </li>
                        <li>
                            <a class="reference internal" href="#for-developers-to-work-with-a-git-monorepo"
                            id="id18">
                                开发者使用git monorepo
                            </a>
                        </li>
                    </ul>
                </li>
                <li>
                    <a class="reference internal" href="#local-llvm-configuration" id="id19">
                        本地的LLVM配置
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#compiling-the-llvm-suite-source-code"
                    id="id20">
                        编译LLVM套件的源码
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#cross-compiling-llvm" id="id21">
                        交叉编译LLVM
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#the-location-of-llvm-object-files"
                    id="id22">
                        LLVM对象文件的位置
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#optional-configuration-items" id="id23">
                        可选的配置项目
                    </a>
                </li>
            </ul>
        </li>
        <li>
            <a class="reference internal" href="#directory-layout" id="id24">
                目录布局
            </a>
            <ul>
                <li>
                    <a class="reference internal" href="#llvm-examples" id="id25">
                        <code class="docutils literal">
                            <span class="pre">
                                llvm/examples
                            </span>
                        </code>
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#llvm-include" id="id26">
                        <code class="docutils literal">
                            <span class="pre">
                                llvm/include
                            </span>
                        </code>
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#llvm-lib" id="id27">
                        <code class="docutils literal">
                            <span class="pre">
                                llvm/lib
                            </span>
                        </code>
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#llvm-projects" id="id28">
                        <code class="docutils literal">
                            <span class="pre">
                                llvm/projects
                            </span>
                        </code>
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#llvm-test" id="id29">
                        <code class="docutils literal">
                            <span class="pre">
                                llvm/test
                            </span>
                        </code>
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#test-suite" id="id30">
                        <code class="docutils literal">
                            <span class="pre">
                                test-suite
                            </span>
                        </code>
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#llvm-tools" id="id31">
                        <code class="docutils literal">
                            <span class="pre">
                                llvm/tools
                            </span>
                        </code>
                    </a>
                </li>
                <li>
                    <a class="reference internal" href="#llvm-utils" id="id32">
                        <code class="docutils literal">
                            <span class="pre">
                                llvm/utils
                            </span>
                        </code>
                    </a>
                </li>
            </ul>
        </li>
        <li>
            <a class="reference internal" href="#an-example-using-the-llvm-tool-chain"
            id="id33">
                一个使用LLVM工具链的例子
            </a>
            <ul>
                <li>
                    <a class="reference internal" href="#example-with-clang" id="id34">
                        clang的例子
                    </a>
                </li>
            </ul>
        </li>
        <li>
            <a class="reference internal" href="#common-problems" id="id35">
                常见问题
            </a>
        </li>
        <li>
            <a class="reference internal" href="#links" id="id36">
                链接
            </a>
        </li>
    </ul>
</div>
<div class="section" id="overview">
    <h2>
        <a class="toc-backref" href="#id4">
            概述
        </a>
        <a class="headerlink" href="#overview" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        欢迎来到LLVM！为了入门，你首先需要了解一些基本的信息。
    </p>
    <p>
        首先，LLVM有三个部分。第一个部分是LLVM套件。它包含使用LLVM所需的全部的工具，库，以及头文件。它包含一个汇编程序，反汇编程序，字节码分析器和字节码优化器。它还包含基本的回归测试，可以用来测试LLVM工具和Clang前端。
    </p>
    <p>
        第二个部分则是
        <a class="reference external" href="http://clang.llvm.org/">
            Clang
        </a>
        前端。这个组件编译C，C++，Objective C，和Objective C++代码为LLVM的字节码，它是一个可以被来自LLVM套件的LLVM工具操作的程序。
    </p>
    <p>
        第三部分，是一个叫做测试套件的可选的块。它是一个程序的套件，带有一个可以用来进一步测试LLVM的功能和性能的测试工具。
    </p>
</div>
<div class="section" id="getting-started-quickly-a-summary">
    <h2>
        <a class="toc-backref" href="#id5">
            快速入门（摘要）
        </a>
        <a class="headerlink" href="#getting-started-quickly-a-summary" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        LLVM的入门文档可能已过期。因此
        <a class="reference external" href="http://clang.llvm.org/get_started.html">
            Clang入门
        </a>
        也是一个不错的入门的地方。
    </p>
    <p>
        这里是使用LLVM快速启动和运行的简短历程：
    </p>
    <ol class="arabic">
        <li>
            <p class="first">
                阅读文档。
            </p>
        </li>
        <li>
            <p class="first">
                阅读文档。
            </p>
        </li>
        <li>
            <p class="first">
                记住，你被提醒了两次要阅读文档。
            </p>
            <ul class="simple">
                <li>
                    特别地，
                    <em>
                        指定相对路径是非常重要的
                    </em>
                    。
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取LLVM：
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/llvm/trunk
                        </span>
                        <span class="pre">
                            llvm
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取Clang：
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            llvm/tools
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/cfe/trunk
                        </span>
                        <span class="pre">
                            clang
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取LLD linker
                <strong>
                    [可选]
                </strong>
                ：
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            llvm/tools
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/lld/trunk
                        </span>
                        <span class="pre">
                            lld
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取Polly Loop优化器
                <strong>
                    [可选]
                </strong>
                ：
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            llvm/tools
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/polly/trunk
                        </span>
                        <span class="pre">
                            polly
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取Compiler-RT（build“粉碎机”（sanitizers）所必须的）
                <strong>
                    [可选]
                </strong>
                :
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            llvm/projects
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/compiler-rt/trunk
                        </span>
                        <span class="pre">
                            compiler-rt
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取Libomp（OpenMP支持所必须的）
                <strong>
                    [可选]
                </strong>
                ：
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            llvm/projects
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/openmp/trunk
                        </span>
                        <span class="pre">
                            openmp
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取libcxx和libcxxabi
                <strong>
                    [可选]
                </strong>
                ：
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            llvm/projects
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/libcxx/trunk
                        </span>
                        <span class="pre">
                            libcxx
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/libcxxabi/trunk
                        </span>
                        <span class="pre">
                            libcxxabi
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                获取测试套件的源码
                <strong>
                    [可选]
                </strong>
            </p>
            <ul class="simple">
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            你要将llvm保存到的地方
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            cd
                        </span>
                        <span class="pre">
                            llvm/projects
                        </span>
                    </code>
                </li>
                <li>
                    <code class="docutils literal">
                        <span class="pre">
                            svn
                        </span>
                        <span class="pre">
                            co
                        </span>
                        <span class="pre">
                            http://llvm.org/svn/llvm-project/test-suite/trunk
                        </span>
                        <span class="pre">
                            test-suite
                        </span>
                    </code>
                </li>
            </ul>
        </li>
        <li>
            <p class="first">
                配置并build LLVM和Clang：
            </p>
            <p>
                <em>
                    警告：
                </em>
                确保你已在尝试配置cmake前，获取了
                <em>
                    全部的
                </em>
                源码。cmake不能在增量编译中，获取新添加的源码的目录。
            </p>
            <p>
                build使用
                <a class="reference external" href="CMake.html">
                    CMake
                </a>
                。LLVM要求CMake 3.4.3来build。通常建议最新的CMake，尤其在你生成Ninja build文件的时候。这是因为CMake项目一直在持续地提高生成器的质量，Ninja生成器受到了较多的关注。
            </p>
            <ul>
                <li>
                    <p class="first">
                        <code class="docutils literal">
                            <span class="pre">
                                cd
                            </span>
                            <span class="pre">
                                where
                            </span>
                            <span class="pre">
                                you
                            </span>
                            <span class="pre">
                                want
                            </span>
                            <span class="pre">
                                to
                            </span>
                            <span class="pre">
                                build
                            </span>
                            <span class="pre">
                                llvm
                            </span>
                        </code>
                    </p>
                </li>
                <li>
                    <p class="first">
                        <code class="docutils literal">
                            <span class="pre">
                                mkdir
                            </span>
                            <span class="pre">
                                build
                            </span>
                        </code>
                    </p>
                </li>
                <li>
                    <p class="first">
                        <code class="docutils literal">
                            <span class="pre">
                                cd
                            </span>
                            <span class="pre">
                                build
                            </span>
                        </code>
                    </p>
                </li>
                <li>
                    <p class="first">
                        <code class="docutils literal">
                            <span class="pre">
                                cmake
                            </span>
                            <span class="pre">
                                -G
                            </span>
                            <span class="pre">
                                &lt;generator&gt;
                            </span>
                            <span class="pre">
                                [options]
                            </span>
                            <span class="pre">
                                &lt;path
                            </span>
                            <span class="pre">
                                to
                            </span>
                            <span class="pre">
                                llvm
                            </span>
                            <span class="pre">
                                sources&gt;
                            </span>
                        </code>
                    </p>
                    <p>
                        一些常见的生成器有：
                    </p>
                    <ul class="simple">
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    Unix
                                </span>
                                <span class="pre">
                                    Makefiles
                                </span>
                            </code>
                            - 用来生成兼容的并行makefile。
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    Ninja
                                </span>
                            </code>
                            - 用来生成
                            <a class="reference external" href="https://ninja-build.org">
                                Ninja
                            </a>
                            build文件。大多数的llvm的开发者都使用Ninja。
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    Visual
                                </span>
                                <span class="pre">
                                    Studio
                                </span>
                            </code>
                            - 用来生成Visual Studio项目和解决方案。
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    Xcode
                                </span>
                            </code>
                            - 用来生成Xcode项目。
                        </li>
                    </ul>
                    <p>
                        一些常用的选项：
                    </p>
                    <ul class="simple">
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    -DCMAKE_INSTALL_PREFIX=directory
                                </span>
                            </code>
                            - 指定你想要将LLVM工具和库安装到的
                            <em>
                                目录
                            </em>
                            的全路径（默认值为
                            <code class="docutils literal">
                                <span class="pre">
                                    /usr/local
                                </span>
                            </code>
                            ）。
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    -DCMAKE_BUILD_TYPE=type
                                </span>
                            </code>
                            - 
                            <em>
                                type
                            </em>
                            的有效选项有Debug，Release，RelWithDebInfo，和MinSizeRel。默认为Default。
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    -DLLVM_ENABLE_ASSERTIONS=On
                                </span>
                            </code>Yes
                            - 编译时打开断言（Debug build时默认为Yes，但并非对全部的build类似都是这样）。
                        </li>
                    </ul>
                </li>
                <li>
                    <p class="first">
                        运行你的build工具的选择！
                    </p>
                    <ul class="simple">
                        <li>
                            默认的target（也就是说
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                            </code>
                            ）将会build全部的LLVM
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    check-all
                                </span>
                            </code>
                            target（也就是说
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                                <span class="pre">
                                    check-all
                                </span>
                            </code>
                            ）将运行回归测试来确保每一件事有序地工作。
                        </li>
                        <li>
                            CMake将为每个工具和库生成build target，大多数LLVM的子项目会生成它们自己的
                            <code class="docutils literal">
                                <span class="pre">
                                    check-&lt;project&gt;
                                </span>
                            </code>
                            target。
                        </li>
                        <li>
                            运行串行的build将会
                            <em>
                                较慢
                            </em>
                            。确保你运行平行的build；对于
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                            </code>
                            ，使用
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                                <span class="pre">
                                    -j
                                </span>
                            </code>
                            。
                        </li>
                    </ul>
                </li>
                <li>
                    <p class="first">
                        有关更多的信息，请参考
                        <a class="reference external" href="CMake.html">
                            CMake
                        </a>
                    </p>
                </li>
                <li>
                    <p class="first">
                        如果你遇到了“内部编译错误（ICE）”或测试失败，参考
                        <a class="reference internal" href="#below">
                            下文
                        </a>
                        。
                    </p>
                </li>
            </ul>
        </li>
    </ol>
    <p>
        关于配置和编译LLVM的详细信息，请查阅
        <a class="reference internal" href="#getting-started-with-llvm">
            LLVM入门
        </a>
        这部分。前往
        <a class="reference internal" href="#directory-layout">
            Directory Layout
        </a>
        来了解源码树的布局。
    </p>
</div>
<div class="section" id="requirements">
    <h2>
        <a class="toc-backref" href="#id6">
            要求
        </a>
        <a class="headerlink" href="#requirements" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        在你开始使用LLVM系统之前，回顾下面列出的要求。这可以通过提前了解你需要什么硬件和软件，来把你从一些麻烦中解救出来。
    </p>
    <div class="section" id="hardware">
        <h3>
            <a class="toc-backref" href="#id7">
                硬件
            </a>
            <a class="headerlink" href="#hardware" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            已知LLVM可以在以下的主机平台运行：
        </p>
        <table class="docutils">
            <colgroup>
                <col width="35%">
                    <col width="40%">
                        <col width="25%">
            </colgroup>
            <thead valign="bottom">
                <tr class="row-odd">
                    <th class="head">
                        操作系统
                    </th>
                    <th class="head">
                        架构
                    </th>
                    <th class="head">
                        编译器
                    </th>
                </tr>
            </thead>
            <tbody valign="top">
                <tr class="row-even">
                    <td>
                        Linux
                    </td>
                    <td>
                        x86
                        <sup>
                            1
                        </sup>
                    </td>
                    <td>
                        GCC, Clang
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        Linux
                    </td>
                    <td>
                        amd64
                    </td>
                    <td>
                        GCC, Clang
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        Linux
                    </td>
                    <td>
                        ARM
                        <sup>
                            4
                        </sup>
                    </td>
                    <td>
                        GCC, Clang
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        Linux
                    </td>
                    <td>
                        PowerPC
                    </td>
                    <td>
                        GCC, Clang
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        Solaris
                    </td>
                    <td>
                        V9 (Ultrasparc)
                    </td>
                    <td>
                        GCC
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        FreeBSD
                    </td>
                    <td>
                        x86
                        <sup>
                            1
                        </sup>
                    </td>
                    <td>
                        GCC, Clang
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        FreeBSD
                    </td>
                    <td>
                        amd64
                    </td>
                    <td>
                        GCC, Clang
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        MacOS X
                        <sup>
                            2
                        </sup>
                    </td>
                    <td>
                        PowerPC
                    </td>
                    <td>
                        GCC
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        MacOS X
                    </td>
                    <td>
                        x86
                    </td>
                    <td>
                        GCC, Clang
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        Cygwin/Win32
                    </td>
                    <td>
                        x86
                        <sup>
                            1, 3
                        </sup>
                    </td>
                    <td>
                        GCC
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        Windows
                    </td>
                    <td>
                        x86
                        <sup>
                            1
                        </sup>
                    </td>
                    <td>
                        Visual Studio
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        Windows x64
                    </td>
                    <td>
                        x86-64
                    </td>
                    <td>
                        Visual Studio
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="admonition note">
            <p class="first admonition-title">
                注意
            </p>
            <ol class="last arabic simple">
                <li>
                    支持奔腾处理器及以上的代码生成器
                </li>
                <li>
                    仅支持32位的ABI（应用系统二进制接口）的代码生成器
                </li>
                <li>
                    为了在基于Win32的系统上使用LLVM模块，你可以用
                    <code class="docutils literal">
                        <span class="pre">
                            -DBUILD_SHARED_LIBS=On
                        </span>
                    </code>
                    来配置LLVM。
                </li>
                <li>
                    MCJIT在v7版本之前工作不正常，因为旧的JIT引擎不再支持。
                    MCJIT not working well pre-v7, old JIT engine not supported any more.
                </li>
            </ol>
        </div>
        <p>
            注意，Debug的build需要大量的时间和磁盘空间。仅build LLVM的情况就需要大概1-3 GB的空间。而完整的LLVM和Clang的build则需要15-20 GB的磁盘空间。准确的空间需求则会随着系统的变化而变化。（之所以需求如此之大，是由于全部的debug信息，以及大量的库都是被静态连接到多个工具中的事实）。
        </p>
        <p>
            如果您的空间有限，你可以只build选择的工具或选择的target。Release的build只需要相当少的空间。
        </p>
        <p>
            LLVM套件
            <em>
                may
            </em>
            可能在其它平台上编译，但不能确保这么做。如果编译成功，LLVM工具就应当可以完成汇编、反汇编、分析和优化LLVM字节码。代码生成器也应该可以工作，尽管生成的本地代码可能无法在你的平台上运行。
        </p>
    </div>
    <div class="section" id="software">
        <h3>
            <a class="toc-backref" href="#id8">
                软件
            </a>
            <a class="headerlink" href="#software" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            编译LLVM需要你安装几个软件包。下表列出了这些需求的包。Package列是LLVM以来的软件包的常用名。Version列提供了包的“已知的工作”的版本。Notes列描述了LLVM怎么使用包和提供其它信息。
        </p>
        <table class="docutils">
            <colgroup>
                <col width="52%">
                    <col width="11%">
                        <col width="37%">
            </colgroup>
            <thead valign="bottom">
                <tr class="row-odd">
                    <th class="head">
                        Package
                    </th>
                    <th class="head">
                        Version
                    </th>
                    <th class="head">
                        Notes
                    </th>
                </tr>
            </thead>
            <tbody valign="top">
                <tr class="row-even">
                    <td>
                        <a class="reference external" href="http://savannah.gnu.org/projects/make">
                            GNU Make
                        </a>
                    </td>
                    <td>
                        3.79, 3.79.1
                    </td>
                    <td>
                        Makefile/build processor
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        <a class="reference external" href="http://gcc.gnu.org/">
                            GCC
                        </a>
                    </td>
                    <td>
                        &gt;=4.8.0
                    </td>
                    <td>
                        C/C++ compiler
                        <sup>
                            1
                        </sup>
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        <a class="reference external" href="http://www.python.org/">
                            python
                        </a>
                    </td>
                    <td>
                        &gt;=2.7
                    </td>
                    <td>
                        Automated test suite
                        <sup>
                            2
                        </sup>
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        <a class="reference external" href="http://zlib.net">
                            zlib
                        </a>
                    </td>
                    <td>
                        &gt;=1.2.3.4
                    </td>
                    <td>
                        Compression library
                        <sup>
                            3
                        </sup>
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="admonition note">
            <p class="first admonition-title">
                注意
            </p>
            <ol class="last arabic simple">
                <li>
                    只需要C和C++语言，因此无需为LLVM构建其它的语言。查看
                    <cite>
                        下面
                    </cite>
                    特定版本的信息。
                </li>
                <li>
                    仅在你想要在
                    <code class="docutils literal">
                        <span class="pre">
                            llvm/test
                        </span>
                    </code>
                    目录下运行自动测试套件时才需要。
                </li>
                <li>
                    添加压缩/解压的能力到LLVM工具中是可选的。
                </li>
            </ol>
        </div>
        <p>
            另外，希望你的编译主机含有下列的Unix工具。尤其是：
        </p>
        <ul class="simple">
            <li>
                <strong>
                    ar
                </strong>
                - 归档库构建器
            </li>
            <li>
                <strong>
                    bzip2
                </strong>
                - bzip2命令用于发布版本
            </li>
            <li>
                <strong>
                    bunzip2
                </strong>
                - bunzip2命令用于发布校验
            </li>
            <li>
                <strong>
                    chmod
                </strong>
                - 改变一个文件的权限
            </li>
            <li>
                <strong>
                    cat
                </strong>
                - 输出的连结工具
            </li>
            <li>
                <strong>
                    cp
                </strong>
                - 拷贝文件
            </li>
            <li>
                <strong>
                    date
                </strong>
                - 打印当前的日期/时间
            </li>
            <li>
                <strong>
                    echo
                </strong>
                - 打印到标注输出
            </li>
            <li>
                <strong>
                    egrep
                </strong>
                - 扩展的正则表达式搜索工具
            </li>
            <li>
                <strong>
                    find
                </strong>
                - 在文件系统中查找文件/目录
            </li>
            <li>
                <strong>
                    grep
                </strong>
                - 正则表达式搜索工具
            </li>
            <li>
                <strong>
                    gzip
                </strong>
                - gzip命令用来发布版本
            </li>
            <li>
                <strong>
                    gunzip
                </strong>
                - gunzip命令用来发布校验
            </li>
            <li>
                <strong>
                    install
                </strong>
                - 安装目录/文件
            </li>
            <li>
                <strong>
                    mkdir
                </strong>
                - 创建一个目录
            </li>
            <li>
                <strong>
                    mv
                </strong>
                - 移动（重命名）文件
            </li>
            <li>
                <strong>
                    ranlib
                </strong>
                - 归档库的符号表生成器
            </li>
            <li>
                <strong>
                    rm
                </strong>
                - 删除文件和目录
            </li>
            <li>
                <strong>
                    sed
                </strong>
                - 用于转换输出的流编辑器
            </li>
            <li>
                <strong>
                    sh
                </strong>
                - 用来build脚本的Bourne shell
            </li>
            <li>
                <strong>
                    tar
                </strong>
                - 用于发布版本的tape归档
            </li>
            <li>
                <strong>
                    test
                </strong>
                - 在文件系统中进行测试
            </li>
            <li>
                <strong>
                    unzip
                </strong>
                - unzip命令用于发布校验
            </li>
            <li>
                <strong>
                    zip
                </strong>
                - zip命令用于发布版本
            </li>
        </ul>
    </div>
    <div class="section" id="host-c-toolchain-both-compiler-and-standard-library">
        <span id="check-here">
        </span>
        <span id="below">
        </span>
        <h3>
            <a class="toc-backref" href="#id9">
                主C++工具链，包含编译器和标注库
            </a>
            <a class="headerlink" href="#host-c-toolchain-both-compiler-and-standard-library"
            title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            主机的C++编译器对LLVM的要求非常高，因此往往编译器会出现错误。我们也在计划在C++语言，及合理关联的库中进一步地发展完善。因此，为了build LLVM，我们要求一个现代的主C++工具链，包含编译器和标注库。
        </p>
        <p>
            关于最流行的主工具链，我们在构建系统确定的最低版本：
        </p>
        <ul class="simple">
            <li>
                Clang 3.1
            </li>
            <li>
                GCC 4.8
            </li>
            <li>
                Visual Studio 2015 (Update 3)
            </li>
        </ul>
        <p>
            比这些工具链更老的
            <em>
                也可以
            </em>
            工作，但会要求构建系统带有一个特定的选项，并不是实际地支持的主平台。同时，注意这些较老版本的编译器经常会崩溃，或错误地编译LLVM。
        </p>
        <p>
            对于并不广泛使用的主工具链，例如ICC或xlC，注意可能需要一个最新版本，来支持用于LLVM的全部的C++特性。
        </p>
        <p>
            我们会追踪
            <em>
                已知的
            </em>
            当被作为工具链的一部分使用时，会失败的某一版本的软件。这些有时甚至会包含连接器。
        </p>
        <p>
            <strong>
                GNU ld 2.16.X
            </strong>
            。一些某一版本的软件版本的ld连接器，会产生非常长的警告信息，抱怨一些
            <code class="docutils literal">
                <span class="pre">
                    .gnu.linkonce.t.*
                </span>
            </code>
            ”符号被定义到了一个已废弃的部分。你可以安全地忽略掉这些信息，因为它们是错误的，连接是正确的。这些信息在ld 2.17版本时已消失。
        </p>
        <p>
            <strong>
                GNU binutils 2.17
            </strong>
            ：Binutils 2.17包含
            <a class="reference external" href="http://sourceware.org/bugzilla/show_bug.cgi?id=3111">
                一个bug
            </a>
            ，它在构建LLVM造成了大量的连接时间（分钟级的）。我们建议将其升级到一个更新的版本（2.17.50.0.4或更高）。
        </p>
        <p>
            <strong>
                GNU Binutils 2.19.1 Gold
            </strong>
            ：这个Gold版本包含
            <a class="reference external" href="http://sourceware.org/bugzilla/show_bug.cgi?id=9836">
                一个bug
            </a>
            ，当构建和位置无关的LLVM时，它造成了一个偶现的失败。这个现象是一个有关循环依赖的错误。我们建议更新到一个新的Gold版本。
        </p>
        <div class="section" id="getting-a-modern-host-c-toolchain">
            <h4>
                <a class="toc-backref" href="#id10">
                    获得一个现代的主C++工具链
                </a>
                <a class="headerlink" href="#getting-a-modern-host-c-toolchain" title="Permalink to this headline">
                    ¶
                </a>
            </h4>
            <p>
                这个部分主要应用于Linux和更老版本的BSD。在Mac OS X中，你应当有一个足够现代的Xcode，否则你将需要升级，直到可以为止。Windows中并没有“系统编译器”，因此你必须安装Visual Studio 2015或最新版本的mingw64。FreeBSD 10.0或更新的版本含有现代的Clang可作为系统编译器。
            </p>
            <p>
                然后，一些Linux的发布版，及一些其它的或更老的BSD有时会有极老版本的GCC。下面这些步骤会尝试在这样的一个系统上帮助你更新你的编译器。然而，如果可能的话，我们鼓励你使用能够满足要求的，带有现代系统编译器的最新版本。注意，它会尝试安装先前版本的Clang和libc++到主编译器上，然而，在相对最新的版本之前，libc++尚未被很好地测试，或准备好构建到Linux上。因此，这个指导将使用libstdc++和现代的GCC，作为在bootstrap中的初始主机，然后再使用Clang（和潜在的libc++）。
            </p>
            <p>
                第一步是安装一个最新版本的工具链。用户在版本需求方面，最常用的版本是Ubuntu Precise，12.04 LTS。对于这个版本，一个很容易的选择，是安装
                <a class="reference external" href="https://launchpad.net/~ubuntu-toolchain-r/+archive/test">
                    工具链测试PPA（Personal Package Archives个人软件包档案）
                </a>
                ，并使用它来安装一个现代的GCC。关于这个，这里有一个很好的探讨：
                <a class="reference external" href="http://askubuntu.com/questions/271388/how-to-install-gcc-4-8-in-ubuntu-12-04-from-the-terminal">
                    请问ubuntu的栈交换
                </a>
                。然而，并非所有的用户都可以使用PPA，这里有很多其它的讨论，因此有必要（或只是有用处，如果你在做编译器的开发的话）从其它的源构建和安装GCC。在这些天做到也是很容易的。
            </p>
            <p>
                安装GCC 4.8.2的简要步骤：
            </p>
            <pre><span></span><span class="gp">%</span> wget https://ftp.gnu.org/gnu/gcc/gcc-4.8.2/gcc-4.8.2.tar.bz2
<span class="gp">%</span> wget https://ftp.gnu.org/gnu/gcc/gcc-4.8.2/gcc-4.8.2.tar.bz2.sig
<span class="gp">%</span> wget https://ftp.gnu.org/gnu/gnu-keyring.gpg
<span class="gp">%</span> <span class="nv">signature_invalid</span><span class="o">=</span><span class="sb">`</span>gpg --verify --no-default-keyring --keyring ./gnu-keyring.gpg gcc-4.8.2.tar.bz2.sig<span class="sb">`</span>
<span class="gp">%</span> <span class="k">if</span> <span class="o">[</span> <span class="nv">$signature_invalid</span> <span class="o">]</span><span class="p">;</span> <span class="k">then</span> <span class="nb">echo</span> <span class="s2">"Invalid signature"</span> <span class="p">;</span> <span class="nb">exit</span> <span class="m">1</span> <span class="p">;</span> <span class="k">fi</span>
<span class="gp">%</span> tar -xvjf gcc-4.8.2.tar.bz2
<span class="gp">%</span> <span class="nb">cd</span> gcc-4.8.2
<span class="gp">%</span> ./contrib/download_prerequisites
<span class="gp">%</span> <span class="nb">cd</span> ..
<span class="gp">%</span> mkdir gcc-4.8.2-build
<span class="gp">%</span> <span class="nb">cd</span> gcc-4.8.2-build
<span class="gp">%</span> <span class="nv">$PWD</span>/../gcc-4.8.2/configure --prefix<span class="o">=</span><span class="nv">$HOME</span>/toolchains --enable-languages<span class="o">=</span>c,c++
<span class="gp">%</span> make -j<span class="k">$(</span>nproc<span class="k">)</span>
<span class="gp">%</span> make install
</pre>
            <p>
                关于更多细节，参考
                <a class="reference external" href="http://gcc.gnu.org/wiki/InstallingGCC">
                    GCC wiki
                </a>
                ，在这里你可以得到大部分的信息。
            </p>
            <p>
                当你有了GCC工具链之后，配置你的LLVM的build来为你的主编译器和C++标准库使用新的工具链。因为libstdc++的新版本并不在系统库的搜索路径中，你需要传递额外的连接标记，让它可以在连接时(<span class="pre">-L</span>)和编译时（
                <code class="docutils literal">
                    <span class="pre">
                        -rpath
                    </span>
                </code>
                ）被找到。如果你正在使用CMake，这个调用应当会产生可行的二进制文件：
            </p>
            <pre><span></span><span class="gp">%</span> mkdir build
<span class="gp">%</span> <span class="nb">cd</span> build
<span class="gp">%</span> <span class="nv">CC</span><span class="o">=</span><span class="nv">$HOME</span>/toolchains/bin/gcc <span class="nv">CXX</span><span class="o">=</span><span class="nv">$HOME</span>/toolchains/bin/g++ <span class="se">\</span>
<span class="go">  cmake .. -DCMAKE_CXX_LINK_FLAGS="-Wl,-rpath,$HOME/toolchains/lib64 -L$HOME/toolchains/lib64"</span>
</pre>
            <p>
                如果你无法设置rpath，大多数的LLVM二进制文件将在启动时失败，并在loader上显示一条类似于
                <code class="docutils literal">
                    <span class="pre">
                        libstdc++.so.6:
                    </span>
                    <span class="pre">
                        version
                    </span>
                    <span class="pre">
                        `GLIBCXX_3.4.20'
                    </span>
                    <span class="pre">
                        not
                    </span>
                    <span class="pre">
                        found
                    </span>
                </code>
                的信息。这意味着你需要调整（tweak）-rpath连接器标志。
            </p>
            <p>
                当构建Clang的时候，为了将它作为你bootstrap中一部分的新主机，你需要给
                <em>
                    它
                </em>
                访问现代的C++11标准库的权限。有两种简便的方式来做到这点，一种是构建（并安装）libc++和clang，然后用
                <code class="docutils literal">
                    <span class="pre">
                        -stdlib=libc++
                    </span>
                </code>
                编译和连接标志来使用它；另一种是安装Clang到和GCC相同的前缀的（
                <code class="docutils literal">
                    <span class="pre">
                        $HOME/toolchains
                    </span>
                </code>
                上面）中。Clang如果可以找到的话，就会在自己的前缀中查找libstdc++并使用它。你也可以为Clang添加一个明确的前缀，来查找带有
                <code class="docutils literal">
                    <span class="pre">
                        --gcc-toolchain=/opt/my/gcc/prefix
                    </span>
                </code>
                标记的GCC工具链，就可以在使用你刚构建的Clang进行bootstrap时，传递它到编译和连接命令中。
            </p>
        </div>
    </div>
</div>
<div class="section" id="getting-started-with-llvm">
    <span id="id2">
    </span>
    <h2>
        <a class="toc-backref" href="#id11">
            LLVM入门
        </a>
        <a class="headerlink" href="#getting-started-with-llvm" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        这篇向导的剩余部分，让你可以运行LLVM，并给出你一些关于LLVM环境的基本信息。
    </p>
    <p>
        这篇向导后面的部分描述了LLVM源码树的
        <a class="reference internal" href="#general-layout">
            一般布局
        </a>
        ，以及一个使用LLVM工具链的
        <a class="reference internal" href="#simple-example">
            简单例子
        </a>
        ，并
        <a class="reference internal" href="#links">
            连接
        </a>
        到查找更多关于LLVM的信息，或通过电子邮件获取帮助。
    </p>
    <div class="section" id="terminology-and-notation">
        <h3>
            <a class="toc-backref" href="#id12">
                术语和符号
            </a>
            <a class="headerlink" href="#terminology-and-notation" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            在这个手册中，下列名称用来表示指向本地系统和工作环境的路径。
            <em>
                这些并不是你需要设置的环境变量，而是在这篇文档下面的部分用到的字符串
            </em>
            。在下面的例子中，会在你本地的系统上，将这些名称中的每一个，简单替换为相应的路径名称：
        </p>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    SRC_ROOT
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                LLVM源码树的根目录。
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    OBJ_ROOT
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                LLVM对象树的根目录（也就是说，对象文件和被编译的程序的书将被放置的地方。它可以和SRC_ROOT相同）。
            </div>
        </blockquote>
    </div>
    <div class="section" id="unpacking-the-llvm-archives">
        <h3>
            <a class="toc-backref" href="#id13">
                打开LLVM的归档
            </a>
            <a class="headerlink" href="#unpacking-the-llvm-archives" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            If you have the LLVM distribution, 
            you will need to unpack it before you can begin to compile it. 
            LLVM is distributed as a set of two files: 
            the LLVM suite and the LLVM GCC front end compiled for your platform. 
            There is an additional test suite that is optional. 
            Each file is a TAR archive that is compressed with the gzip program.
        </p>
        <p>
            The files are as follows, with
            <em>
                x.y
            </em>
            marking the version number:
        </p>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm-x.y.tar.gz
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Source release for the LLVM libraries and tools.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm-test-x.y.tar.gz
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Source release for the LLVM test-suite.
            </div>
        </blockquote>
    </div>
    <div class="section" id="checkout-llvm-from-subversion">
        <span id="checkout">
        </span>
        <h3>
            <a class="toc-backref" href="#id14">
                Checkout LLVM from Subversion
            </a>
            <a class="headerlink" href="#checkout-llvm-from-subversion" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            If you have access to our Subversion repository, 
            you can get a fresh copy of the entire source code. 
            All you need to do is check it out from Subversion as follows:
        </p>
        <ul class="simple">
            <li>
                <code class="docutils literal">
                    <span class="pre">
                        cd
                    </span>
                    <span class="pre">
                        where-you-want-llvm-to-live
                    </span>
                </code>
            </li>
            <li>
                Read-Only:
                <code class="docutils literal">
                    <span class="pre">
                        svn
                    </span>
                    <span class="pre">
                        co
                    </span>
                    <span class="pre">
                        http://llvm.org/svn/llvm-project/llvm/trunk
                    </span>
                    <span class="pre">
                        llvm
                    </span>
                </code>
            </li>
            <li>
                Read-Write:
                <code class="docutils literal">
                    <span class="pre">
                        svn
                    </span>
                    <span class="pre">
                        co
                    </span>
                    <span class="pre">
                        https://user@llvm.org/svn/llvm-project/llvm/trunk
                    </span>
                    <span class="pre">
                        llvm
                    </span>
                </code>
            </li>
        </ul>
        <p>
            This will create an ‘
            <code class="docutils literal">
                <span class="pre">
                    llvm
                </span>
            </code>
            ‘ directory in the current directory and fully populate it with the LLVM source code, 
            Makefiles, test directories, and local copies of documentation files.
        </p>
        <p>
            If you want to get a specific release (as opposed to the most recent revision), you can checkout it from the ‘
            <code class="docutils literal">
                <span class="pre">
                    tags
                </span>
            </code>
            ‘ directory (instead of ‘
            <code class="docutils literal">
                <span class="pre">
                    trunk
                </span>
            </code>
            ‘). The following releases are located in the following subdirectories of the ‘
            <code class="docutils literal">
                <span class="pre">
                    tags
                </span>
            </code>
            ‘ directory:
        </p>
        <ul class="simple">
            <li>
                Release 3.4:
                <strong>
                    RELEASE_34/final
                </strong>
            </li>
            <li>
                Release 3.3:
                <strong>
                    RELEASE_33/final
                </strong>
            </li>
            <li>
                Release 3.2:
                <strong>
                    RELEASE_32/final
                </strong>
            </li>
            <li>
                Release 3.1:
                <strong>
                    RELEASE_31/final
                </strong>
            </li>
            <li>
                Release 3.0:
                <strong>
                    RELEASE_30/final
                </strong>
            </li>
            <li>
                Release 2.9:
                <strong>
                    RELEASE_29/final
                </strong>
            </li>
            <li>
                Release 2.8:
                <strong>
                    RELEASE_28
                </strong>
            </li>
            <li>
                Release 2.7:
                <strong>
                    RELEASE_27
                </strong>
            </li>
            <li>
                Release 2.6:
                <strong>
                    RELEASE_26
                </strong>
            </li>
            <li>
                Release 2.5:
                <strong>
                    RELEASE_25
                </strong>
            </li>
            <li>
                Release 2.4:
                <strong>
                    RELEASE_24
                </strong>
            </li>
            <li>
                Release 2.3:
                <strong>
                    RELEASE_23
                </strong>
            </li>
            <li>
                Release 2.2:
                <strong>
                    RELEASE_22
                </strong>
            </li>
            <li>
                Release 2.1:
                <strong>
                    RELEASE_21
                </strong>
            </li>
            <li>
                Release 2.0:
                <strong>
                    RELEASE_20
                </strong>
            </li>
            <li>
                Release 1.9:
                <strong>
                    RELEASE_19
                </strong>
            </li>
            <li>
                Release 1.8:
                <strong>
                    RELEASE_18
                </strong>
            </li>
            <li>
                Release 1.7:
                <strong>
                    RELEASE_17
                </strong>
            </li>
            <li>
                Release 1.6:
                <strong>
                    RELEASE_16
                </strong>
            </li>
            <li>
                Release 1.5:
                <strong>
                    RELEASE_15
                </strong>
            </li>
            <li>
                Release 1.4:
                <strong>
                    RELEASE_14
                </strong>
            </li>
            <li>
                Release 1.3:
                <strong>
                    RELEASE_13
                </strong>
            </li>
            <li>
                Release 1.2:
                <strong>
                    RELEASE_12
                </strong>
            </li>
            <li>
                Release 1.1:
                <strong>
                    RELEASE_11
                </strong>
            </li>
            <li>
                Release 1.0:
                <strong>
                    RELEASE_1
                </strong>
            </li>
        </ul>
        <p>
            If you would like to get the LLVM test suite (a separate package as of
            1.4), you get it from the Subversion repository:
        </p>
        <pre><span></span><span class="gp">%</span> <span class="nb">cd</span> llvm/projects
<span class="gp">%</span> svn co http://llvm.org/svn/llvm-project/test-suite/trunk test-suite
</pre>
        <p>
            By placing it in the
            <code class="docutils literal">
                <span class="pre">
                    llvm/projects
                </span>
            </code>
            , it will be automatically configured by the LLVM cmake configuration.
        </p>
    </div>
    <div class="section" id="git-mirror">
        <h3>
            <a class="toc-backref" href="#id15">
                Git Mirror
            </a>
            <a class="headerlink" href="#git-mirror" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Git mirrors are available for a number of LLVM subprojects. These mirrors
            sync automatically with each Subversion commit and contain all necessary
            git-svn marks (so, you can recreate git-svn metadata locally). Note that
            right now mirrors reflect only
            <code class="docutils literal">
                <span class="pre">
                    trunk
                </span>
            </code>
            for each project. You can do the read-only Git clone of LLVM via:
        </p>
        <pre><span></span><span class="gp">%</span> git clone http://llvm.org/git/llvm.git
</pre>
        <p>
            If you want to check out clang too, run:
        </p>
        <pre><span></span><span class="gp">%</span> <span class="nb">cd</span> llvm/tools
<span class="gp">%</span> git clone http://llvm.org/git/clang.git
</pre>
        <p>
            If you want to check out compiler-rt (required to build the sanitizers),
            run:
        </p>
        <pre><span></span><span class="gp">%</span> <span class="nb">cd</span> llvm/projects
<span class="gp">%</span> git clone http://llvm.org/git/compiler-rt.git
</pre>
        <p>
            If you want to check out libomp (required for OpenMP support), run:
        </p>
        <pre><span></span><span class="gp">%</span> <span class="nb">cd</span> llvm/projects
<span class="gp">%</span> git clone http://llvm.org/git/openmp.git
</pre>
        <p>
            If you want to check out libcxx and libcxxabi (optional), run:
        </p>
        <pre><span></span><span class="gp">%</span> <span class="nb">cd</span> llvm/projects
<span class="gp">%</span> git clone http://llvm.org/git/libcxx.git
<span class="gp">%</span> git clone http://llvm.org/git/libcxxabi.git
</pre>
        <p>
            If you want to check out the Test Suite Source Code (optional), run:
        </p>
        <pre><span></span><span class="gp">%</span> <span class="nb">cd</span> llvm/projects
<span class="gp">%</span> git clone http://llvm.org/git/test-suite.git
</pre>
        <p>
            Since the upstream repository is in Subversion, you should use
            <code class="docutils literal">
                <span class="pre">
                    git
                </span>
                <span class="pre">
                    pull
                </span>
                <span class="pre">
                    --rebase
                </span>
            </code>
            instead of
            <code class="docutils literal">
                <span class="pre">
                    git
                </span>
                <span class="pre">
                    pull
                </span>
            </code>
            to avoid generating a non-linear history in your clone. To configure
            <code class="docutils literal">
                <span class="pre">
                    git
                </span>
                <span class="pre">
                    pull
                </span>
            </code>
            to pass
            <code class="docutils literal">
                <span class="pre">
                    --rebase
                </span>
            </code>
            by default on the master branch, run the following command:
        </p>
        <pre><span></span><span class="gp">%</span> git config branch.master.rebase <span class="nb">true</span>
</pre>
        <div class="section" id="sending-patches-with-git">
            <h4>
                <a class="toc-backref" href="#id16">
                    Sending patches with Git
                </a>
                <a class="headerlink" href="#sending-patches-with-git" title="Permalink to this headline">
                    ¶
                </a>
            </h4>
            <p>
                Please read
                <a class="reference external" href="DeveloperPolicy.html#one-off-patches">
                    Developer Policy
                </a>
                , too.
            </p>
            <p>
                Assume
                <code class="docutils literal">
                    <span class="pre">
                        master
                    </span>
                </code>
                points the upstream and
                <code class="docutils literal">
                    <span class="pre">
                        mybranch
                    </span>
                </code>
                points your working branch, and
                <code class="docutils literal">
                    <span class="pre">
                        mybranch
                    </span>
                </code>
                is rebased onto
                <code class="docutils literal">
                    <span class="pre">
                        master
                    </span>
                </code>
                . At first you may check sanity of whitespaces:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git diff --check master..mybranch
                    </pre>
                </div>
            </div>
            <p>
                The easiest way to generate a patch is as below:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git diff master..mybranch &gt; /path/to/mybranch.diff
                    </pre>
                </div>
            </div>
            <p>
                It is a little different from svn-generated diff. git-diff-generated diff
                has prefixes like
                <code class="docutils literal">
                    <span class="pre">
                        a/
                    </span>
                </code>
                and
                <code class="docutils literal">
                    <span class="pre">
                        b/
                    </span>
                </code>
                . Don’t worry, most developers might know it could be accepted with
                <code class="docutils literal">
                    <span class="pre">
                        patch
                    </span>
                    <span class="pre">
                        -p1
                    </span>
                    <span class="pre">
                        -N
                    </span>
                </code>
                .
            </p>
            <p>
                But you may generate patchset with git-format-patch. It generates by-each-commit
                patchset. To generate patch files to attach to your article:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git format-patch --no-attach master..mybranch -o /path/to/your/patchset
                    </pre>
                </div>
            </div>
            <p>
                If you would like to send patches directly, you may use git-send-email
                or git-imap-send. Here is an example to generate the patchset in Gmail’s
                [Drafts].
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git format-patch --attach master..mybranch --stdout
                        <span class="p">
                            |
                        </span>
                        git imap-send
                    </pre>
                </div>
            </div>
            <p>
                Then, your .git/config should have [imap] sections.
            </p>
            <div class="highlight-ini">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="k">
                            [imap]
                        </span>
                        <span class="na">
                            host
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="s">
                            imaps://imap.gmail.com
                        </span>
                        <span class="s">
                            user = your.gmail.account@gmail.com
                        </span>
                        <span class="s">
                            pass = himitsu!
                        </span>
                        <span class="s">
                            port = 993
                        </span>
                        <span class="s">
                            sslverify = false
                        </span>
                        <span class="c1">
                            ; in English
                        </span>
                        <span class="na">
                            folder
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="s">
                            "[Gmail]/Drafts"
                        </span>
                        <span class="c1">
                            ; example for Japanese, "Modified UTF-7" encoded.
                        </span>
                        <span class="na">
                            folder
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="s">
                            "[Gmail]/&amp;Tgtm+DBN-"
                        </span>
                        <span class="c1">
                            ; example for Traditional Chinese
                        </span>
                        <span class="na">
                            folder
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="s">
                            "[Gmail]/&amp;g0l6Pw-"
                        </span>
                    </pre>
                </div>
            </div>
        </div>
        <div class="section" id="for-developers-to-work-with-git-svn">
            <span id="developers-work-with-git-svn">
            </span>
            <h4>
                <a class="toc-backref" href="#id17">
                    For developers to work with git-svn
                </a>
                <a class="headerlink" href="#for-developers-to-work-with-git-svn" title="Permalink to this headline">
                    ¶
                </a>
            </h4>
            <p>
                To set up clone from which you can submit code using
                <code class="docutils literal">
                    <span class="pre">
                        git-svn
                    </span>
                </code>
                , run:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git clone http://llvm.org/git/llvm.git
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        llvm
                        <span class="gp">
                            %
                        </span>
                        git svn init https://llvm.org/svn/llvm-project/llvm/trunk --username
                        <span class="o">
                            =
                        </span>
                        &lt;username&gt;
                        <span class="gp">
                            %
                        </span>
                        git config svn-remote.svn.fetch :refs/remotes/origin/master
                        <span class="gp">
                            %
                        </span>
                        git svn rebase -l
                        <span class="c1">
                            # -l avoids fetching ahead of the git mirror.
                        </span>
                        <span class="gp">
                            #
                        </span>
                        If you have clang too:
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        tools
                        <span class="gp">
                            %
                        </span>
                        git clone http://llvm.org/git/clang.git
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        clang
                        <span class="gp">
                            %
                        </span>
                        git svn init https://llvm.org/svn/llvm-project/cfe/trunk --username
                        <span class="o">
                            =
                        </span>
                        &lt;username&gt;
                        <span class="gp">
                            %
                        </span>
                        git config svn-remote.svn.fetch :refs/remotes/origin/master
                        <span class="gp">
                            %
                        </span>
                        git svn rebase -l
                    </pre>
                </div>
            </div>
            <p>
                Likewise for compiler-rt, libomp and test-suite.
            </p>
            <p>
                To update this clone without generating git-svn tags that conflict with
                the upstream Git repo, run:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git fetch
                        <span class="o">
                            &amp;&amp;
                        </span>
                        <span class="o">
                            (
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        tools/clang
                        <span class="o">
                            &amp;&amp;
                        </span>
                        git fetch
                        <span class="o">
                            )
                        </span>
                        <span class="c1">
                            # Get matching revisions of both trees.
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git checkout master
                        <span class="gp">
                            %
                        </span>
                        git svn rebase -l
                        <span class="gp">
                            %
                        </span>
                        <span class="o">
                            (
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        tools/clang
                        <span class="o">
                            &amp;&amp;
                        </span>
                        <span class="go">
                            git checkout master &amp;&amp;
                        </span>
                        <span class="go">
                            git svn rebase -l)
                        </span>
                    </pre>
                </div>
            </div>
            <p>
                Likewise for compiler-rt, libomp and test-suite.
            </p>
            <p>
                This leaves your working directories on their master branches, so you’ll
                need to
                <code class="docutils literal">
                    <span class="pre">
                        checkout
                    </span>
                </code>
                each working branch individually and
                <code class="docutils literal">
                    <span class="pre">
                        rebase
                    </span>
                </code>
                it on top of its parent branch.
            </p>
            <p>
                For those who wish to be able to update an llvm repo/revert patches easily
                using git-svn, please look in the directory for the scripts
                <code class="docutils literal">
                    <span class="pre">
                        git-svnup
                    </span>
                </code>
                and
                <code class="docutils literal">
                    <span class="pre">
                        git-svnrevert
                    </span>
                </code>
                .
            </p>
            <p>
                To perform the aforementioned update steps go into your source directory
                and just type
                <code class="docutils literal">
                    <span class="pre">
                        git-svnup
                    </span>
                </code>
                or
                <code class="docutils literal">
                    <span class="pre">
                        git
                    </span>
                    <span class="pre">
                        svnup
                    </span>
                </code>
                and everything will just work.
            </p>
            <p>
                If one wishes to revert a commit with git-svn, but do not want the git
                hash to escape into the commit message, one can use the script
                <code class="docutils literal">
                    <span class="pre">
                        git-svnrevert
                    </span>
                </code>
                or
                <code class="docutils literal">
                    <span class="pre">
                        git
                    </span>
                    <span class="pre">
                        svnrevert
                    </span>
                </code>
                which will take in the git hash for the commit you want to revert, look
                up the appropriate svn revision, and output a message where all references
                to the git hash have been replaced with the svn revision.
            </p>
            <p>
                To commit back changes via git-svn, use
                <code class="docutils literal">
                    <span class="pre">
                        git
                    </span>
                    <span class="pre">
                        svn
                    </span>
                    <span class="pre">
                        dcommit
                    </span>
                </code>
                :
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git svn dcommit
                    </pre>
                </div>
            </div>
            <p>
                Note that git-svn will create one SVN commit for each Git commit you have
                pending, so squash and edit each commit before executing
                <code class="docutils literal">
                    <span class="pre">
                        dcommit
                    </span>
                </code>
                to make sure they all conform to the coding standards and the developers’
                policy.
            </p>
            <p>
                On success,
                <code class="docutils literal">
                    <span class="pre">
                        dcommit
                    </span>
                </code>
                will rebase against the HEAD of SVN, so to avoid conflict, please make
                sure your current branch is up-to-date (via fetch/rebase) before proceeding.
            </p>
            <p>
                The git-svn metadata can get out of sync after you mess around with branches
                and
                <code class="docutils literal">
                    <span class="pre">
                        dcommit
                    </span>
                </code>
                . When that happens,
                <code class="docutils literal">
                    <span class="pre">
                        git
                    </span>
                    <span class="pre">
                        svn
                    </span>
                    <span class="pre">
                        dcommit
                    </span>
                </code>
                stops working, complaining about files with uncommitted changes. The fix
                is to rebuild the metadata:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        rm -rf .git/svn
                        <span class="gp">
                            %
                        </span>
                        git svn rebase -l
                    </pre>
                </div>
            </div>
            <p>
                Please, refer to the Git-SVN manual (
                <code class="docutils literal">
                    <span class="pre">
                        man
                    </span>
                    <span class="pre">
                        git-svn
                    </span>
                </code>
                ) for more information.
            </p>
        </div>
        <div class="section" id="for-developers-to-work-with-a-git-monorepo">
            <h4>
                <a class="toc-backref" href="#id18">
                    For developers to work with a git monorepo
                </a>
                <a class="headerlink" href="#for-developers-to-work-with-a-git-monorepo"
                title="Permalink to this headline">
                    ¶
                </a>
            </h4>
            <div class="admonition note">
                <p class="first admonition-title">
                    Note
                </p>
                <p class="last">
                    This set-up is using unofficial mirror hosted on GitHub, use with caution.
                </p>
            </div>
            <p>
                To set up a clone of all the llvm projects using a unified repository:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            export
                        </span>
                        <span class="nv">
                            TOP_LEVEL_DIR
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="sb">
                            `
                        </span>
                        <span class="nb">
                            pwd
                        </span>
                        <span class="sb">
                            `
                        </span>
                        <span class="gp">
                            %
                        </span>
                        git clone https://github.com/llvm-project/llvm-project/
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        llvm-project
                        <span class="gp">
                            %
                        </span>
                        git config branch.master.rebase
                        <span class="nb">
                            true
                        </span>
                    </pre>
                </div>
            </div>
            <p>
                You can configure various build directory from this clone, starting with
                a build of LLVM alone:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        <span class="nv">
                            $TOP_LEVEL_DIR
                        </span>
                        <span class="gp">
                            %
                        </span>
                        mkdir llvm-build
                        <span class="o">
                            &amp;&amp;
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        llvm-build
                        <span class="gp">
                            %
                        </span>
                        cmake -GNinja ../llvm-project/llvm
                    </pre>
                </div>
            </div>
            <p>
                Or lldb:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        <span class="nv">
                            $TOP_LEVEL_DIR
                        </span>
                        <span class="gp">
                            %
                        </span>
                        mkdir lldb-build
                        <span class="o">
                            &amp;&amp;
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        lldb-build
                        <span class="gp">
                            %
                        </span>
                        cmake -GNinja ../llvm-project/llvm -DLLVM_ENABLE_PROJECTS
                        <span class="o">
                            =
                        </span>
                        lldb
                    </pre>
                </div>
            </div>
            <p>
                Or a combination of multiple projects:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        <span class="nv">
                            $TOP_LEVEL_DIR
                        </span>
                        <span class="gp">
                            %
                        </span>
                        mkdir clang-build
                        <span class="o">
                            &amp;&amp;
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        clang-build
                        <span class="gp">
                            %
                        </span>
                        cmake -GNinja ../llvm-project/llvm -DLLVM_ENABLE_PROJECTS
                        <span class="o">
                            =
                        </span>
                        <span class="s2">
                            "clang;libcxx;libcxxabi"
                        </span>
                    </pre>
                </div>
            </div>
            <p>
                A helper script is provided in
                <cite>
                    llvm/utils/git-svn/git-llvm
                </cite>
                . After you add it to your path, you can push committed changes upstream
                with
                <cite>
                    git llvm push
                </cite>
                .
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            export
                        </span>
                        <span class="nv">
                            PATH
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="nv">
                            $PATH
                        </span>
                        :
                        <span class="nv">
                            $TOP_LEVEL_DIR
                        </span>
                        /llvm-project/llvm/utils/git-svn/
                        <span class="gp">
                            %
                        </span>
                        git llvm push
                    </pre>
                </div>
            </div>
            <p>
                While this is using SVN under the hood, it does not require any interaction
                from you with git-svn. After a few minutes,
                <cite>
                    git pull
                </cite>
                should get back the changes as they were committed. Note that a current
                limitation is that
                <cite>
                    git
                </cite>
                does not directly record file rename, and thus it is propagated to SVN
                as a combination of delete-add instead of a file rename.
            </p>
            <p>
                If you are using
                <cite>
                    arc
                </cite>
                to interact with Phabricator, you need to manually put it at the root
                of the checkout:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        <span class="nv">
                            $TOP_LEVEL_DIR
                        </span>
                        <span class="gp">
                            %
                        </span>
                        cp llvm/.arcconfig ./
                        <span class="gp">
                            %
                        </span>
                        mkdir -p .git/info/
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            echo
                        </span>
                        .arcconfig &gt;&gt; .git/info/exclude
                    </pre>
                </div>
            </div>
        </div>
    </div>
    <div class="section" id="local-llvm-configuration">
        <h3>
            <a class="toc-backref" href="#id19">
                Local LLVM Configuration
            </a>
            <a class="headerlink" href="#local-llvm-configuration" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Once checked out from the Subversion repository, the LLVM suite source
            code must be configured before being built. This process uses CMake. Unlinke
            the normal
            <code class="docutils literal">
                <span class="pre">
                    configure
                </span>
            </code>
            script, CMake generates the build files in whatever format you request
            as well as various
            <code class="docutils literal">
                <span class="pre">
                    *.inc
                </span>
            </code>
            files, and
            <code class="docutils literal">
                <span class="pre">
                    llvm/include/Config/config.h
                </span>
            </code>
            .
        </p>
        <p>
            Variables are passed to
            <code class="docutils literal">
                <span class="pre">
                    cmake
                </span>
            </code>
            on the command line using the format
            <code class="docutils literal">
                <span class="pre">
                    -D&lt;variable
                </span>
                <span class="pre">
                    name&gt;=&lt;value&gt;
                </span>
            </code>
            . The following variables are some common options used by people developing
            LLVM.
        </p>
        <table border="1" class="docutils">
            <colgroup>
                <col width="32%">
                    <col width="68%">
            </colgroup>
            <thead valign="bottom">
                <tr class="row-odd">
                    <th class="head">
                        Variable
                    </th>
                    <th class="head">
                        Purpose
                    </th>
                </tr>
            </thead>
            <tbody valign="top">
                <tr class="row-even">
                    <td>
                        CMAKE_C_COMPILER
                    </td>
                    <td>
                        Tells
                        <code class="docutils literal">
                            <span class="pre">
                                cmake
                            </span>
                        </code>
                        which C compiler to use. By default, this will be /usr/bin/cc.
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        CMAKE_CXX_COMPILER
                    </td>
                    <td>
                        Tells
                        <code class="docutils literal">
                            <span class="pre">
                                cmake
                            </span>
                        </code>
                        which C++ compiler to use. By default, this will be /usr/bin/c++.
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        CMAKE_BUILD_TYPE
                    </td>
                    <td>
                        Tells
                        <code class="docutils literal">
                            <span class="pre">
                                cmake
                            </span>
                        </code>
                        what type of build you are trying to generate files for. Valid options
                        are Debug, Release, RelWithDebInfo, and MinSizeRel. Default is Debug.
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        CMAKE_INSTALL_PREFIX
                    </td>
                    <td>
                        Specifies the install directory to target when running the install action
                        of the build files.
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        LLVM_TARGETS_TO_BUILD
                    </td>
                    <td>
                        A semicolon delimited list controlling which targets will be built and
                        linked into llc. This is equivalent to the
                        <code class="docutils literal">
                            <span class="pre">
                                --enable-targets
                            </span>
                        </code>
                        option in the configure script. The default list is defined as
                        <code class="docutils literal">
                            <span class="pre">
                                LLVM_ALL_TARGETS
                            </span>
                        </code>
                        , and can be set to include out-of-tree targets. The default value includes:
                        <code class="docutils literal">
                            <span class="pre">
                                AArch64,
                            </span>
                            <span class="pre">
                                AMDGPU,
                            </span>
                            <span class="pre">
                                ARM,
                            </span>
                            <span class="pre">
                                BPF,
                            </span>
                            <span class="pre">
                                Hexagon,
                            </span>
                            <span class="pre">
                                Mips,
                            </span>
                            <span class="pre">
                                MSP430,
                            </span>
                            <span class="pre">
                                NVPTX,
                            </span>
                            <span class="pre">
                                PowerPC,
                            </span>
                            <span class="pre">
                                Sparc,
                            </span>
                            <span class="pre">
                                SystemZ,
                            </span>
                            <span class="pre">
                                X86,
                            </span>
                            <span class="pre">
                                XCore
                            </span>
                        </code>
                        .
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        LLVM_ENABLE_DOXYGEN
                    </td>
                    <td>
                        Build doxygen-based documentation from the source code This is disabled
                        by default because it is slow and generates a lot of output.
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        LLVM_ENABLE_SPHINX
                    </td>
                    <td>
                        Build sphinx-based documentation from the source code. This is disabled
                        by default because it is slow and generates a lot of output.
                    </td>
                </tr>
                <tr class="row-odd">
                    <td>
                        LLVM_BUILD_LLVM_DYLIB
                    </td>
                    <td>
                        Generate libLLVM.so. This library contains a default set of LLVM components
                        that can be overridden with
                        <code class="docutils literal">
                            <span class="pre">
                                LLVM_DYLIB_COMPONENTS
                            </span>
                        </code>
                        . The default contains most of LLVM and is defined in
                        <code class="docutils literal">
                            <span class="pre">
                                tools/llvm-shlib/CMakelists.txt
                            </span>
                        </code>
                        .
                    </td>
                </tr>
                <tr class="row-even">
                    <td>
                        LLVM_OPTIMIZED_TABLEGEN
                    </td>
                    <td>
                        Builds a release tablegen that gets used during the LLVM build. This can
                        dramatically speed up debug builds.
                    </td>
                </tr>
            </tbody>
        </table>
        <p>
            To configure LLVM, follow these steps:
        </p>
        <ol class="arabic">
            <li>
                <p class="first">
                    Change directory into the object root directory:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            <span class="nb">
                                cd
                            </span>
                            OBJ_ROOT
                        </pre>
                    </div>
                </div>
            </li>
            <li>
                <p class="first">
                    Run the
                    <code class="docutils literal">
                        <span class="pre">
                            cmake
                        </span>
                    </code>
                    :
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            cmake -G
                            <span class="s2">
                                "Unix Makefiles"
                            </span>
                            -DCMAKE_INSTALL_PREFIX
                            <span class="o">
                                =
                            </span>
                            <span class="nv">
                                prefix
                            </span>
                            <span class="o">
                                =
                            </span>
                            /install/path
                            <span class="go">
                                [other options] SRC_ROOT
                            </span>
                        </pre>
                    </div>
                </div>
            </li>
        </ol>
    </div>
    <div class="section" id="compiling-the-llvm-suite-source-code">
        <h3>
            <a class="toc-backref" href="#id20">
                Compiling the LLVM Suite Source Code
            </a>
            <a class="headerlink" href="#compiling-the-llvm-suite-source-code" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Unlike with autotools, with CMake your build type is defined at configuration.
            If you want to change your build type, you can re-run cmake with the following
            invocation:
        </p>
        <blockquote>
            <div>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            cmake -G
                            <span class="s2">
                                "Unix Makefiles"
                            </span>
                            -DCMAKE_BUILD_TYPE
                            <span class="o">
                                =
                            </span>
                            <span class="nb">
                                type
                            </span>
                            SRC_ROOT
                        </pre>
                    </div>
                </div>
            </div>
        </blockquote>
        <p>
            Between runs, CMake preserves the values set for all options. CMake has
            the following build types defined:
        </p>
        <p>
            Debug
        </p>
        <blockquote>
            <div>
                These builds are the default. The build system will compile the tools
                and libraries unoptimized, with debugging information, and asserts enabled.
            </div>
        </blockquote>
        <p>
            Release
        </p>
        <blockquote>
            <div>
                For these builds, the build system will compile the tools and libraries
                with optimizations enabled and not generate debug info. CMakes default
                optimization level is -O3. This can be configured by setting the
                <code class="docutils literal">
                    <span class="pre">
                        CMAKE_CXX_FLAGS_RELEASE
                    </span>
                </code>
                variable on the CMake command line.
            </div>
        </blockquote>
        <p>
            RelWithDebInfo
        </p>
        <blockquote>
            <div>
                These builds are useful when debugging. They generate optimized binaries
                with debug information. CMakes default optimization level is -O2. This
                can be configured by setting the
                <code class="docutils literal">
                    <span class="pre">
                        CMAKE_CXX_FLAGS_RELWITHDEBINFO
                    </span>
                </code>
                variable on the CMake command line.
            </div>
        </blockquote>
        <p>
            Once you have LLVM configured, you can build it by entering the
            <em>
                OBJ_ROOT
            </em>
            directory and issuing the following command:
        </p>
        <div class="highlight-console">
            <div class="highlight">
                <pre>
                    <span>
                    </span>
                    <span class="gp">
                        %
                    </span>
                    make
                </pre>
            </div>
        </div>
        <p>
            If the build fails, please
            <a class="reference internal" href="#check-here">
                check here
            </a>
            to see if you are using a version of GCC that is known not to compile
            LLVM.
        </p>
        <p>
            If you have multiple processors in your machine, you may wish to use some
            of the parallel build options provided by GNU Make. For example, you could
            use the command:
        </p>
        <div class="highlight-console">
            <div class="highlight">
                <pre>
                    <span>
                    </span>
                    <span class="gp">
                        %
                    </span>
                    make -j2
                </pre>
            </div>
        </div>
        <p>
            There are several special targets which are useful when working with the
            LLVM source code:
        </p>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    make
                </span>
                <span class="pre">
                    clean
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Removes all files generated by the build. This includes object files,
                generated C/C++ files, libraries, and executables.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    make
                </span>
                <span class="pre">
                    install
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Installs LLVM header files, libraries, tools, and documentation in a hierarchy
                under
                <code class="docutils literal">
                    <span class="pre">
                        $PREFIX
                    </span>
                </code>
                , specified with
                <code class="docutils literal">
                    <span class="pre">
                        CMAKE_INSTALL_PREFIX
                    </span>
                </code>
                , which defaults to
                <code class="docutils literal">
                    <span class="pre">
                        /usr/local
                    </span>
                </code>
                .
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    make
                </span>
                <span class="pre">
                    docs-llvm-html
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                If configured with
                <code class="docutils literal">
                    <span class="pre">
                        -DLLVM_ENABLE_SPHINX=On
                    </span>
                </code>
                , this will generate a directory at
                <code class="docutils literal">
                    <span class="pre">
                        OBJ_ROOT/docs/html
                    </span>
                </code>
                which contains the HTML formatted documentation.
            </div>
        </blockquote>
    </div>
    <div class="section" id="cross-compiling-llvm">
        <h3>
            <a class="toc-backref" href="#id21">
                Cross-Compiling LLVM
            </a>
            <a class="headerlink" href="#cross-compiling-llvm" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            It is possible to cross-compile LLVM itself. That is, you can create LLVM
            executables and libraries to be hosted on a platform different from the
            platform where they are built (a Canadian Cross build). To generate build
            files for cross-compiling CMake provides a variable
            <code class="docutils literal">
                <span class="pre">
                    CMAKE_TOOLCHAIN_FILE
                </span>
            </code>
            which can define compiler flags and variables used during the CMake test
            operations.
        </p>
        <p>
            The result of such a build is executables that are not runnable on on
            the build host but can be executed on the target. As an example the following
            CMake invocation can generate build files targeting iOS. This will work
            on Mac OS X with the latest Xcode:
        </p>
        <div class="highlight-console">
            <div class="highlight">
                <pre>
                    <span>
                    </span>
                    <span class="gp">
                        %
                    </span>
                    cmake -G
                    <span class="s2">
                        "Ninja"
                    </span>
                    -DCMAKE_OSX_ARCHITECTURES
                    <span class="o">
                        =
                    </span>
                    <span class="s2">
                        "armv7;armv7s;arm64"
                    </span>
                    <span class="go">
                        -DCMAKE_TOOLCHAIN_FILE=&lt;PATH_TO_LLVM&gt;/cmake/platforms/iOS.cmake
                    </span>
                    <span class="go">
                        -DCMAKE_BUILD_TYPE=Release -DLLVM_BUILD_RUNTIME=Off -DLLVM_INCLUDE_TESTS=Off
                    </span>
                    <span class="go">
                        -DLLVM_INCLUDE_EXAMPLES=Off -DLLVM_ENABLE_BACKTRACES=Off [options]
                    </span>
                    <span class="go">
                        &lt;PATH_TO_LLVM&gt;
                    </span>
                </pre>
            </div>
        </div>
        <p>
            Note: There are some additional flags that need to be passed when building
            for iOS due to limitations in the iOS SDK.
        </p>
        <p>
            Check
            <a class="reference internal" href="HowToCrossCompileLLVM.html">
                <span class="doc">
                    How To Cross-Compile Clang/LLVM using Clang/LLVM
                </span>
            </a>
            and
            <a class="reference external" href="http://clang.llvm.org/docs/CrossCompilation.html">
                Clang docs on how to cross-compile in general
            </a>
            for more information about cross-compiling.
        </p>
    </div>
    <div class="section" id="the-location-of-llvm-object-files">
        <h3>
            <a class="toc-backref" href="#id22">
                The Location of LLVM Object Files
            </a>
            <a class="headerlink" href="#the-location-of-llvm-object-files" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            The LLVM build system is capable of sharing a single LLVM source tree
            among several LLVM builds. Hence, it is possible to build LLVM for several
            different platforms or configurations using the same source tree.
        </p>
        <ul>
            <li>
                <p class="first">
                    Change directory to where the LLVM object files should live:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            <span class="nb">
                                cd
                            </span>
                            OBJ_ROOT
                        </pre>
                    </div>
                </div>
            </li>
            <li>
                <p class="first">
                    Run
                    <code class="docutils literal">
                        <span class="pre">
                            cmake
                        </span>
                    </code>
                    :
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            cmake -G
                            <span class="s2">
                                "Unix Makefiles"
                            </span>
                            SRC_ROOT
                        </pre>
                    </div>
                </div>
            </li>
        </ul>
        <p>
            The LLVM build will create a structure underneath
            <em>
                OBJ_ROOT
            </em>
            that matches the LLVM source tree. At each level where source files are
            present in the source tree there will be a corresponding
            <code class="docutils literal">
                <span class="pre">
                    CMakeFiles
                </span>
            </code>
            directory in the
            <em>
                OBJ_ROOT
            </em>
            . Underneath that directory there is another directory with a name ending
            in
            <code class="docutils literal">
                <span class="pre">
                    .dir
                </span>
            </code>
            under which you’ll find object files for each source.
        </p>
        <p>
            For example:
        </p>
        <blockquote>
            <div>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            <span class="nb">
                                cd
                            </span>
                            llvm_build_dir
                            <span class="gp">
                                %
                            </span>
                            find lib/Support/ -name APFloat*
                            <span class="go">
                                lib/Support/CMakeFiles/LLVMSupport.dir/APFloat.cpp.o
                            </span>
                        </pre>
                    </div>
                </div>
            </div>
        </blockquote>
    </div>
    <div class="section" id="optional-configuration-items">
        <h3>
            <a class="toc-backref" href="#id23">
                Optional Configuration Items
            </a>
            <a class="headerlink" href="#optional-configuration-items" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            If you’re running on a Linux system that supports the
            <a class="reference external" href="http://en.wikipedia.org/wiki/binfmt_misc">
                binfmt_misc
            </a>
            module, and you have root access on the system, you can set your system
            up to execute LLVM bitcode files directly. To do this, use commands like
            this (the first command may not be required if you are already using the
            module):
        </p>
        <div class="highlight-console">
            <div class="highlight">
                <pre>
                    <span>
                    </span>
                    <span class="gp">
                        %
                    </span>
                    mount -t binfmt_misc none /proc/sys/fs/binfmt_misc
                    <span class="gp">
                        %
                    </span>
                    <span class="nb">
                        echo
                    </span>
                    <span class="s1">
                        ':llvm:M::BC::/path/to/lli:'
                    </span>
                    &gt; /proc/sys/fs/binfmt_misc/register
                    <span class="gp">
                        %
                    </span>
                    chmod u+x hello.bc
                    <span class="o">
                        (
                    </span>
                    <span class="k">
                        if
                    </span>
                    needed
                    <span class="o">
                        )
                    </span>
                    <span class="gp">
                        %
                    </span>
                    ./hello.bc
                </pre>
            </div>
        </div>
        <p>
            This allows you to execute LLVM bitcode files directly. On Debian, you
            can also use this command instead of the ‘echo’ command above:
        </p>
        <div class="highlight-console">
            <div class="highlight">
                <pre>
                    <span>
                    </span>
                    <span class="gp">
                        %
                    </span>
                    sudo update-binfmts --install llvm /path/to/lli --magic
                    <span class="s1">
                        'BC'
                    </span>
                </pre>
            </div>
        </div>
    </div>
</div>
<div class="section" id="directory-layout">
    <span id="general-layout">
    </span>
    <span id="program-layout">
    </span>
    <h2>
        <a class="toc-backref" href="#id24">
            Directory Layout
        </a>
        <a class="headerlink" href="#directory-layout" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        One useful source of information about the LLVM source base is the LLVM
        <a class="reference external" href="http://www.doxygen.org/">
            doxygen
        </a>
        documentation available at
        <a class="reference external" href="http://llvm.org/doxygen/">
            http://llvm.org/doxygen/
        </a>
        . The following is a brief introduction to code layout:
    </p>
    <div class="section" id="llvm-examples">
        <h3>
            <a class="toc-backref" href="#id25">
                <code class="docutils literal">
                    <span class="pre">
                        llvm/examples
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#llvm-examples" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Simple examples using the LLVM IR and JIT.
        </p>
    </div>
    <div class="section" id="llvm-include">
        <h3>
            <a class="toc-backref" href="#id26">
                <code class="docutils literal">
                    <span class="pre">
                        llvm/include
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#llvm-include" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Public header files exported from the LLVM library. The three main subdirectories:
        </p>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/include/llvm
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                All LLVM-specific header files, and subdirectories for different portions
                of LLVM:
                <code class="docutils literal">
                    <span class="pre">
                        Analysis
                    </span>
                </code>
                ,
                <code class="docutils literal">
                    <span class="pre">
                        CodeGen
                    </span>
                </code>
                ,
                <code class="docutils literal">
                    <span class="pre">
                        Target
                    </span>
                </code>
                ,
                <code class="docutils literal">
                    <span class="pre">
                        Transforms
                    </span>
                </code>
                , etc...
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/include/llvm/Support
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Generic support libraries provided with LLVM but not necessarily specific
                to LLVM. For example, some C++ STL utilities and a Command Line option
                processing library store header files here.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/include/llvm/Config
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Header files configured by the
                <code class="docutils literal">
                    <span class="pre">
                        configure
                    </span>
                </code>
                script. They wrap “standard” UNIX and C header files. Source code can
                include these header files which automatically take care of the conditional
                #includes that the
                <code class="docutils literal">
                    <span class="pre">
                        configure
                    </span>
                </code>
                script generates.
            </div>
        </blockquote>
    </div>
    <div class="section" id="llvm-lib">
        <h3>
            <a class="toc-backref" href="#id27">
                <code class="docutils literal">
                    <span class="pre">
                        llvm/lib
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#llvm-lib" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Most source files are here. By putting code in libraries, LLVM makes it
            easy to share code among the
            <a class="reference internal" href="#tools">
                tools
            </a>
            .
        </p>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/IR/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Core LLVM source files that implement core classes like Instruction and
                BasicBlock.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/AsmParser/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Source code for the LLVM assembly language parser library.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/Bitcode/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Code for reading and writing bitcode.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/Analysis/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                A variety of program analyses, such as Call Graphs, Induction Variables,
                Natural Loop Identification, etc.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/Transforms/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                IR-to-IR program transformations, such as Aggressive Dead Code Elimination,
                Sparse Conditional Constant Propagation, Inlining, Loop Invariant Code
                Motion, Dead Global Elimination, and many others.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/Target/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Files describing target architectures for code generation. For example,
                <code class="docutils literal">
                    <span class="pre">
                        llvm/lib/Target/X86
                    </span>
                </code>
                holds the X86 machine description.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/CodeGen/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                The major parts of the code generator: Instruction Selector, Instruction
                Scheduling, and Register Allocation.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/MC/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                (FIXME: T.B.D.) ....?
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/ExecutionEngine/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Libraries for directly executing bitcode at runtime in interpreted and
                JIT-compiled scenarios.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm/lib/Support/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Source code that corresponding to the header files in
                <code class="docutils literal">
                    <span class="pre">
                        llvm/include/ADT/
                    </span>
                </code>
                and
                <code class="docutils literal">
                    <span class="pre">
                        llvm/include/Support/
                    </span>
                </code>
                .
            </div>
        </blockquote>
    </div>
    <div class="section" id="llvm-projects">
        <h3>
            <a class="toc-backref" href="#id28">
                <code class="docutils literal">
                    <span class="pre">
                        llvm/projects
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#llvm-projects" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Projects not strictly part of LLVM but shipped with LLVM. This is also
            the directory for creating your own LLVM-based projects which leverage
            the LLVM build system.
        </p>
    </div>
    <div class="section" id="llvm-test">
        <h3>
            <a class="toc-backref" href="#id29">
                <code class="docutils literal">
                    <span class="pre">
                        llvm/test
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#llvm-test" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Feature and regression tests and other sanity checks on LLVM infrastructure.
            These are intended to run quickly and cover a lot of territory without
            being exhaustive.
        </p>
    </div>
    <div class="section" id="test-suite">
        <h3>
            <a class="toc-backref" href="#id30">
                <code class="docutils literal">
                    <span class="pre">
                        test-suite
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#test-suite" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            A comprehensive correctness, performance, and benchmarking test suite
            for LLVM. Comes in a separate Subversion module because not every LLVM
            user is interested in such a comprehensive suite. For details see the
            <a class="reference internal" href="TestingGuide.html">
                <span class="doc">
                    Testing Guide
                </span>
            </a>
            document.
        </p>
    </div>
    <div class="section" id="llvm-tools">
        <span id="tools">
        </span>
        <h3>
            <a class="toc-backref" href="#id31">
                <code class="docutils literal">
                    <span class="pre">
                        llvm/tools
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#llvm-tools" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Executables built out of the libraries above, which form the main part
            of the user interface. You can always get help for a tool by typing
            <code class="docutils literal">
                <span class="pre">
                    tool_name
                </span>
                <span class="pre">
                    -help
                </span>
            </code>
            . The following is a brief introduction to the most important tools. More
            detailed information is in the
            <a class="reference external" href="CommandGuide/index.html">
                Command Guide
            </a>
            .
        </p>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    bugpoint
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                <code class="docutils literal">
                    <span class="pre">
                        bugpoint
                    </span>
                </code>
                is used to debug optimization passes or code generation backends by narrowing
                down the given test case to the minimum number of passes and/or instructions
                that still cause a problem, whether it is a crash or miscompilation. See
                <a class="reference external" href="HowToSubmitABug.html">
                    HowToSubmitABug.html
                </a>
                for more information on using
                <code class="docutils literal">
                    <span class="pre">
                        bugpoint
                    </span>
                </code>
                .
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm-ar
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                The archiver produces an archive containing the given LLVM bitcode files,
                optionally with an index for faster lookup.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm-as
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                The assembler transforms the human readable LLVM assembly to LLVM bitcode.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm-dis
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                The disassembler transforms the LLVM bitcode to human readable LLVM assembly.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvm-link
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                <code class="docutils literal">
                    <span class="pre">
                        llvm-link
                    </span>
                </code>
                , not surprisingly, links multiple LLVM modules into a single program.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    lli
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                <code class="docutils literal">
                    <span class="pre">
                        lli
                    </span>
                </code>
                is the LLVM interpreter, which can directly execute LLVM bitcode (although
                very slowly...). For architectures that support it (currently x86, Sparc,
                and PowerPC), by default,
                <code class="docutils literal">
                    <span class="pre">
                        lli
                    </span>
                </code>
                will function as a Just-In-Time compiler (if the functionality was compiled
                in), and will execute the code
                <em>
                    much
                </em>
                faster than the interpreter.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llc
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                <code class="docutils literal">
                    <span class="pre">
                        llc
                    </span>
                </code>
                is the LLVM backend compiler, which translates LLVM bitcode to a native
                code assembly file or to C code (with the
                <code class="docutils literal">
                    <span class="pre">
                        -march=c
                    </span>
                </code>
                option).
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    opt
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                <p>
                    <code class="docutils literal">
                        <span class="pre">
                            opt
                        </span>
                    </code>
                    reads LLVM bitcode, applies a series of LLVM to LLVM transformations (which
                    are specified on the command line), and outputs the resultant bitcode.
                    ‘
                    <code class="docutils literal">
                        <span class="pre">
                            opt
                        </span>
                        <span class="pre">
                            -help
                        </span>
                    </code>
                    ‘ is a good way to get a list of the program transformations available
                    in LLVM.
                </p>
                <p>
                    <code class="docutils literal">
                        <span class="pre">
                            opt
                        </span>
                    </code>
                    can also run a specific analysis on an input LLVM bitcode file and print
                    the results. Primarily useful for debugging analyses, or familiarizing
                    yourself with what an analysis does.
                </p>
            </div>
        </blockquote>
    </div>
    <div class="section" id="llvm-utils">
        <h3>
            <a class="toc-backref" href="#id32">
                <code class="docutils literal">
                    <span class="pre">
                        llvm/utils
                    </span>
                </code>
            </a>
            <a class="headerlink" href="#llvm-utils" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Utilities for working with LLVM source code; some are part of the build
            process because they are code generators for parts of the infrastructure.
        </p>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    codegen-diff
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                <code class="docutils literal">
                    <span class="pre">
                        codegen-diff
                    </span>
                </code>
                finds differences between code that LLC generates and code that LLI generates.
                This is useful if you are debugging one of them, assuming that the other
                generates correct output. For the full user manual, run
                <code class="docutils literal">
                    <span class="pre">
                        `perldoc
                    </span>
                    <span class="pre">
                        codegen-diff'
                    </span>
                </code>
                .
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    emacs/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Emacs and XEmacs syntax highlighting for LLVM assembly files and TableGen
                description files. See the
                <code class="docutils literal">
                    <span class="pre">
                        README
                    </span>
                </code>
                for information on using them.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    getsrcs.sh
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Finds and outputs all non-generated source files, useful if one wishes
                to do a lot of development across directories and does not want to find
                each file. One way to use it is to run, for example:
                <code class="docutils literal">
                    <span class="pre">
                        xemacs
                    </span>
                    <span class="pre">
                        `utils/getsources.sh`
                    </span>
                </code>
                from the top of the LLVM source tree.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    llvmgrep
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Performs an
                <code class="docutils literal">
                    <span class="pre">
                        egrep
                    </span>
                    <span class="pre">
                        -H
                    </span>
                    <span class="pre">
                        -n
                    </span>
                </code>
                on each source file in LLVM and passes to it a regular expression provided
                on
                <code class="docutils literal">
                    <span class="pre">
                        llvmgrep
                    </span>
                </code>
                ‘s command line. This is an efficient way of searching the source base
                for a particular regular expression.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    makellvm
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Compiles all files in the current directory, then compiles and links the
                tool that is the first argument. For example, assuming you are in
                <code class="docutils literal">
                    <span class="pre">
                        llvm/lib/Target/Sparc
                    </span>
                </code>
                , if
                <code class="docutils literal">
                    <span class="pre">
                        makellvm
                    </span>
                </code>
                is in your path, running
                <code class="docutils literal">
                    <span class="pre">
                        makellvm
                    </span>
                    <span class="pre">
                        llc
                    </span>
                </code>
                will make a build of the current directory, switch to directory
                <code class="docutils literal">
                    <span class="pre">
                        llvm/tools/llc
                    </span>
                </code>
                and build it, causing a re-linking of LLC.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    TableGen/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                Contains the tool used to generate register descriptions, instruction
                set descriptions, and even assemblers from common TableGen description
                files.
            </div>
        </blockquote>
        <p>
            <code class="docutils literal">
                <span class="pre">
                    vim/
                </span>
            </code>
        </p>
        <blockquote>
            <div>
                vim syntax-highlighting for LLVM assembly files and TableGen description
                files. See the
                <code class="docutils literal">
                    <span class="pre">
                        README
                    </span>
                </code>
                for how to use them.
            </div>
        </blockquote>
    </div>
</div>
<div class="section" id="an-example-using-the-llvm-tool-chain">
    <span id="simple-example">
    </span>
    <h2>
        <a class="toc-backref" href="#id33">
            An Example Using the LLVM Tool Chain
        </a>
        <a class="headerlink" href="#an-example-using-the-llvm-tool-chain" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        This section gives an example of using LLVM with the Clang front end.
    </p>
    <div class="section" id="example-with-clang">
        <h3>
            <a class="toc-backref" href="#id34">
                Example with clang
            </a>
            <a class="headerlink" href="#example-with-clang" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <ol class="arabic">
            <li>
                <p class="first">
                    First, create a simple C file, name it ‘hello.c’:
                </p>
                <div class="highlight-c">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="cp">
                                #include
                            </span>
                            <span class="cpf">
                                &lt;stdio.h&gt;
                            </span>
                            <span class="cp">
                            </span>
                            <span class="kt">
                                int
                            </span>
                            <span class="nf">
                                main
                            </span>
                            <span class="p">
                                ()
                            </span>
                            <span class="p">
                                {
                            </span>
                            <span class="n">
                                printf
                            </span>
                            <span class="p">
                                (
                            </span>
                            <span class="s">
                                "hello world
                            </span>
                            <span class="se">
                                \n
                            </span>
                            <span class="s">
                                "
                            </span>
                            <span class="p">
                                );
                            </span>
                            <span class="k">
                                return
                            </span>
                            <span class="mi">
                                0
                            </span>
                            <span class="p">
                                ;
                            </span>
                            <span class="p">
                                }
                            </span>
                        </pre>
                    </div>
                </div>
            </li>
            <li>
                <p class="first">
                    Next, compile the C file into a native executable:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            clang hello.c -o hello
                        </pre>
                    </div>
                </div>
                <div class="admonition note">
                    <p class="first admonition-title">
                        Note
                    </p>
                    <p class="last">
                        Clang works just like GCC by default. The standard -S and -c arguments
                        work as usual (producing a native .s or .o file, respectively).
                    </p>
                </div>
            </li>
            <li>
                <p class="first">
                    Next, compile the C file into an LLVM bitcode file:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            clang -O3 -emit-llvm hello.c -c -o hello.bc
                        </pre>
                    </div>
                </div>
                <p>
                    The -emit-llvm option can be used with the -S or -c options to emit an
                    LLVM
                    <code class="docutils literal">
                        <span class="pre">
                            .ll
                        </span>
                    </code>
                    or
                    <code class="docutils literal">
                        <span class="pre">
                            .bc
                        </span>
                    </code>
                    file (respectively) for the code. This allows you to use the
                    <a class="reference external" href="CommandGuide/index.html">
                        standard LLVM tools
                    </a>
                    on the bitcode file.
                </p>
            </li>
            <li>
                <p class="first">
                    Run the program in both forms. To run the program, use:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            ./hello
                        </pre>
                    </div>
                </div>
                <p>
                    and
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            lli hello.bc
                        </pre>
                    </div>
                </div>
                <p>
                    The second examples shows how to invoke the LLVM JIT,
                    <a class="reference internal" href="CommandGuide/lli.html">
                        <span class="doc">
                            lli
                        </span>
                    </a>
                    .
                </p>
            </li>
            <li>
                <p class="first">
                    Use the
                    <code class="docutils literal">
                        <span class="pre">
                            llvm-dis
                        </span>
                    </code>
                    utility to take a look at the LLVM assembly code:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            llvm-dis &lt; hello.bc
                            <span class="p">
                                |
                            </span>
                            less
                        </pre>
                    </div>
                </div>
            </li>
            <li>
                <p class="first">
                    Compile the program to native assembly using the LLC code generator:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            llc hello.bc -o hello.s
                        </pre>
                    </div>
                </div>
            </li>
            <li>
                <p class="first">
                    Assemble the native assembly language file into a program:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            /opt/SUNWspro/bin/cc -xarch
                            <span class="o">
                                =
                            </span>
                            v9 hello.s -o hello.native
                            <span class="c1">
                                # On Solaris
                            </span>
                            <span class="gp">
                                %
                            </span>
                            gcc hello.s -o hello.native
                            <span class="c1">
                                # On others
                            </span>
                        </pre>
                    </div>
                </div>
            </li>
            <li>
                <p class="first">
                    Execute the native code program:
                </p>
                <div class="highlight-console">
                    <div class="highlight">
                        <pre>
                            <span>
                            </span>
                            <span class="gp">
                                %
                            </span>
                            ./hello.native
                        </pre>
                    </div>
                </div>
                <p>
                    Note that using clang to compile directly to native code (i.e. when the
                    <code class="docutils literal">
                        <span class="pre">
                            -emit-llvm
                        </span>
                    </code>
                    option is not present) does steps 6/7/8 for you.
                </p>
            </li>
        </ol>
    </div>
</div>
<div class="section" id="common-problems">
    <h2>
        <a class="toc-backref" href="#id35">
            Common Problems
        </a>
        <a class="headerlink" href="#common-problems" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        If you are having problems building or using LLVM, or if you have any
        other general questions about LLVM, please consult the
        <a class="reference external" href="FAQ.html">
            Frequently Asked Questions
        </a>
        page.
    </p>
</div>
<div class="section" id="links">
    <span id="id3">
    </span>
    <h2>
        <a class="toc-backref" href="#id36">
            Links
        </a>
        <a class="headerlink" href="#links" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        This document is just an
        <strong>
            introduction
        </strong>
        on how to use LLVM to do some simple things... there are many more interesting
        and complicated things that you can do that aren’t documented here (but
        we’ll gladly accept a patch if you want to write something up!). For more
        information about LLVM, check out:
    </p>
    <ul class="simple">
        <li>
            <a class="reference external" href="http://llvm.org/">
                LLVM Homepage
            </a>
        </li>
        <li>
            <a class="reference external" href="http://llvm.org/doxygen/">
                LLVM Doxygen Tree
            </a>
        </li>
        <li>
            <a class="reference external" href="http://llvm.org/docs/Projects.html">
                Starting a Project that Uses LLVM
            </a>
        </li>
    </ul>
</div>