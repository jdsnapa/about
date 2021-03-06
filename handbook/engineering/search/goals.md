# Search goals and priorities

## Goals

Goals help us achieve our [vision](index.md#vision) for search.

### Scalable

- **Scale indexed search to 500k repositories**
   - **Problem:** We have customers who need Sourcegraph to scale to 500k repositories. Some parts of Sourcegraph don't work well at that scale.
   - **Outcome:** Sourcegraph can search 500k repositories in less than 300ms. This is on par with [grep.app](https://grep.app).
   - **Planned work:** [Scaling indexed text search to 500k repositories](#4-scaling-indexed-text-search-to-500k-repositories)

### Fast

- **Unblock improving user perceived performance**
  - **Problem:** Our current search infrastructure relies on on-shot requests with aggressive timeouts, but it is hard to tune those timeouts for large codebases. If we make the timeouts too small, then search may not return results for needle-in-the-haystack queries (because the search timed out). If we make the timeouts too large, then search becomes slower across the board and users spend time waiting for more results when we could have returned useful results to them sooner. Detecting and handling these timeouts across multiple service boundaries is also error prone and has led to bugs.
  - **Outcome:**
      - Unblock the ability to add responsive and fast-loading search results.
      - Return results faster for large result sets, e.g. indexed repositories in very large codebases.
  - **In progress work:** [Streaming search](#5-streaming-search)

### Expressive

- **Extend Search Query Language**
  - **Problem:** It is imperative that users can find and filter the code, files, repositories, and commits they care about in extremely large codebases.
  - **Outcomes:** Users can express relations on code, files, repositories, and commits in search queries to more effectively filter the data they need. Sourcegraph is the exclusive industrial-strength search solution that provides these capabilities.
  - **Planned work:** [Search language rules engine](#10-search-language-rules-engine)

### Easy to use

- **Improve search experience**
  - **Problem:**
      - New users who are trying Sourcegraph for the first time have trouble learning the syntax and breadth of Sourcegraph features.
          - **In progress work:** [Search tour](#2-search-tour)
      - It is hard for users to quickly get to code they care about.
          - **In progress work:** [Enterprise homepage](#1-enterprise-homepage)
  - **Outcomes:**
     - New users introduced to Sourcegraph are able to quickly run searches that show them the value of Sourcegraph.
     - Users can run searches over code they care about more quickly.
     - Sourcegraph surfaces code and searches users care about.

### Shareable

- **Code monitoring** ([RFC 227](https://docs.google.com/document/d/1_R5DgpUkxyZilsJ9vBQm5cvRPT2udc3tZIPg2q3cnZU/edit))
  - **Problem:** Users want to be notified about important things going on in their code.
  - **Outcome:** Notifications create a shared understanding and raise awareness of what’s going on in the code.
  - **Planned work:** [Code monitoring version 1](#6-code-monitoring-version-1)

---

## Roadmap

The search roadmap is driven by the team's [goals](#goals).


1. 🔄 [Enterprise homepage](#1-enterprise-homepage)
1. 🔄 [Search tour](#2-search-tour)
1. 🔄 [Search expressions](#3-search-expressions)
1. 🔄 [Scaling indexed text search to 500k repositories](#4-scaling-indexed-text-search-to-500k-repositories)
1. 🔄 [Streaming search](#5-streaming-search)
1. [Code monitoring (private code monitors, no sharing, emails + webhooks)](#6-code-monitoring-version-1)
1. [Performance at scale](#7-performance-at-scale)
follow-up to “scale indexed text search to 500k repositories”, focus and scope TBD
1. [Consolidate repogroups + search scopes](#8-consolidate-repogroups-search-scopes)
as a user, I can create a scope of code I want to search across as a list of repositories 
1. [Better version contexts 1/2](#9-better-version-contexts-12)
as a user, I can create a scope of code I want to search across as a list of repositories + branches
1. [Search language rules engine](#10-search-language-rules-engine)
1. [Saved searches without monitoring](#11-saved-searches-without-monitoring)
1. [Search results redesign](#12-search-results-redesign)
1. [Diff/commit search performance](#13-diffcommit-search-performance)
1. [Search input redesign](#14-search-input-redesign)
1. [Structural search performance](#15-structural-search-performance)
1. [Better version contexts 2/2](#16-better-version-contexts-22) 
as a user, I can create a scope of code I want to search across as a list of repositories + branches that should be indexed
1. [Code monitoring version 2](#17-code-monitoring-version-2)
1. [Semantic search: prototype validation](#18-semantic-search-prototype-validation)
1. [External search result providers](#19-external-search-result-providers)
1. [Semantic search: implementation](#20-semantic-search-implementation)

See [search roadmap prioritization](https://docs.google.com/document/d/1sUoaF8otA25NMapVcM5yHfP82kFie0NUd3_kL5Rg2Ns/edit) for more details on individual items.

---

## Roadmap details

### 1. Enterprise homepage

- **Owner:** Farhan, Juliana
- **Status:** Completed
- **Estimated completion**: 3.21

### 2. Search tour

- **Owner:** Farhan
- **Status:** Completed
- **Estimated completion**:
       - ~~3.20~~ 2020-09-22 update: not all bugs found during the initial round of user testing were fixed in 3.20
       - 3.21

### 3. Search expressions

- **Owner:** Rijnard
- **Status:** In progress

### 4. Scaling indexed text search to 500k repositories

- **Plan:** Incrementally add repositories to Sourcegraph.com until searches get slow or start breaking. Fix those things. Then continue adding repositories.
- **Owners:** Keegan/Stefan
- **Status:** [In progress](perf.md)
- **Estimated completion**: 3.23 (End of December 2020)

### 5. Streaming search

- **Plan:** Streaming search
- **Owners:** Keegan, Juliana
- **Status:** In progress
- **Estimated completion:**
  - ~~3.21~~ 2020-09-23 update: We revised this estimate after discussing needed work on the design & frontend side.
  - 3.22

### 6. Code monitoring version 1

- Code monitoring sends users notifications for new search results in channels outside of Sourcegraph.
- Improve email notification support and expand the types of notification channels available.
- **Plan**
  - Personal code monitors (no organization level monitors in v1)
  - Email and Webhooks Support
- **Owner:** Juliana, Stefan
- **Status:** Not started
- **Estimated start:** 2020-11-02
- **Estimated effort:** 4 weeks
  
### 7. Performance at scale

Follow-up to “scale indexed text search to 500k repositories”, focus and scope TBD

### 8. Consolidate repogroups + search scopes

As a user, I can create a scope of code I want to search across as a list of repositories

- Consolidate the overlapping features for this experience - repogroups and search scope pages.
- Scoping your search to multiple repositories is intuitive and easy ([issue](https://github.com/sourcegraph/sourcegraph/issues/10621))

### 9. Better version contexts 1/2

As a user, I can create a scope of code I want to search across as a list of repositories + branches

- Creating version context scopes manually is time consuming. Improve this user experience ([issue](https://github.com/sourcegraph/sourcegraph/issues/11569))
- ToDo: consolidate user requests for a better search experience with version contexts set

### 10. Search language rules engine

- **Owner:** Rijnard
- **Status:** In progress
- **Plan**
  - Implement a query language extension to express relations (i.e., rules) on code, files, repositories, and commits. This replaces awkward one-off filters like `repohasfile`, `repohascommitafter` that do not generalize.
  - Prototype semantic search functionality that combines text search and LSIF data
  - Implement quality-of-life features for search: syntax highlighting, multiline queries, improve structural search performance
- **Owner:** Rijnard/Stefan
- **Status:** Not started
- **Estimated start:** 3.21
- **Estimated effort:** 4 months
  
### 11. Saved searches without monitoring

- Save or bookmark a search query you want to run again.
- Save a "composable query" or a query that can added on to the existing search query entered (i.e., improve [search scopes](https://docs.sourcegraph.com/code_search/how-to/scopes)).
  
### 12. Search results redesign

- Search Tabs
- Search results with sidebar
- Design refresh
- and more. scope TBD
  
### 13. Diff/commit search performance

- Diff/commit search performance works beyond the 50 repository limit ([issue](https://github.com/sourcegraph/sourcegraph/issues/6826)).
- Support security use cases which require searching over code history, specifically commits and diffs.
  
### 14. Search input redesign

- Reduce business in the search bar
- Search Expressions are supported
- and more. scope TBD

### 15. Structural search performance

- Structural search is a good experience for larger-scale code bases and cloud users.
- Structural search supports security use cases that require returning exhaustive search results, i.e., every result from the entire set of code they care about.

### 16. Better version contexts 2/2

As a user, I can create a scope of code I want to search across as a list of repositories + branches that should be indexed

- Improve the speed for unindexed code (e.g. diffs, commits) in the version context scopes they want to search over.

### 17. Code monitoring version 2

- Code monitoring sends users notifications for new search results in channels outside of Sourcegraph.
- Plan below should be updated based on learnings from user testing code monitoring version 1.
- **Plan**
  - Organization level code monitors

### 18. Semantic search: prototype validation

- Referencing precise code intelligence (e.g. usages, definition) in search
- **Plan**
  - Build a prototype to validate the idea
  
### 19. External search result providers

- Ability to search over data from issue trackers, internal tools, etc.
- The first set of providers is likely Sourcegraph [extensions](https://sourcegraph.com/extensions)
  
### 20. Semantic search: implementation

- Referencing precise code intelligence (e.g. usages, definition) in search
