# 拉取请求 {#pull-requests}

您可以通过提交[拉取请求][pull request]来为 MkDocs 的 Material 做出贡献，维护者将审查这些请求，并在更改被批准后将其整合到主仓库中。您可以贡献错误修复、文档更改或您开发的新功能。

[pull request]: https://docs.github.com/en/pull-requests

!!! note "考虑一个拉取请求"

    在决定投入精力进行更改并创建拉取请求之前，请讨论您打算做什么。如果您认为可能遇到了一个错误，请首先提交一个[错误报告][bug report]。如果您打算处理文档，创建一个[文档问题][documentation issue]。如果您想开发新功能，请创建一个[变更请求][change request]。

    请注意给出的指导并让人们为您提供建议。可能有更简单的解决方案可以解决您所认为的问题。也可能您想要实现的功能通过配置或[自定义][customization]已经可以完成。

[bug report]: reporting-a-bug.md
[documentation issue]: reporting-a-docs-issue.md
[change request]: requesting-a-change.md
[customization]: ../customization.md

## 关于拉取请求的学习 {#learning-about-pull-requests}

拉取请求是基于 Git 的概念，由提供 Git 托管服务的服务层提供。在您考虑发起拉取请求之前，您应该熟悉 GitHub 的文档，我们正在使用这个服务。以下文章尤为重要：

1. [Forking a repository]
2. [Creating a pull request from a fork]
3. [Creating a pull request]

请注意，他们为不同的操作系统和与 GitHub 交互的不同方式提供了定制化的文档。我们在这里的文档中尽力描述了这一过程如何适用于 MkDocs 的 Material，但不能覆盖所有可能的工具组合和做事方式。在继续之前了解拉取请求的一般概念也很重要。

[Forking a repository]: https://docs.github.com/en/get-started/quickstart/fork-a-repo
[Creating a pull request from a fork]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork
[Creating a pull request]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

## 拉取请求流程 {#pull-request-process}

以下描述了发起拉取请求的一般流程。这里的目标是提供一个高层次的概览，然后再详细描述。

### 准备更改和草稿PR {#preparing-changes-and-draft-pr}

下面的图表描述了在准备拉取请求过程中通常会发生的事情。我们将讨论下面的审查修改过程。在担心具体命令之前，首先了解整个流程是很重要的。这就是为什么我们首先介绍这个，然后再提供下面的指令。

``` mermaid
sequenceDiagram
  autonumber

  participant mkdocs-material
  participant PR
  participant fork
  participant local

  mkdocs-material ->> fork: fork on GitHub
  fork ->> local: clone to local
  local ->> local: branch
  loop prepare
    loop push
      loop edit
        local ->> local: commit
      end
      local ->> fork: push
    end
    mkdocs-material ->> fork: merge in any changes
    fork ->>+ PR: create draft PR
    PR ->> PR: review your changes
  end
```

1. 第一步是创建 Material for MkDocs 仓库的一个分支，你可以选择 [mkdocs-material] 或 [mkdocs-material-insiders] （仅对赞助者开放）。这样你就拥有了一个可以提交更改的仓库。注意，任何时候你都无法拥有一个给定仓库的多个分支。因此，你创建的分支将是 *你拥有的* 分支。

2. 分支创建后，将其克隆到你的本地机器上，开始你的修改工作。

3. 所有贡献都应通过一个名为“主题分支”的分支进行，分支名应描述正在进行的工作。这使你能够同时进行多个工作，并且，如果你使用的是公共版本，还能清晰地向他人展示代码处于进行中状态。主题分支的生命周期相对较短，在最终将你的更改并入代码库时会消失。

4. 接下来是反复编辑、提交到你的克隆库的过程。请分段提交，每次提交应代表一项完整的工作，而不是一次性提交所有更改。

    请记住，细粒度的增量提交比大范围的大修改更容易审核。尽量保持你的更改尽可能小和局部，提交时要考虑审阅者。特别是要确保写下有意义的提交信息。

5. 定期将你的工作推送到你的分支。

