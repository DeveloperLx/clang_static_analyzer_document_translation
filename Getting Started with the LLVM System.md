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
        欢迎来到LLVM！为了入行，你首先需要了解一些基本的信息。
    </p>
    <p>
        首先，LLVM有三个部分。第一块是LLVM套件。它包含使用LLVM所需的全部的工具，库，以及头文件。它包含一个汇编程序，反汇编程序，字节码分析器和字节码优化器。它还包含基本的回归测试，可以用来测试LLVM工具和Clang前端。
    </p>
    <p>
        第二块则是
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
        可能也是一个不错的入门的地方。
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
                记住，你被警告了两次要阅读文档。
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
                获取Compiler-RT（build sanitizers所必须的）
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
                    Warning:
                </em>
                Make sure you’ve checked out
                <em>
                    all of
                </em>
                the source code before trying to configure with cmake. cmake does not
                pickup newly added source directories in incremental builds.
            </p>
            <p>
                The build uses
                <a class="reference external" href="CMake.html">
                    CMake
                </a>
                . LLVM requires CMake 3.4.3 to build. It is generally recommended to use
                a recent CMake, especially if you’re generating Ninja build files. This
                is because the CMake project is constantly improving the quality of the
                generators, and the Ninja generator gets a lot of attention.
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
                        Some common generators are:
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
                            — for generating make-compatible parallel makefiles.
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    Ninja
                                </span>
                            </code>
                            — for generating
                            <a class="reference external" href="https://ninja-build.org">
                                Ninja
                            </a>
                            build files. Most llvm developers use Ninja.
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
                            — for generating Visual Studio projects and solutions.
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    Xcode
                                </span>
                            </code>
                            — for generating Xcode projects.
                        </li>
                    </ul>
                    <p>
                        Some Common options:
                    </p>
                    <ul class="simple">
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    -DCMAKE_INSTALL_PREFIX=directory
                                </span>
                            </code>
                            — Specify for
                            <em>
                                directory
                            </em>
                            the full pathname of where you want the LLVM tools and libraries to be
                            installed (default
                            <code class="docutils literal">
                                <span class="pre">
                                    /usr/local
                                </span>
                            </code>
                            ).
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    -DCMAKE_BUILD_TYPE=type
                                </span>
                            </code>
                            — Valid options for
                            <em>
                                type
                            </em>
                            are Debug, Release, RelWithDebInfo, and MinSizeRel. Default is Debug.
                        </li>
                        <li>
                            <code class="docutils literal">
                                <span class="pre">
                                    -DLLVM_ENABLE_ASSERTIONS=On
                                </span>
                            </code>
                            — Compile with assertion checks enabled (default is Yes for Debug builds,
                            No for all other build types).
                        </li>
                    </ul>
                </li>
                <li>
                    <p class="first">
                        Run your build tool of choice!
                    </p>
                    <ul class="simple">
                        <li>
                            The default target (i.e.
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                            </code>
                            ) will build all of LLVM
                        </li>
                        <li>
                            The
                            <code class="docutils literal">
                                <span class="pre">
                                    check-all
                                </span>
                            </code>
                            target (i.e.
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                                <span class="pre">
                                    check-all
                                </span>
                            </code>
                            ) will run the regression tests to ensure everything is in working order.
                        </li>
                        <li>
                            CMake will generate build targets for each tool and library, and most
                            LLVM sub-projects generate their own
                            <code class="docutils literal">
                                <span class="pre">
                                    check-&lt;project&gt;
                                </span>
                            </code>
                            target.
                        </li>
                        <li>
                            Running a serial build will be
                            <em>
                                slow
                            </em>
                            . Make sure you run a parallel build; for
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                            </code>
                            , use
                            <code class="docutils literal">
                                <span class="pre">
                                    make
                                </span>
                                <span class="pre">
                                    -j
                                </span>
                            </code>
                            .
                        </li>
                    </ul>
                </li>
                <li>
                    <p class="first">
                        For more information see
                        <a class="reference external" href="CMake.html">
                            CMake
                        </a>
                    </p>
                </li>
                <li>
                    <p class="first">
                        If you get an “internal compiler error (ICE)” or test failures, see
                        <a class="reference internal" href="#below">
                            below
                        </a>
                        .
                    </p>
                </li>
            </ul>
        </li>
    </ol>
    <p>
        Consult the
        <a class="reference internal" href="#getting-started-with-llvm">
            Getting Started with LLVM
        </a>
        section for detailed information on configuring and compiling LLVM. Go
        to
        <a class="reference internal" href="#directory-layout">
            Directory Layout
        </a>
        to learn about the layout of the source code tree.
    </p>
