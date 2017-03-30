#### [原文地址](http://clang.llvm.org/get_started.html) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div id="content">
    <h1>
        开始：build和执行Clang
    </h1>
    <p>
        本篇将给你最快捷的路径来查看Clang，并演示一些选项。这需要打起精神来（get you up），并以最小的混乱（muss）和烦躁（fuss）来执行。如果你喜欢你看到的，请考虑
        <a href="http://clang.llvm.org/get_involved.html">
            getting involved
        </a>
        和clang社区。如果你撞到了问题，请归档问题到
        <a href="http://llvm.org/bugs/">
            LLVM Bugzilla
        </a>
        。
    </p>
    <h2 id="download">
        Clang版本发布
    </h2>
    <p>
        Clang是作为常规LLVM发布的一部分进行发布的。你可以从
        <a href="http://llvm.org/releases/">
            http://llvm.org/releases/
        </a>
        下载发布的版本。
    </p>
    <p>
        Clang也在全部主要的BSD或GNU/Linux的发布版中有提供，作为它们相应的包系统（packaging systems）的一部分。对于Xcode 4.2，Clang是Mac OS X默认的编译器。
    </p>
    <h2 id="build">
        build clang并与代码一起工作
    </h2>
    <h3 id="buildNix">
        在类Unix系统上
    </h3>
    <p>
        注意：作为一个实验性的配置，你可以对全部的项目使用
        <b>
            single checkout
        </b>
        ，和
        <b>
            easy CMake invocation
        </b>
        ，查看LLVM的文档 “
        <a href="https://github.com/DeveloperLx/clang_static_analyzer_document_translation/blob/master/Getting%20Started%20with%20the%20LLVM%20System.md">
            For developers to work with a git monorepo
        </a>
        “
    </p>
    <p>
        如果你想要查看并build Clang，当前的步骤如下：
    </p>
    <ol>
        <li>
            获取需求的工作。
            <ul>
                <li>
                    查看
                    <a href="http://llvm.org/docs/GettingStarted.html#requirements">
                        Getting Started with the LLVM System - Requirements
                    </a>
                    。
                </li>
                <li>
                    注意运行测试套件也需要Python。从这里获取：
                    <a href="http://www.python.org/download">
                        http://www.python.org/download
                    </a>
                </li>
                <li>
                    标准的build过程使用CMake。从这里获取：
                    <a href="http://www.cmake.org/download">
                        http://www.cmake.org/download
                    </a>
                </li>
            </ul>
        </li>
        <li>
            查看LLVM：
            <ul>
                <li>
                    改变目录到你想要放置llvm目录的位置。
                </li>
                <li>
                    <tt>
                        svn co http://llvm.org/svn/llvm-project/llvm/trunk llvm
                    </tt>
                </li>
            </ul>
        </li>
        <li>
            查看Clang：
            <ul>
                <li>
                    <tt>
                        cd llvm/tools
                    </tt>
                </li>
                <li>
                    <tt>
                        svn co http://llvm.org/svn/llvm-project/cfe/trunk clang
                    </tt>
                </li>
                <li>
                    <tt>
                        cd ../..
                    </tt>
                </li>
            </ul>
        </li>
        <li>
            查看额外的Clang工具：（可选）
            <ul>
                <li>
                    <tt>
                        cd llvm/tools/clang/tools
                    </tt>
                </li>
                <li>
                    <tt>
                        svn co http://llvm.org/svn/llvm-project/clang-tools-extra/trunk extra
                    </tt>
                </li>
                <li>
                    <tt>
                        cd ../../../..
                    </tt>
                </li>
            </ul>
        </li>
        <li>
            查看Compiler-RT (可选)：
            <ul>
                <li>
                    <tt>
                        cd llvm/projects
                    </tt>
                </li>
                <li>
                    <tt>
                        svn co http://llvm.org/svn/llvm-project/compiler-rt/trunk compiler-rt
                    </tt>
                </li>
                <li>
                    <tt>
                        cd ../..
                    </tt>
                </li>
            </ul>
        </li>
        <li>
            查看libcxx：（仅在OS X平台上build并运行Compiler-RT测试时是必须的，对于其它情况下都是可选的）
            <ul>
                <li>
                    <tt>
                        cd llvm/projects
                    </tt>
                </li>
                <li>
                    <tt>
                        svn co http://llvm.org/svn/llvm-project/libcxx/trunk libcxx
                    </tt>
                </li>
                <li>
                    <tt>
                        cd ../..
                    </tt>
                </li>
            </ul>
        </li>
        <li>
            Build LLVM和Clang:
            <ul>
                <li>
                    <tt>
                        mkdir build
                    </tt>
                    (in-tree build is not supported)
                </li>
                <li>
                    <tt>
                        cd build
                    </tt>
                </li>
                <li>
                    <tt>
                        cmake -G "Unix Makefiles" ../llvm
                    </tt>
                </li>
                <li>
                    <tt>
                        make
                    </tt>
                </li>
                <li>
                    这将在debug模式下build LLVM和Clang。
                </li>
                <li>
                    注意：对于随后的Clang开发，你只需运行
                    <tt>
                        make clang
                    </tt>
                    即可。
                </li>
                <li>
                    你可以用CMake来生成几种IDE的项目文件：Xcode，Eclipse CDT4，CodeBlocks，Qt-Creator（使用CodeBlocks生成器），KDevelop3。对于更多的信息请查看
                    <a href="http://llvm.org/docs/CMake.html">
                        Building LLVM with CMake
                    </a>
                    。
                </li>
            </ul>
        </li>
        <li>
            如果你打算使用Clang的C++的支持，你就需要告知它如何来找到你的C++标准库头文件。通常来说，Clang将会探测可用的最好的libstdc++头文件的版本，并使用它们 - 它将查看libstdc++的系统安装的版本，和相邻Clang本身的安装版本。如果你的配置不适用这些情景中的任何一种，你可以使用
            <tt>
                -DGCC_INSTALL_PREFIX
            </tt>
            这个cmake选项来告诉Clang，包含有期望的libstdc++的gcc的安装的位置。
        </li>
        <li>
            事实看（假设你已添加了llvm/build/bin到你的路径中）：
            <ul>
                <li>
                    <tt>
                        clang --help
                    </tt>
                </li>
                <li>
                    <tt>
                        clang file.c -fsyntax-only
                    </tt>
                    （检查正确性）
                </li>
                <li>
                    <tt>
                        clang file.c -S -emit-llvm -o -
                    </tt>
                    （输出未优化过的llvm代码）
                </li>
                <li>
                    <tt>
                        clang file.c -S -emit-llvm -o - -O3
                    </tt>
                </li>
                <li>
                    <tt>
                        clang file.c -S -O3 -o -
                    </tt>
                    （输出本地的机器码）
                </li>
            </ul>
        </li>
        <li>
            运行测试套件：
            <ul>
                <li>
                    <tt>
                        make check-clang
                    </tt>
                </li>
            </ul>
        </li>
    </ol>
    <p>
        如果你在build Clang时遇到了问题，请确保你的LLVM检出和你的Clang检出是相同的。LLVM的界面会随着时间而改变，不匹配的版本不会被期望工作在一起。
    </p>
    <h3>
    	同时build Clang和LLVM：
    </h3>
    <p>
    	一旦你将Clang check到llvm的源码树中，它将与剩余的
        <tt>
            llvm
        </tt>
        一起构建。为了同时一起build所有的LLVM和Clang，只需在LLVM的根目录中运行
        <tt>
            make
        </tt>
        。
    </p>
    <p>
        <em>
            注意：
        </em>
        注意到，Clang在技术上是Subversion仓库中的单独的一部分。正如上面所提到的，最新的Clang源码依赖于最新的LLVM树中的源码。你可以使用
        <tt>
            <b>
                make update
            </b>
        </tt>
        来更新你顶层的LLVM项目，以及在其中的全部（可能都没有关系）的项目。这将在所有相关于subversion的子目录中运行
        <tt>
            svn update
        </tt>
        。
    </p>
    <h3 id="buildWindows">
        使用Visual Studio
    </h3>
    <p>
        下列的细节，可以在Windows上使用Visual Studio设置和build Clang：
    </p>
    <ol>
        <li>
            获取必须的工具：
            <ul>
                <li>
                    <b>
                        Subversion
                    </b>
                    。源码控制程序。从这里获取：
                    <a href="http://subversion.apache.org/packages.html">
                        http://subversion.apache.org/packages.html
                    </a>
                </li>
                <li>
                    <b>
                        CMake
                    </b>
                    。用来生成Visual Studio的解决方案和项目文件。从这里获取：
                    <a href="http://www.cmake.org/cmake/resources/software.html">
                        http://www.cmake.org/cmake/resources/software.html
                    </a>
                </li>
                <li>
                    <b>
                        Visual Studio 2013或更高的版本
                    </b>
                </li>
                <li>
                    <b>
                        Python
                    </b>
                    。这仅在你运行测试时需要（如果你要为clang进行开发，测试时非常必要的）。从这里获取：
                    <a href="http://www.python.org/download/">
                        http://www.python.org/download/
                    </a>
                </li>
                <li>
                    <b>
                        GnuWin32工具
                    </b>
                    这些对于运行测试也是必须的。（注意，由于在搜索字符串中嵌入了双引号，MSYS（Minimal GNU（POSIX）system on Windows 是一个小型的GNU环境）或Cygwin（小型的UNIX模拟环境）的grep无法起作用。但GNU的grep在这个case下是可以正常工作的。）从这里获取：
                    <a href="http://getgnuwin32.sourceforge.net/">
                        http://getgnuwin32.sourceforge.net/
                    </a>
                    。
                </li>
            </ul>
        </li>
        <li>
            获取LLVM:
            <ul>
                <li>
                    <tt>
                        svn co http://llvm.org/svn/llvm-project/llvm/trunk llvm
                    </tt>
                </li>
            </ul>
        </li>
        <li>
            获取Clang:
            <ul>
                <li>
                    <tt>
                        cd llvm\tools
                    </tt>
                </li>
                <li>
                    <tt>
                        svn co http://llvm.org/svn/llvm-project/cfe/trunk clang
                    </tt>
                </li>
            </ul>
            <p>
                <em>
                    注意
                </em>
                ：一些Clang的测试对于行的结尾是敏感的。确保被check的文件没有将LF的行结尾转化为CR+LF的。如果你使用的是git-svn，确保你的
                <tt>
                    core.autocrlf
                </tt>
                设置为false。
            </p>
        </li>
        <li>
            运行CMake来生成Visual Studio的解决方案和项目文件：
            <ul>
                <li>
                    <tt>
                        cd ..\..
                    </tt>
                    （回到你开始的位置）
                </li>
                <li>
                    <tt>
                        mkdir build
                    </tt>
                    （为了在没有污染源码目录的前提下进行build）
                </li>
                <li>
                    <tt>
                        cd build
                    </tt>
                </li>
                <li>
                    如果你正在使用Visual Studio 2013：
                    <tt>
                        cmake -G "Visual Studio 12" ..\llvm
                    </tt>
                </li>
                <li>
                    关于CMake的其它配置选项，查看
                    <a href="http://www.llvm.org/docs/CMake.html">
                        LLVM CMake guide
                    </a>
                    。
                </li>
                <li>
                    如果成功完成了上述步骤，就会创建出一个LLVM.sln文件在
                    <tt>
                        build
                    </tt>
                    目录中。
                </li>
            </ul>
        </li>
        <li>
            构建Clang：
            <ul>
                <li>
                    在Visual Studio中打开LLVM.sln。
                </li>
                <li>
                    仅为编译器驱动和前端build"clang"项目，或者build包括工具在内的”ALL_BUILD“项目。
                </li>
            </ul>
        </li>
        <li>
            尝试一下（假设你已添加了llvm/debug/bin到你的路径中）。（见上面的运行示例）
        </li>
        <li>
            关于在Windows上执行回归测试的相关信息，请参考
            <a href="http://www.llvm.org/hacking.html#testingWindows">
                clang上的黑客攻击 - 使用Visual Studio在Windows上进行测试
            </a>
            。
        </li>
    </ol>
    <p>
        Note that once you have checked out both llvm and clang, to synchronize
        to the latest code base, use the
        <tt>
            svn update
        </tt>
        command in both the llvm and llvm\tools\clang directories, as they are
        separate repositories.
    </p>
    <h2 id="driver">
        Clang Compiler Driver (Drop-in Substitute for GCC)
    </h2>
    <p>
        The
        <tt>
            clang
        </tt>
        tool is the compiler driver and front-end, which is designed to be a drop-in
        replacement for the
        <tt>
            gcc
        </tt>
        command. Here are some examples of how to use the high-level driver:
    </p>
    <pre class="code">
        $
        <b>
            cat t.c
        </b>
        #include &lt;stdio.h&gt; int main(int argc, char **argv) { printf("hello
        world\n"); } $
        <b>
            clang t.c
        </b>
        $
        <b>
            ./a.out
        </b>
        hello world
    </pre>
    <p>
        The 'clang' driver is designed to work as closely to GCC as possible to
        maximize portability. The only major difference between the two is that
        Clang defaults to gnu99 mode while GCC defaults to gnu89 mode. If you see
        weird link-time errors relating to inline functions, try passing -std=gnu89
        to clang.
    </p>
    <h2>
        Examples of using Clang
    </h2>
    <!-- Thanks to http://shiflett.org/blog/2006/oct/formatting-and-highlighting-php-code-listings
    Site suggested using pre in CSS, but doesn't work in IE, so went for the
    <pre>
    tag. -->
    <pre class="code">
        $
        <b>
            cat ~/t.c
        </b>
        typedef float V __attribute__((vector_size(16))); V foo(V a, V b) { return
        a+b*a; }
    </pre>
    <h3>
        Preprocessing:
    </h3>
    <pre class="code">
        $
        <b>
            clang ~/t.c -E
        </b>
        # 1 "/Users/sabre/t.c" 1 typedef float V __attribute__((vector_size(16)));
        V foo(V a, V b) { return a+b*a; }
    </pre>
    <h3>
        Type checking:
    </h3>
    <pre class="code">
        $
        <b>
            clang -fsyntax-only ~/t.c
        </b>
    </pre>
    <h3>
        GCC options:
    </h3>
    <pre class="code">
        $
        <b>
            clang -fsyntax-only ~/t.c -pedantic
        </b>
        /Users/sabre/t.c:2:17:
        <span style="color:magenta">
            warning:
        </span>
        extension used
        <span style="color:darkgreen">
            typedef float V __attribute__((vector_size(16)));
        </span>
        <span style="color:blue">
            ^
        </span>
        1 diagnostic generated.
    </pre>
    <h3>
        Pretty printing from the AST:
    </h3>
    <p>
        Note, the
        <tt>
            -cc1
        </tt>
        argument indicates the compiler front-end, and not the driver, should
        be run. The compiler front-end has several additional Clang specific features
        which are not exposed through the GCC compatible driver interface.
    </p>
    <pre class="code">
        $
        <b>
            clang -cc1 ~/t.c -ast-print
        </b>
        typedef float V __attribute__(( vector_size(16) )); V foo(V a, V b) {
        return a + b * a; }
    </pre>
    <h3>
        Code generation with LLVM:
    </h3>
    <pre class="code">
        $
        <b>
            clang ~/t.c -S -emit-llvm -o -
        </b>
        define &lt;4 x float&gt; @foo(&lt;4 x float&gt; %a, &lt;4 x float&gt;
        %b) { entry: %mul = mul &lt;4 x float&gt; %b, %a %add = add &lt;4 x float&gt;
        %mul, %a ret &lt;4 x float&gt; %add } $
        <b>
            clang -fomit-frame-pointer -O3 -S -o - t.c
        </b>
        <i>
            # On x86_64
        </i>
        ... _foo: Leh_func_begin1: mulps %xmm0, %xmm1 addps %xmm1, %xmm0 ret Leh_func_end1:
    </pre>
</div>