6. 你还应该关注你克隆的 Material for MkDocs 仓库中的变化。如果你的工作花费了一些时间，这一点尤其重要。请尝试定期将任何同时发生的更改合并到你的分支和分支中。在创建拉取请求之前，你*必须*至少做一次合并，因此请更频繁地这样做，以尽量减少冲突更改的风险。

7. 一旦你对你的更改感到满意，认为它们已经可以在*草稿*拉取请求中描述了，你应该创建它。确保引用任何之前的讨论或问题，这些讨论或问题引发了你的工作。创建草稿是从维护者或其他人那里获得*早期*反馈的好方法。你可以在认为这很重要的时候明确要求审查。

8. 如同你是审查者一样审查你的工作，修复到目前为止你的工作中的任何问题。仔细查看你所改变的文件的差异。特别注意更改是否尽可能小，以及你是否遵循了项目中使用的一般编码风格。如果你收到了反馈，根据需要重复到目前为止的过程。

    你应该选择一些项目来测试你的更改。你应该确保更改不会破坏 Material for MkDocs 的文档构建，你可以在 `docs` 文件夹中找到它。你可能还想确保[示例仓库]中的相关示例仍然可以正常构建。

[mkdocs-material]: https://github.com/squidfunk/mkdocs-material
[mkdocs-material-insiders]: https://github.com/squidfunk/mkdocs-material-insiders/
[examples repository]: https://github.com/mkdocs-material/examples

### 完成 {#finalizing}

一旦你对更改感到满意，你可以转到下一步，完成你的拉取请求，并要求进行更正式和详细的审查。下面的图表显示了过程：

``` mermaid
sequenceDiagram
  autonumber
  participant mkdocs-material
  participant PR
  participant fork
  participant local

  activate PR
  PR ->> PR : finalize PR
  loop review
    loop discuss
      PR ->> PR: request review
      PR ->> PR: discussion
      local ->> fork: push further changes
    end
    PR ->> mkdocs-material: merge (and squash)
    deactivate PR
    fork ->> fork: delete branch
    mkdocs-material ->> fork: pull
    local ->> local: delete branch
    fork ->> local: pull
  end
```

1. 当你对所做的更改满意，并认为维护者可以将其整合到代码库时，完成拉取请求。这向所有人表明你认为工作已经‘完成’，并且可以进行审查以便接受和整合。

2. 向维护者 `@squidfunk` 请求审查。

3. 维护者可能会对你的代码发表评论，你应该与他们讨论。在此过程中，请记住维护者可能与你的观点不同。他们通常会从长远维护项目的角度考虑，而你可能更专注于你所工作的特定问题或功能。请始终保持讨论的尊重。

    重要的是要注意，并非所有拉取请求都会并入代码库。原因可能各不相同。工作可能揭示了阻碍拉取请求整合的其他问题。有时候，它有助于发现更好的做事方法，或者显示需要更通用的方法。所有这些都有助于项目的进展，即使特定的更改最终可能不被接受也是如此。

4. 根据请求，将任何要求的更改提交到你的本地克隆，并将它们推送到你的分支。这将自动更新拉取请求。这可能需要几次迭代才能将你的贡献达到可接受的状态。通过仔细阅读评论并小心地进行更改，你可以帮助这一过程。

5. 一旦审查者对更改完全满意，他们可以将其合并到主分支（或‘master’）。在此过程中，他们可能会将你的提交合并成较少的提交，并可能编辑描述它们的消息。恭喜，你现在已经为这个项目做出了贡献，并且应该在主分支下看到你的名字。

6. 现在你可以删除分支和你的本地仓库，并在下次再次开始时从头开始。或者，你可以保留仓库和本地克隆，但重要的是，你需要将它们与上游仓库同步，以便进行任何后续工作。我们建议你首先删除你在分支上使用的分支。

7. 为确保你拥有你生成的更改，请从主仓库将更改拉取到你的分支的主分支。

8. 同样，从你的本地克隆中删除主题分支并...

9. 拉取更改到其主分支。

## 步骤 {#steps}

