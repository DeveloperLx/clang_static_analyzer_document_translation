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
        的子项目，但拥有自己的邮件列表，因为这个群体中含有不同利益的人。两个clang list是
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
        The best way to talk with other developers on the project is through the
        <a href="http://lists.llvm.org/mailman/listinfo/cfe-dev">
            cfe-dev mailing list
        </a>
        . The clang mailing list is a very friendly place and we welcome newcomers.
        In addition to the cfe-dev list, a significant amount of design discussion
        takes place on the
        <a href="http://lists.llvm.org/mailman/listinfo/cfe-commits">
            cfe-commits mailing list
        </a>
        . All of these lists have archives, so you can browse through previous
        discussions or follow the list development on the web if you prefer.
    </p>
    <p>
        You can also follow the
        <a href="http://planet.clang.org/">
            Planet Clang
        </a>
        community news feed which offers a window into the world, work and lives
        of Clang developers, contributors and the standards they implement.
    </p>
    <p>
        If you're looking for something to work on, check out our
        <a href="http://clang.llvm.org/OpenProjects.html">
            Open Projects
        </a>
        page or look through the
        <a href="http://llvm.org/bugs/">
            Bugzilla bug database
        </a>
        .
    </p>
    <h2 id="criteria">
        Contributing Extensions to Clang
    </h2>
    <p>
        Clang has always been designed as a platform for experimentation, allowing
        programmers to easily extend the compiler to support great new language
        features and tools. At some point, the authors of these extensions may
        propose that the extensions become a part of Clang itself, to benefit the
        whole Clang community. But not every idea--not even every great idea--should
        become part of Clang. Extensions (particularly language extensions) pose
        a long-term maintenance burden on Clang, and therefore the benefits of
        the extension must outweight those costs. Hence, these are the seven criteria
        used to evaluate the merits of a proposed extension:
    </p>
    <ol>
        <li>
            Evidence of a significant user community: This is based on a number of
            factors, including an actual, existing user community, the perceived likelihood
            that users would adopt such a feature if it were available, and any "trickle-down"
            effects that come from, e.g., a library adopting the feature and providing
            benefits to its users.
        </li>
        <li>
            A specific need to reside within the Clang tree: There are some extensions
            that would be better expressed as a separate tool, and should remain as
            separate tools even if they end up being hosted as part of the LLVM umbrella
            project.
        </li>
        <li>
            A complete specification: The specification must be sufficient to understand
            the design of the feature as well as interpret the meaning of specific
            examples. The specification should be detailed enough that another compiler
            vendor could conceivably implement the feature.
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
            A long-term support plan: Contributing a non-trivial extension to Clang
            implies a commitment to supporting that extension, improving the implementation
            and specification as Clang evolves. The capacity of the contributor to
            make that commitment is as important as the commitment itself.
        </li>
        <li>
            A high-quality implementation: The implementation must fit well into Clang's
            architecture, follow LLVM's coding conventions, and meet Clang's quality
            standards, including high-quality diagnostics and rich AST representations.
            This is particularly important for language extensions, because users will
            learn how those extensions work through the behavior of the compiler.
        </li>
        <li>
            A proper test suite: Extensive testing is crucial to ensure that the language
            extension is not broken by ongoing maintenance in Clang. The test suite
            should be complete enough that another compiler vendor could conceivably
            validate their implementation of the feature against it.
        </li>
    </ol>
</div>