</div>
<div class="section" id="requirements">
    <h2>
        <a class="toc-backref" href="#id6">
            Requirements
        </a>
        <a class="headerlink" href="#requirements" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        Before you begin to use the LLVM system, review the requirements given
        below. This may save you some trouble by knowing ahead of time what hardware
        and software you will need.
    </p>
    <div class="section" id="hardware">
        <h3>
            <a class="toc-backref" href="#id7">
                Hardware
            </a>
            <a class="headerlink" href="#hardware" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            LLVM is known to work on the following host platforms:
        </p>
        <table border="1" class="docutils">
            <colgroup>
                <col width="35%">
                    <col width="40%">
                        <col width="25%">
            </colgroup>
            <thead valign="bottom">
                <tr class="row-odd">
                    <th class="head">
                        OS
                    </th>
                    <th class="head">
                        Arch
                    </th>
                    <th class="head">
                        Compilers
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
                Note
            </p>
            <ol class="last arabic simple">
                <li>
                    Code generation supported for Pentium processors and up
                </li>
                <li>
                    Code generation supported for 32-bit ABI only
                </li>
                <li>
                    To use LLVM modules on Win32-based system, you may configure LLVM with
                    <code class="docutils literal">
                        <span class="pre">
                            -DBUILD_SHARED_LIBS=On
                        </span>
                    </code>
                    .
                </li>
                <li>
                    MCJIT not working well pre-v7, old JIT engine not supported any more.
                </li>
            </ol>
        </div>
        <p>
            Note that Debug builds require a lot of time and disk space. An LLVM-only
            build will need about 1-3 GB of space. A full build of LLVM and Clang will
            need around 15-20 GB of disk space. The exact space requirements will vary
            by system. (It is so large because of all the debugging information and
            the fact that the libraries are statically linked into multiple tools).
        </p>
        <p>
            If you you are space-constrained, you can build only selected tools or
            only selected targets. The Release build requires considerably less space.
        </p>
        <p>
            The LLVM suite
            <em>
                may
            </em>
            compile on other platforms, but it is not guaranteed to do so. If compilation
            is successful, the LLVM utilities should be able to assemble, disassemble,
            analyze, and optimize LLVM bitcode. Code generation should work as well,
            although the generated native code may not work on your platform.
        </p>
    </div>
    <div class="section" id="software">
        <h3>
            <a class="toc-backref" href="#id8">
                Software
            </a>
            <a class="headerlink" href="#software" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Compiling LLVM requires that you have several software packages installed.
            The table below lists those required packages. The Package column is the
            usual name for the software package that LLVM depends on. The Version column
            provides “known to work” versions of the package. The Notes column describes
            how LLVM uses the package and provides other details.
        </p>
        <table border="1" class="docutils">
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
                Note
            </p>
            <ol class="last arabic simple">
                <li>
                    Only the C and C++ languages are needed so there’s no need to build the
                    other languages for LLVM’s purposes. See
                    <cite>
                        below
                    </cite>
                    for specific version info.
                </li>
                <li>
                    Only needed if you want to run the automated test suite in the
                    <code class="docutils literal">
                        <span class="pre">
                            llvm/test
                        </span>
                    </code>
                    directory.
                </li>
                <li>
                    Optional, adds compression / uncompression capabilities to selected LLVM
                    tools.
                </li>
            </ol>
        </div>
        <p>
            Additionally, your compilation host is expected to have the usual plethora
            of Unix utilities. Specifically:
        </p>
        <ul class="simple">
            <li>
                <strong>
                    ar
                </strong>
                — archive library builder
            </li>
            <li>
                <strong>
                    bzip2
                </strong>
                — bzip2 command for distribution generation
            </li>
            <li>
                <strong>
                    bunzip2
                </strong>
                — bunzip2 command for distribution checking
            </li>
            <li>
                <strong>
                    chmod
                </strong>
                — change permissions on a file
            </li>
            <li>
                <strong>
                    cat
                </strong>
                — output concatenation utility
            </li>
            <li>
                <strong>
                    cp
                </strong>
                — copy files
            </li>
            <li>
                <strong>
                    date
                </strong>
                — print the current date/time
            </li>
            <li>
                <strong>
                    echo
                </strong>
                — print to standard output
            </li>
            <li>
                <strong>
                    egrep
                </strong>
                — extended regular expression search utility
            </li>
            <li>
                <strong>
                    find
                </strong>
                — find files/dirs in a file system
            </li>
            <li>
                <strong>
                    grep
                </strong>
                — regular expression search utility
            </li>
            <li>
                <strong>
                    gzip
                </strong>
                — gzip command for distribution generation
            </li>
            <li>
                <strong>
                    gunzip
                </strong>
                — gunzip command for distribution checking
            </li>
            <li>
                <strong>
                    install
                </strong>
                — install directories/files
            </li>
            <li>
                <strong>
                    mkdir
                </strong>
                — create a directory
            </li>
            <li>
                <strong>
                    mv
                </strong>
                — move (rename) files
            </li>
            <li>
                <strong>
                    ranlib
                </strong>
                — symbol table builder for archive libraries
            </li>
            <li>
                <strong>
                    rm
                </strong>
                — remove (delete) files and directories
            </li>
            <li>
                <strong>
                    sed
                </strong>
                — stream editor for transforming output
            </li>
            <li>
                <strong>
                    sh
                </strong>
                — Bourne shell for make build scripts
            </li>
            <li>
                <strong>
                    tar
                </strong>
                — tape archive for distribution generation
            </li>
            <li>
                <strong>
                    test
                </strong>
                — test things in file system
            </li>
            <li>
                <strong>
                    unzip
                </strong>
                — unzip command for distribution checking
            </li>
            <li>
                <strong>
                    zip
                </strong>
                — zip command for distribution generation
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
                Host C++ Toolchain, both Compiler and Standard Library
            </a>
            <a class="headerlink" href="#host-c-toolchain-both-compiler-and-standard-library"
            title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            LLVM is very demanding of the host C++ compiler, and as such tends to
            expose bugs in the compiler. We are also planning to follow improvements
            and developments in the C++ language and library reasonably closely. As
            such, we require a modern host C++ toolchain, both compiler and standard
            library, in order to build LLVM.
        </p>
        <p>
            For the most popular host toolchains we check for specific minimum versions
            in our build systems:
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
            Anything older than these toolchains
            <em>
                may
            </em>
            work, but will require forcing the build system with a special option
            and is not really a supported host platform. Also note that older versions
            of these compilers have often crashed or miscompiled LLVM.
        </p>
        <p>
            For less widely used host toolchains such as ICC or xlC, be aware that
            a very recent version may be required to support all of the C++ features
            used in LLVM.
        </p>
        <p>
            We track certain versions of software that are
            <em>
                known
            </em>
            to fail when used as part of the host toolchain. These even include linkers
            at times.
        </p>
        <p>
            <strong>
                GNU ld 2.16.X
            </strong>
            . Some 2.16.X versions of the ld linker will produce very long warning
            messages complaining that some “
            <code class="docutils literal">
                <span class="pre">
                    .gnu.linkonce.t.*
                </span>
            </code>
            ” symbol was defined in a discarded section. You can safely ignore these
            messages as they are erroneous and the linkage is correct. These messages
            disappear using ld 2.17.
        </p>
        <p>
            <strong>
                GNU binutils 2.17
            </strong>
            : Binutils 2.17 contains
            <a class="reference external" href="http://sourceware.org/bugzilla/show_bug.cgi?id=3111">
                a bug
            </a>
            which causes huge link times (minutes instead of seconds) when building
            LLVM. We recommend upgrading to a newer version (2.17.50.0.4 or later).
        </p>
        <p>
            <strong>
                GNU Binutils 2.19.1 Gold
            </strong>
            : This version of Gold contained
            <a class="reference external" href="http://sourceware.org/bugzilla/show_bug.cgi?id=9836">
                a bug
            </a>
            which causes intermittent failures when building LLVM with position independent
            code. The symptom is an error about cyclic dependencies. We recommend upgrading
            to a newer version of Gold.
        </p>
        <div class="section" id="getting-a-modern-host-c-toolchain">
            <h4>
                <a class="toc-backref" href="#id10">
                    Getting a Modern Host C++ Toolchain
                </a>
                <a class="headerlink" href="#getting-a-modern-host-c-toolchain" title="Permalink to this headline">
                    ¶
                </a>
            </h4>
            <p>
                This section mostly applies to Linux and older BSDs. On Mac OS X, you
                should have a sufficiently modern Xcode, or you will likely need to upgrade
                until you do. Windows does not have a “system compiler”, so you must install
                either Visual Studio 2015 or a recent version of mingw64. FreeBSD 10.0
                and newer have a modern Clang as the system compiler.
            </p>
            <p>
                However, some Linux distributions and some other or older BSDs sometimes
                have extremely old versions of GCC. These steps attempt to help you upgrade
                you compiler even on such a system. However, if at all possible, we encourage
                you to use a recent version of a distribution with a modern system compiler
                that meets these requirements. Note that it is tempting to to install a
                prior version of Clang and libc++ to be the host compiler, however libc++
                was not well tested or set up to build on Linux until relatively recently.
                As a consequence, this guide suggests just using libstdc++ and a modern
                GCC as the initial host in a bootstrap, and then using Clang (and potentially
                libc++).
            </p>
            <p>
                The first step is to get a recent GCC toolchain installed. The most common
                distribution on which users have struggled with the version requirements
                is Ubuntu Precise, 12.04 LTS. For this distribution, one easy option is
                to install the
                <a class="reference external" href="https://launchpad.net/~ubuntu-toolchain-r/+archive/test">
                    toolchain testing PPA
                </a>
                and use it to install a modern GCC. There is a really nice discussions
                of this on the
                <a class="reference external" href="http://askubuntu.com/questions/271388/how-to-install-gcc-4-8-in-ubuntu-12-04-from-the-terminal">
                    ask ubuntu stack exchange
                </a>
                . However, not all users can use PPAs and there are many other distributions,
                so it may be necessary (or just useful, if you’re here you
                <em>
                    are
                </em>
                doing compiler development after all) to build and install GCC from source.
                It is also quite easy to do these days.
            </p>
            <p>
                Easy steps for installing GCC 4.8.2:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        wget https://ftp.gnu.org/gnu/gcc/gcc-4.8.2/gcc-4.8.2.tar.bz2
                        <span class="gp">
                            %
                        </span>
                        wget https://ftp.gnu.org/gnu/gcc/gcc-4.8.2/gcc-4.8.2.tar.bz2.sig
                        <span class="gp">
                            %
                        </span>
                        wget https://ftp.gnu.org/gnu/gnu-keyring.gpg
                        <span class="gp">
                            %
                        </span>
                        <span class="nv">
                            signature_invalid
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="sb">
                            `
                        </span>
                        gpg --verify --no-default-keyring --keyring ./gnu-keyring.gpg gcc-4.8.2.tar.bz2.sig
                        <span class="sb">
                            `
                        </span>
                        <span class="gp">
                            %
                        </span>
                        <span class="k">
                            if
                        </span>
                        <span class="o">
                            [
                        </span>
                        <span class="nv">
                            $signature_invalid
                        </span>
                        <span class="o">
                            ]
                        </span>
                        <span class="p">
                            ;
                        </span>
                        <span class="k">
                            then
                        </span>
                        <span class="nb">
                            echo
                        </span>
                        <span class="s2">
                            "Invalid signature"
                        </span>
                        <span class="p">
                            ;
                        </span>
                        <span class="nb">
                            exit
                        </span>
                        <span class="m">
                            1
                        </span>
                        <span class="p">
                            ;
                        </span>
                        <span class="k">
                            fi
                        </span>
                        <span class="gp">
                            %
                        </span>
                        tar -xvjf gcc-4.8.2.tar.bz2
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        gcc-4.8.2
                        <span class="gp">
                            %
                        </span>
                        ./contrib/download_prerequisites
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        ..
                        <span class="gp">
                            %
                        </span>
                        mkdir gcc-4.8.2-build
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        gcc-4.8.2-build
                        <span class="gp">
                            %
                        </span>
                        <span class="nv">
                            $PWD
                        </span>
                        /../gcc-4.8.2/configure --prefix
                        <span class="o">
                            =
                        </span>
                        <span class="nv">
                            $HOME
                        </span>
                        /toolchains --enable-languages
                        <span class="o">
                            =
                        </span>
                        c,c++
                        <span class="gp">
                            %
                        </span>
                        make -j
                        <span class="k">
                            $(
                        </span>
                        nproc
                        <span class="k">
                            )
                        </span>
                        <span class="gp">
                            %
                        </span>
                        make install
                    </pre>
                </div>
            </div>
            <p>
                For more details, check out the excellent
                <a class="reference external" href="http://gcc.gnu.org/wiki/InstallingGCC">
                    GCC wiki entry
                </a>
                , where I got most of this information from.
            </p>
            <p>
                Once you have a GCC toolchain, configure your build of LLVM to use the
                new toolchain for your host compiler and C++ standard library. Because
                the new version of libstdc++ is not on the system library search path,
                you need to pass extra linker flags so that it can be found at link time
                (
                <code class="docutils literal">
                    <span class="pre">
                        -L
                    </span>
                </code>
                ) and at runtime (
                <code class="docutils literal">
                    <span class="pre">
                        -rpath
                    </span>
                </code>
                ). If you are using CMake, this invocation should produce working binaries:
            </p>
            <div class="highlight-console">
                <div class="highlight">
                    <pre>
                        <span>
                        </span>
                        <span class="gp">
                            %
                        </span>
                        mkdir build
                        <span class="gp">
                            %
                        </span>
                        <span class="nb">
                            cd
                        </span>
                        build
                        <span class="gp">
                            %
                        </span>
                        <span class="nv">
                            CC
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="nv">
                            $HOME
                        </span>
                        /toolchains/bin/gcc
                        <span class="nv">
                            CXX
                        </span>
                        <span class="o">
                            =
                        </span>
                        <span class="nv">
                            $HOME
                        </span>
                        /toolchains/bin/g++
                        <span class="se">
                            \
                        </span>
                        <span class="go">
                            cmake .. -DCMAKE_CXX_LINK_FLAGS="-Wl,-rpath,$HOME/toolchains/lib64 -L$HOME/toolchains/lib64"
                        </span>
                    </pre>
                </div>
            </div>
            <p>
                If you fail to set rpath, most LLVM binaries will fail on startup with
                a message from the loader similar to
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
                . This means you need to tweak the -rpath linker flag.
            </p>
            <p>
                When you build Clang, you will need to give
                <em>
                    it
                </em>
                access to modern C++11 standard library in order to use it as your new
                host in part of a bootstrap. There are two easy ways to do this, either
                build (and install) libc++ along with Clang and then use it with the
                <code class="docutils literal">
                    <span class="pre">
                        -stdlib=libc++
                    </span>
                </code>
                compile and link flag, or install Clang into the same prefix (
                <code class="docutils literal">
                    <span class="pre">
                        $HOME/toolchains
                    </span>
                </code>
                above) as GCC. Clang will look within its own prefix for libstdc++ and
                use it if found. You can also add an explicit prefix for Clang to look
                in for a GCC toolchain with the
                <code class="docutils literal">
                    <span class="pre">
                        --gcc-toolchain=/opt/my/gcc/prefix
                    </span>
                </code>
                flag, passing it to both compile and link commands when using your just-built-Clang
                to bootstrap.
            </p>
        </div>
    </div>