现在整个过程已经概述，以下是具体的指导和提示。在描述通过拉取请求为项目做出贡献的过程时，有许多选择需要做出。在接下来的内容中，我们假设你正在使用 Git 命令行工具。对于大多数其他选择（如使用 IDE 或通过 GitHub 网页界面提供的功能），将命令行指令转换应该足够简单。我们将仅在真正必要时添加注释，以保持这一点的复杂性处于合理水平。

### 分支仓库 {#forking-the-repository}

要对 Material for MkDocs 进行更改，你首先需要在 GitHub 上分支其仓库之一。这样你就有了一个可以推送更改的 GitHub 仓库（只有维护者和合作者才有权限访问原始仓库）。

如果你想对公共版本的代码或文档进行更改，请分支[公共版本的仓库][repository for the public version]。更改仓库名称，通过添加 `-fork` 来让发现它的人知道他们找到的是项目的临时分支而不是原始或永久分支是一个好主意。你也可能想添加一个说明仓库用途的描述。

[repository for the public version]: https://github.com/squidfunk/mkdocs-material

要对只在内部版本中可用的功能进行更改，请分支[内部版本仓库][the Insiders repository]。请注意，分支将是一个私有仓库。请遵守[内部计划条款][terms of the Insiders program]和用于维护和开发 Material for MkDocs 的 Sponsorware 方法的精神。

[the Insiders repository]: https://github.com/squidfunk/mkdocs-material-insiders/
[terms of the Insiders program]: http://localhost:8000/mkdocs-material/insiders/faq/sponsoring/#licensing

### 设置开发环境 {#setting-up-a-development-environment}

从这一点开始，请遵循[设置开发环境的指导][instructions for setting up the development environment]。这些指导将带你完成设置一个可以进行更改和审查/测试的环境的过程。

[instructions for setting up the development environment]: ../customization.md#environment-setup

### 进行更改 {#making-changes}

当你对代码或文档进行更改时，请遵循项目中使用的既定风格。这样做可以提高可读性，并帮助审查拉取请求的人更容易阅读差异。避免进行任何大规模的风格更改，如让你的 IDE 重新格式化所有代码。

请仔细研究你正在修改的代码，以确保在尝试更改之前你已完全理解其工作原理。这不仅可以帮助你解决你试图解决的问题，还可以最小化创建意外副作用的风险。

### 提交到分支

拉取请求的开发最好在与 `master` 分支分开的主题分支上进行。使用 `git switch -c <name>` 创建一个新的本地分支，并将你的更改提交到这个分支。

当你想将提交推送到你的分支时，你可以使用 `git push -u origin <name>`。`-u` 参数是 `--set-upstream` 的简写，这使得新创建的分支 '跟踪' 你分支中同名的分支。这意味着之后的 `pull` 和 `push` 命令将默认针对你分支中的那个分支。

### 合并同时发生的更改 {#merging-concurrent-changes}

如果你的工作需要一些时间，那么主仓库在你工作期间进行更改的可能性就会增加。将原始的 Material for MkDocs 仓库设置为你本地克隆的 `upstream` 仓库可能是个好主意。

这可能是这样的：

```bash hl_lines="4"
$ git remote -v
origin	git@github.com:<your_username>/mkdocs-material-fork.git (fetch)
origin	git@github.com:<your_username>/mkdocs-material-fork.git (push)
$ git remote add upstream https://github.com/squidfunk/mkdocs-material.git
$ git remote -v
origin	git@github.com:alexvoss/mkdocs-material-fork.git (fetch)
origin	git@github.com:alexvoss/mkdocs-material-fork.git (push)
upstream	https://github.com/squidfunk/mkdocs-material.git (fetch)
upstream	https://github.com/squidfunk/mkdocs-material.git (push)
```

完成此操作后，你可以直接从上游仓库将任何同时发生的更改拉取到你的克隆中，并在那里进行必要的合并，然后将它们推送到你的分支。当你执行 `pull` 时，你需要明确指定你想要使用的远程仓库：

```bash
# making and committing some local changes
push pull upstream master
```

这会将更改从 `master` 分支拉取到你的主题分支并合并它们。

### 测试和审查更改 {#testing-and-reviewing-changes}

