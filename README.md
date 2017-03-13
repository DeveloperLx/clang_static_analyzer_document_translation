# clang_static_analyzer_document_translation





<div id="content">
    <table style="margin-top:0px" width="100%" border="0" cellpadding="0px"
    cellspacing="0">
        <tbody>
            <tr>
                <td>
                    <h1>
                        Clang Static Analyzer
                    </h1>
                    <p>
                        The Clang Static Analyzer is a source code analysis tool that finds bugs
                        in C, C++, and Objective-C programs.
                    </p>
                    <p>
                        Currently it can be run either as a
                        <a href="scan-build.html">
                            standalone tool
                        </a>
                        or
                        <a href="xcode.html">
                            within Xcode
                        </a>
                        . The standalone tool is invoked from the command line, and is intended
                        to be run in tandem with a build of a codebase.
                    </p>
                    <p>
                        The analyzer is 100% open source and is part of the
                        <a href="http://clang.llvm.org">
                            Clang
                        </a>
                        project. Like the rest of Clang, the analyzer is implemented as a C++
                        library that can be used by other tools and applications.
                    </p>
                    <h2>
                        Download
                    </h2>
                    <div style="padding:0px; font-size: 90%">
                        <b class="spiffy">
                            <b class="spiffy1">
                                <b>
                                </b>
                            </b>
                            <b class="spiffy2">
                                <b>
                                </b>
                            </b>
                            <b class="spiffy3">
                            </b>
                            <b class="spiffy4">
                            </b>
                            <b class="spiffy5">
                            </b>
                        </b>
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
                                            <a href="downloads/checker-279.tar.bz2">
                                                checker-279.tar.bz2
                                            </a>
                                        </b>
                                        (built November 14, 2016)
                                    </li>
                                    <li>
                                        <a href="/release_notes.html">
                                            Release notes
                                        </a>
                                    </li>
                                    <li>
                                        This build can be used both from the command line and from within Xcode
                                    </li>
                                    <li>
                                        <a href="/installation.html">
                                            Installation
                                        </a>
                                        and
                                        <a href="/scan-build.html">
                                            usage
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                        <b class="spiffy">
                            <b class="spiffy5">
                            </b>
                            <b class="spiffy4">
                            </b>
                            <b class="spiffy3">
                            </b>
                            <b class="spiffy2">
                                <b>
                                </b>
                            </b>
                            <b class="spiffy1">
                                <b>
                                </b>
                            </b>
                        </b>
                    </div>
                    <div style="padding:0; margin-top:10px; font-size: 90%">
                        <b class="spiffy">
                            <b class="spiffy1">
                                <b>
                                </b>
                            </b>
                            <b class="spiffy2">
                                <b>
                                </b>
                            </b>
                            <b class="spiffy3">
                            </b>
                            <b class="spiffy4">
                            </b>
                            <b class="spiffy5">
                            </b>
                        </b>
                        <div class="spiffyfg">
                            <div style="padding:15px">
                                <h3 style="margin:0px;padding:0px">
                                    Other Platforms
                                </h3>
                                <p>
                                    For other platforms, please follow the instructions for
                                    <a href="/installation#OtherPlatforms">
                                        building the analyzer
                                    </a>
                                    from source code.
                                </p>
                                <p>
                                </p>
                            </div>
                        </div>
                        <b class="spiffy">
                            <b class="spiffy5">
                            </b>
                            <b class="spiffy4">
                            </b>
                            <b class="spiffy3">
                            </b>
                            <b class="spiffy2">
                                <b>
                                </b>
                            </b>
                            <b class="spiffy1">
                                <b>
                                </b>
                            </b>
                        </b>
                    </div>
                </td>
                <td style="padding-left:10px">
                    <a href="images/analyzer_xcode.png">
                        <img src="images/analyzer_xcode.png" width="450" alt="analyzer in xcode">
                    </a>
                    <div style="text-align:center">
                        <b>
                            Viewing static analyzer results in Xcode
                        </b>
                    </div>
                    <a href="images/analyzer_html.png">
                        <img src="images/analyzer_html.png" width="450" alt="analyzer in browser">
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
        <a href="filing_bugs.html">
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
        <a href="filing_bugs.html">
            feature requests
        </a>
        or contribute your own patches.
    </p>
</div>