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
                                        (built于2016年11月14日)
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
                                    其它平台
                                </h3>
                                <p>
                                    对于其它平台，请跟随
                                    <a href="http://clang-analyzer.llvm.org/installation#OtherPlatforms">
                                        说明
                                    </a>
                                    从源码来build分析器。
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
                            在Xcode中查看静态分析的结果
                        </b>
                    </div>
                    <a href="http://clang-analyzer.llvm.org/images/analyzer_html.png">
                        <img src="http://clang-analyzer.llvm.org/images/analyzer_html.png" width="450" alt="analyzer in browser">
                    </a>
                    <div style="text-align:center">
                        <b>
                            在web浏览器中查看静态分析结果
                        </b>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
    <h2 id="StaticAnalysis">
        什么是静态分析？
    </h2>
    <p>
        “静态分析”这个术语是一个组合名词（conflated），但在这里，我们用它来表示一个为自动找出bug，对源码进行分析的算法和技术的集合。这个主意类似于编译的警告（对于找到代码中的错误会非常有用），但又比这更进一步，找到通过传统的，例如测试，的运行时dubug方式才能找到的bug。
    </p>
    <p>
        静态分析找bug的工具，已经从基本的语法分析，到通过推理代码的语义找到深层的bug进化了几十年。Clang静态分析器的目标，是为C，C++，和Objective-C语言的程序，提供一个商业品质的静态分析框架，他是免费可以获取的，可扩展，并有着高质量的实现。
    </p>
    <h3 id="Clang">
        Clang和LLVM的部分
    </h3>
    <p>
        正如它名称所暗示的，Clang静态分析器构建于
        <a href="http://clang.llvm.org">
            Clang
        </a>
        和
        <a href="http://llvm.org">
            LLVM
        </a>
        的顶层。严格地说，这个分析器是Clang的一部分。Clang是由一系列可复用的C++的库构成的，可以用来构建强有力的源码级别的工具。Clang静态分析器使用过的静态分析引擎是一个Clang库，拥有被不同内容和客户端复用的能力。
    </p>
    <h2>
        要考虑的重要的点
    </h2>
    <p>
        当我们相信静态分析器对找到bug是非常有用的，我们要求你在使用时记得一些事。
    </p>
    <h3>
        （半成品）Work-in-Progress
    </h3>
    <p>
        这个分析器是一个可持续加工的产品。这里有很多计划中的增强，来提高精确度，以及分析算法的范围，就如它将要发现的那些bug一样。虽然静态分析能够做什么还有巨大的限制，我们还有很长的路去走，才能叩击到那堵墙。
    </p>
    <h3>
        速度较编译更慢
    </h3>
    <p>
        在执行上，使用静态分析来自动发现深层的程序bug，是一个用CPU时间为代价，来强化代码的交易。由于这个深层的分析，是通过使用最先进技术（state-of-the-art）的静态分析工具执行的，静态分析因此会比编译更慢。
    </p>
    <p>
        尽管Clang静态分析器被设计得尽可能的快和轻量级，请不要期望它想编译一个程序那样快（即使打开优化的情况下）。一些算法需要在最坏的情况下计算来找到bug，造成了指数级的时间。
    </p>
    <p>
        Clang静态分析器通过框定要检查项的数量，还使用聪明的算法来减少它必须要做的用来找到bug的工作的数量，来运行在合理的时间。
    </p>
    <h3>
        错误的报告
    </h3>
    <p>
        静态分析不是完美的。它会有可能在程序中标记错误的bug，但其实那里的代码是正确的。由于一些代码的检查需要更多的分析准确性，在不同的检查中，错误报告的频率将出现非常大的变化。我们的长期目标，是让这个分析器对于大多数的代码能够有较低的错误报告率。
    </p>
    <p>
        请通过
        <a href="http://clang-analyzer.llvm.org/filing_bugs.html">
            报告错误的报告
        </a>
        来尽力帮助我们。错误的报告只有我们知道了才可以解决。
    </p>
    <h3>
        更多检查
    </h3>
    <p>
        静态分析不是魔法；一个静态分析器只能发现被特定设计过要去发现的bug。如果有你想要让Clang静态分析器找出的特定的bug，请放轻松来提出
        <a href="http://clang-analyzer.llvm.org/filing_bugs.html">
            特性请求
        </a>
        或贡献你自己的补丁。
    </p>
</div>