在你提交任何更改之前，你应该确保它们按预期工作，并且不会创建任何意外的副作用。你应该至少在这三个[烟雾测试][smoke tests]上测试它们：

- Material for MkDocs 本身的文档。如果你按照[设置开发环境的指导][instructions for setting up the development environment]建立并运行开发环境，`mkdocs serve` 应该正在运行并连续构建文档。检查是否没有错误消息，并且理想情况下没有（新的）警告。

- 在代表问题的项目上测试，或为新开发的功能测试。如果你已经提交了错误报告并创建了一个[最小再现][minimal reproduction]，你可能已经拥有了这个。如果你正在开发一个新功能，你可能需要构建一个项目作为测试套件。它还可以作为文档，展示你的新功能应该如何工作。

- 使用[Material for MkDocs 示例][Material for MkDocs Examples]仓库中的相关示例进行测试。请注意，要一次构建所有示例，你需要 Insiders 的项目插件，但你总是可以使用公共版本单独构建示例。

[smoke tests]: https://en.wikipedia.org/wiki/Smoke_testing_(software)
[minimal reproduction]: https://squidfunk.github.io/mkdocs-material/guides/creating-a-reproduction/
[Material for MkDocs Examples]: https://github.com/mkdocs-material/examples

- 理想情况下，还应在[示例仓库][examples repository]中测试示例。如果你正在使用 Material for MkDocs 的 Insiders 版本，你可以简单地在顶层开始构建，[项目插件][projects plugin]将为你构建所有示例。如果你在公共版本中，你需要单独构建每个子项目。我们理解这是一个不断增长的示例集合，你可能想优先考虑那些与你更改的功能最相关的示例。

[examples repository]: https://github.com/mkdocs-material/examples
[projects plugin]: https://squidfunk.github.io/mkdocs-material/plugins/projects/

### 创建拉取请求 {#creating-the-pull-request}

最初，**作为草稿**创建拉取请求。你可以[通过 GitHub 提供的各种界面][through the various interfaces that GitHub provides]来完成这一点。你使用哪一个完全取决于你。我们不提供使用界面的具体指导，因为 GitHub 提供的信息应该足够。

[through the various interfaces that GitHub provides]: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

### 提交、信息、错误和 '压缩' {#commits-messages-mistakes-and-squash}

### 删除分支 {#deleting-branches}

一旦拉取请求合并到 Material for MkDocs 仓库的主分支，你应该从 GitHub 上的分支和你的本地克隆中删除分支。这避免了可能对开发状态的混淆。

首先，使用 `git switch master` 切换回 `master` 分支，然后使用 `git branch -d <name>` 删除用于 PR 的分支。

### 后续拉取请求 {#subsequent-pull-requests}

重要的是，后续拉取请求应从 `master` 分支的最新历史开始。一种实现这一点的方法是删除分支，并在下一次开始时使用全新的分支。

如果你经常为 Material for MkDocs 做出贡献，或者只是恰好连续进行两个或更多的拉取请求，你也可以确保同步你的分支（使用 GitHub UI），并从中拉取到你的本地仓库。因此，只需删除你创建的主题分支（本地和在你的分支中都要删除），然后在开始新的拉取请求之前，从主仓库的 `master` 分支拉取到你的 `master` 分支。

### 注意事项 {#dos-and-donts}

1. **不要** 仅创建未说明更改的拉取请求。

2. **要** 在讨论中讨论你打算做什么，以便在你编写或修改代码之前清楚任何更改的理由。

3. **要** 链接到讨论或任何问题以提供拉取请求的上下文。

4. **要** 如果你对任何事情感到不确定，就提问。

5. **要** 问自己你所做的是否有益于更广泛的社区，并使 Material for MkDocs 成为更好的产品。

6. **要** 问自己，进行更改的成本是否与它们带来的好处成正比。一些其他明智的更改可能会增加复杂性，相对于它们带来的收益较小，可能会破坏现有行为，或在需要进行其他更改时可能会变得脆弱。

7. **要** 频繁合并同时发生的更改，以最小化可能难以解决的冲突更改的机会。
