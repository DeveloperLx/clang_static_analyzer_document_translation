#### [原文地址](http://clang.llvm.org/get_involved.html) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div id="content">
    <h1>
        参与clang项目
    </h1>
    <p>
        一旦你
        <a href="http://clang.llvm.org/get_started.html">
            查看和build了
        </a>
        clang，并玩转了它，你可能会好奇怎样让它变得更好，以及对它的开发进行贡献。亦或是，你只是想跟随项目的开发来查看它的进度。
    </p>
    <h2>
        贡献
    </h2>
    查看
    <a href="http://clang.llvm.org/hacking.html">
        hacking文档
    </a>
    中的怎么创建patch的相关信息。
    <h2>
        跟随正在进行中的事
    </h2>
    <p>
        Clang是
        <a href="http://llvm.org">
            LLVM Project
        </a>
        的子项目，但拥有自己的mailing列表，因为这个群体中含有不同利益的人。两个clang list是
    </p>
    <ul>
        <li>
            <a href="http://lists.llvm.org/mailman/listinfo/cfe-commits">
                cfe-commits
            </a>
            - 这个列表中是提交和讨论的patch。
        </li>
        <li>
            <a href="http://lists.llvm.org/mailman/listinfo/cfe-dev">
                cfe-dev
            </a>
            - 这个列表中是全部其它的clang相关的事（问题和答案，设计讨论，等等）。
        </li>
    </ul>
    <p>
        如果你只对clang感兴趣，这两个列表就是你全部需要的。如果你感兴趣于LLVM优化器和code生成器，那就也需要考虑登记
        <a href="http://lists.llvm.org/mailman/listinfo/llvm-dev">
            llvm-dev
        </a>
        和
        <a href="http://lists.llvm.org/mailman/listinfo/llvm-commits">
            llvm-commits
        </a>
        。
    </p>
    <p>
        在这个项目上，和其它开发者进行讨论的最好的方式，就是通过
        <a href="http://lists.llvm.org/mailman/listinfo/cfe-dev">
            cfe-dev mailing列表
        </a>
        。clang mailing是一个非常友好的地方，我们欢迎新手。除了cfe-dev列表，相当数量的设计讨论进行在
        <a href="http://lists.llvm.org/mailman/listinfo/cfe-commits">
            cfe-commits mailing列表
        </a>
        中。所有的这些列表都已归档，这样你就可以浏览之前的讨论。或如果偏好的话，跟随这个列表在网上开发。
    </p>
    <p>
        你也可以跟随
        You can also follow the
        <a href="http://planet.clang.org/">
            Planet Clang
        </a>
        社区的新闻流，它提供了一个世界的窗口，Clang的开发者，贡献者以及它们实现的标准都工作并生活在此。
    </p>
    <p>
        如果你正在寻找该做些什么，请访问
        <a href="http://clang.llvm.org/OpenProjects.html">
            Open Projects
        </a>
        ，或浏览
        <a href="http://llvm.org/bugs/">
            Bugzilla bug database
        </a>
        。
    </p>
    <h2 id="criteria">
        向clang贡献扩展
    </h2>
    <p>
    	Clang一直都被设计为一个实验性的平台，让编程者可以轻松地扩展编译器来支持新的语言特性和工具。在某种程度上，这些扩展的作者可以建议将这些扩展编程Clang本身的一部分，来使得整个的Clang社区受益。但并不是每一个idea -- 甚至是每一个很棒的idea -- 都应该成为Clang的一部分。扩展（尤其是语言的扩展）使Clang产生了长期持有的负担，因此这个扩展的利处必须胜过这些代价。因此，下面有7个标准用来评估提议的扩展：
    </p>
    <ol>
        <li>
            重大的用户群体的证明：这基于大量的因素，包括在事实上存在用户群体；在它可用的情况下，用户会采用如此特性的可以感知的可能性；还有来自于它的任何“涓流”效应（"trickle-down" effects），例如，某个库采用了这个特性，并为用户提供了益处。
        </li>
        <li>
            特定的需要存在在Clang树的需求：一些扩展，如果被表达为一个独立的工具，可能会更好一些；即使它们最后被托管，成为了LLVM保护伞（umbrella）项目的一部分，也应当仍然作为独立的工具。
        </li>
        <li>
            完整的规范：这个规范，必须足够去理解特性的设计，以及解释特定例子的含义。这个规范必须足够详细，使得另一个编译器供应者可以很容易地实现其特性。
        </li>
        <li>
            Representation within the appropriate governing organization: For extensions
            to a language governed by a standards committee (C, C++, OpenCL), the extension
            itself must have an active proposal and proponent within that committee
            and have a reasonable chance of acceptance. Clang should drive the standard,
            not diverge from it. This criterion does not apply to all extensions, since
            some extensions fall outside of the realm of the standards bodies.
        </li>
        <li>
            长期支持的计划：
            A long-term support plan: Contributing a non-trivial extension to Clang
            implies a commitment to supporting that extension, improving the implementation
            and specification as Clang evolves. The capacity of the contributor to
            make that commitment is as important as the commitment itself.
        </li>
        <li>
            高质量的实现：
            A high-quality implementation: The implementation must fit well into Clang's
            architecture, follow LLVM's coding conventions, and meet Clang's quality
            standards, including high-quality diagnostics and rich AST representations.
            This is particularly important for language extensions, because users will
            learn how those extensions work through the behavior of the compiler.
        </li>
        <li>
            适当的测试组件：
            A proper test suite: Extensive testing is crucial to ensure that the language
            extension is not broken by ongoing maintenance in Clang. The test suite
            should be complete enough that another compiler vendor could conceivably
            validate their implementation of the feature against it.
        </li>
    </ol>
</div>