</div>
<div class="section" id="getting-started-with-llvm">
    <span id="id2">
    </span>
    <h2>
        <a class="toc-backref" href="#id11">
            Getting Started with LLVM
        </a>
        <a class="headerlink" href="#getting-started-with-llvm" title="Permalink to this headline">
            ¶
        </a>
    </h2>
    <p>
        The remainder of this guide is meant to get you up and running with LLVM
        and to give you some basic information about the LLVM environment.
    </p>
    <p>
        The later sections of this guide describe the
        <a class="reference internal" href="#general-layout">
            general layout
        </a>
        of the LLVM source tree, a
        <a class="reference internal" href="#simple-example">
            simple example
        </a>
        using the LLVM tool chain, and
        <a class="reference internal" href="#links">
            links
        </a>
        to find more information about LLVM or to get help via e-mail.
    </p>
    <div class="section" id="terminology-and-notation">
        <h3>
            <a class="toc-backref" href="#id12">
                Terminology and Notation
            </a>
            <a class="headerlink" href="#terminology-and-notation" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            Throughout this manual, the following names are used to denote paths specific
            to the local system and working environment.
            <em>
                These are not environment variables you need to set but just strings used
                in the rest of this document below
            </em>
            . In any of the examples below, simply replace each of these names with
            the appropriate pathname on your local system. All these paths are absolute:
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
                This is the top level directory of the LLVM source tree.
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
                This is the top level directory of the LLVM object tree (i.e. the tree
                where object files and compiled programs will be placed. It can be the
                same as SRC_ROOT).
            </div>
        </blockquote>
    </div>
    <div class="section" id="unpacking-the-llvm-archives">
        <h3>
            <a class="toc-backref" href="#id13">
                Unpacking the LLVM Archives
            </a>
            <a class="headerlink" href="#unpacking-the-llvm-archives" title="Permalink to this headline">
                ¶
            </a>
        </h3>
        <p>
            If you have the LLVM distribution, you will need to unpack it before you
            can begin to compile it. LLVM is distributed as a set of two files: the
            LLVM suite and the LLVM GCC front end compiled for your platform. There
            is an additional test suite that is optional. Each file is a TAR archive
            that is compressed with the gzip program.
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
            If you have access to our Subversion repository, you can get a fresh copy
            of the entire source code. All you need to do is check it out from Subversion
            as follows:
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
            ‘ directory in the current directory and fully populate it with the LLVM
            source code, Makefiles, test directories, and local copies of documentation
            files.
        </p>
        <p>
            If you want to get a specific release (as opposed to the most recent revision),
            you can checkout it from the ‘
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
            ‘). The following releases are located in the following subdirectories
            of the ‘
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
                    llvm/projects
                    <span class="gp">
                        %
                    </span>
                    svn co http://llvm.org/svn/llvm-project/test-suite/trunk test-suite
                </pre>
            </div>
        </div>
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
        <div class="highlight-console">
            <div class="highlight">
                <pre>
                    <span>
                    </span>
                    <span class="gp">
                        %
                    </span>
                    git clone http://llvm.org/git/llvm.git
                </pre>
            </div>
        </div>
        <p>
            If you want to check out clang too, run:
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
                    llvm/tools
                    <span class="gp">
                        %
                    </span>
                    git clone http://llvm.org/git/clang.git
                </pre>
            </div>
        </div>
        <p>
            If you want to check out compiler-rt (required to build the sanitizers),
            run:
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
                    llvm/projects
                    <span class="gp">
                        %
                    </span>
                    git clone http://llvm.org/git/compiler-rt.git
                </pre>
            </div>
        </div>
        <p>
            If you want to check out libomp (required for OpenMP support), run:
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
                    llvm/projects
                    <span class="gp">
                        %
                    </span>
                    git clone http://llvm.org/git/openmp.git
                </pre>
            </div>
        </div>
        <p>
            If you want to check out libcxx and libcxxabi (optional), run:
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
                    llvm/projects
                    <span class="gp">
                        %
                    </span>
                    git clone http://llvm.org/git/libcxx.git
                    <span class="gp">
                        %
                    </span>
                    git clone http://llvm.org/git/libcxxabi.git
                </pre>
            </div>
        </div>
        <p>
            If you want to check out the Test Suite Source Code (optional), run:
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
                    llvm/projects
                    <span class="gp">
                        %
                    </span>
                    git clone http://llvm.org/git/test-suite.git
                </pre>
            </div>
        </div>
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
        <div class="highlight-console">
            <div class="highlight">
                <pre>
                    <span>
                    </span>
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