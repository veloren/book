# Getting Started

Veloren is written in the Rust programming language and is maintained using Git, the industry standard version control system.

## Why Rust?

Rust is a new programming language designed to be fast, safe, and well-suited to concurrent programming. We believe that these attributes make it ideal for game design. As a result, the Veloren engine is extremely quick, very rugged (you'll be hard-pressed to find unintentional crashes or bugs in the codebase), and also multi-threaded (meaning it can take advantage of multi-core CPU architectures).

## Why Git?

Git is an industry standard version control system. It is uses to keep track of different versions of a codebase, and maintains a history of a codebase that can be viewed throughout time. It also makes contributing to the project much easier, since it helps to manage the merging and updating of the codebases maintained by each contributor.

# GitLab and our workflow

The repository is located in [GitLab](https://gitlab.com/veloren/veloren.git).
We use GitLab to manage the source code, assets, our website and this book.
We make heavy usage of the continuous integration of GitLab, we run tests and do code reviews.
Use the issue tracker of GitLab with the corresponding tags to track feature requests as well as bugs.

If you want to contribute source code, meet us at our [Discord](https://discord.gg/BvQuGze) and discuss what needs to be done.
Or just prepare a MR the way you like merge.
The default way of doing so is fork the project, create a branch in your fork, make changes, and then create a Merge Request in `veloren/veloren` to include your changes.
The MR should go to `master` branch.
Best strategy is to create a issue first and then link the MR to the issue so that reviewers know why this change is needed.
Stay active in discord as well as GitLab to answer questions over the next days.

If you contribute constantly you will get a developer role in both discord and GitLab, granting you some trust and the ability change more on your own.

For code snippets and see [Git workflow](../dev/workflow.md)
