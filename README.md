# clang_static_analyzer_document_translation
---
#### [原文地址](http://clang-analyzer.llvm.org/) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)



<div id="content">
    <table style="margin-top:0px" width="100%" border="0" cellpadding="0px"
    cellspacing="0">
        <tbody>
            <tr>
                <td>
                    <h1>
                        Clang静态分析器
                    </h1>
                    <p>	
                    	Clang静态分析器是一个源码分析工具，可以找出在C, C++, 和Objective-C中的bug。
                    </p>
                    <p>
                    	当前它既可以作为
                        Currently it can be run either as a
                        <a href="http://clang-analyzer.llvm.org/scan-build.html">
                            standalone tool
                            单独的工具
                        </a>
                        ，也可以
                        or
                        <a href="http://clang-analyzer.llvm.org/xcode.html">
                        	嵌入到Xcode中
                            within Xcode
                        </a>
                        。单的工程是由命令行调用的，它会基于一个代码库的build，串行地运行。
                    </p>
                    <p>
                    	这个分析器是100%开源的，且它是
                        <a href="http://clang.llvm.org">
                            Clang
                        </a>
                        项目的一部分。类似于Clang的其它部分，这个分析器实现为一个C++库，它可以被其它工具和应用使用。
                    </p>
                    <h2>
                        下载
                    </h2>
                    <div style="padding:0px; font-size: 90%">
                        <div class="spiffyfg">
                            <div style="padding:15px">
                                <h3 style="margin:0px;padding:0px">
                                    Mac OS X
                                </h3>
                                <ul>
                                    <li>
                                        Latest build (10.8+):
                                        <br>
                                        <b>
                                            <a href="http://clang-analyzer.llvm.org/downloads/checker-279.tar.bz2">
                                                checker-279.tar.bz2
                                            </a>
                                        </b>
                                        (built November 14, 2016)
                                    </li>
                                    <li>
                                        <a href="http://clang-analyzer.llvm.org/release_notes.html">
                                            发版说明
                                        </a>
                                    </li>
                                    <li>
                                    	这个包即可用于命令行，亦可用在Xcode中
                                    </li>
                                    <li>
                                        <a href="http://clang-analyzer.llvm.org/installation.html">
                                            安装
                                        </a>
                                        和
                                        <a href="http://clang-analyzer.llvm.org/scan-build.html">
                                            用法
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div style="padding:0; margin-top:10px; font-size: 90%">
                        <div class="spiffyfg">
                            <div style="padding:15px">
                                <h3 style="margin:0px;padding:0px">
                                    Other Platforms
                                </h3>
                                <p>
                                    For other platforms, please follow the instructions for
                                    <a href="http://clang-analyzer.llvm.org/installation#OtherPlatforms">
                                        building the analyzer
                                    </a>
                                    from source code.
                                </p>
                                <p>
                                </p>
                            </div>
                        </div>
                    </div>
                </td>
                <td style="padding-left:10px">
                    <a href="http://clang-analyzer.llvm.org/images/analyzer_xcode.png">
                        <img src="http://clang-analyzer.llvm.org/images/analyzer_xcode.png" width="450" alt="analyzer in xcode">
                    </a>
                    <div style="text-align:center">
                        <b>
                            Viewing static analyzer results in Xcode
                        </b>
                    </div>
                    <a href="http://clang-analyzer.llvm.org/images/analyzer_html.png">
                        <img src="http://clang-analyzer.llvm.org/images/analyzer_html.png" width="450" alt="analyzer in browser">
                    </a>
                    <div style="text-align:center">
                        <b>
                            Viewing static analyzer results in a web browser
                        </b>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
    <h2 id="StaticAnalysis">
        What is Static Analysis?
    </h2>
    <p>
        The term "static analysis" is conflated, but here we use it to mean a
        collection of algorithms and techniques used to analyze source code in
        order to automatically find bugs. The idea is similar in spirit to compiler
        warnings (which can be useful for finding coding errors) but to take that
        idea a step further and find bugs that are traditionally found using run-time
        debugging techniques such as testing.
    </p>
    <p>
        Static analysis bug-finding tools have evolved over the last several decades
        from basic syntactic checkers to those that find deep bugs by reasoning
        about the semantics of code. The goal of the Clang Static Analyzer is to
        provide a industrial-quality static analysis framework for analyzing C,
        C++, and Objective-C programs that is freely available, extensible, and
        has a high quality of implementation.
    </p>
    <h3 id="Clang">
        Part of Clang and LLVM
    </h3>
    <p>
        As its name implies, the Clang Static Analyzer is built on top of
        <a href="http://clang.llvm.org">
            Clang
        </a>
        and
        <a href="http://llvm.org">
            LLVM
        </a>
        . Strictly speaking, the analyzer is part of Clang, as Clang consists
        of a set of reusable C++ libraries for building powerful source-level tools.
        The static analysis engine used by the Clang Static Analyzer is a Clang
        library, and has the capability to be reused in different contexts and
        by different clients.
    </p>
    <h2>
        Important Points to Consider
    </h2>
    <p>
        While we believe that the static analyzer is already very useful for finding
        bugs, we ask you to bear in mind a few points when using it.
    </p>
    <h3>
        Work-in-Progress
    </h3>
    <p>
        The analyzer is a continuous work-in-progress. There are many planned
        enhancements to improve both the precision and scope of its analysis algorithms
        as well as the kinds of bugs it will find. While there are fundamental
        limitations to what static analysis can do, we have a long way to go before
        hitting that wall.
    </p>
    <h3>
        Slower than Compilation
    </h3>
    <p>
        Operationally, using static analysis to automatically find deep program
        bugs is about trading CPU time for the hardening of code. Because of the
        deep analysis performed by state-of-the-art static analysis tools, static
        analysis can be much slower than compilation.
    </p>
    <p>
        While the Clang Static Analyzer is being designed to be as fast and light-weight
        as possible, please do not expect it to be as fast as compiling a program
        (even with optimizations enabled). Some of the algorithms needed to find
        bugs require in the worst case exponential time.
    </p>
    <p>
        The Clang Static Analyzer runs in a reasonable amount of time by both
        bounding the amount of checking work it will do as well as using clever
        algorithms to reduce the amount of work it must do to find bugs.
    </p>
    <h3>
        False Positives
    </h3>
    <p>
        Static analysis is not perfect. It can falsely flag bugs in a program
        where the code behaves correctly. Because some code checks require more
        analysis precision than others, the frequency of false positives can vary
        widely between different checks. Our long-term goal is to have the analyzer
        have a low false positive rate for most code on all checks.
    </p>
    <p>
        Please help us in this endeavor by
        <a href="http://clang-analyzer.llvm.org/filing_bugs.html">
            reporting false positives
        </a>
        . False positives cannot be addressed unless we know about them.
    </p>
    <h3>
        More Checks
    </h3>
    <p>
        Static analysis is not magic; a static analyzer can only find bugs that
        it has been specifically engineered to find. If there are specific kinds
        of bugs you would like the Clang Static Analyzer to find, please feel free
        to file
        <a href="http://clang-analyzer.llvm.org/filing_bugs.html">
            feature requests
        </a>
        or contribute your own patches.
    </p>
</div>