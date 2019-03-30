---
layout: post
title: "Annotations to Pro Git, 2nd Edition"
categories: Annotations
tags: git
---

Here are some annotations to [*Pro Git*, 2nd Edition](https://git-scm.com/book/en/v2) written by Scott Chacon and Ben Straub.

{% include toc.html %}

## 1. Getting Started

### 1.1 About Version Control

What is *version control*?

> Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later.

- **Local Version Control Systems**. VCSs have a simple database that kept all the changes to files under revision control. For example, [Revision Control System(RCS)](https://en.wikipedia.org/wiki/Revision_Control_System).
- **Centralized Version Control Systems**. CVCSs have a single server contains all the versioned files, and a number of clients that check out files from that central place. For example, [CVS](https://en.wikipedia.org/wiki/Concurrent_Versions_System), [Subversion](https://subversion.apache.org/), and [Perforce](https://www.perforce.com/). **Downside**: If the server goes down, the whole system doesn't work.
- **Distributed Version Control Systems**. In a DVCs, clients fully mirror the repository, including its full history.