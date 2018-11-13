# IMS GitHub Guidelines

IMS GitHub usage is centered around the concepts of
[Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow).
If you are familiar with Git Flow, few if any concepts here will be new to you.

Note however that these guidelines focus on how we use GitHub to develop both
_specification documents_ and reference implementations.  Due to certain
specifics of the specification document lifecycle, there are some deviations
from a plain vanilla Git Flow process.

* [Roles](#roles)
* [Branching](#branching)
* [Forking](#forking)
* [Pull Requests](#pullrequests)
* [Issue Tracking](#tracker)
* [Root files](#root)
* [Repository naming](#repo-naming)
* [Tag naming](#tag-naming)
* [Branch naming](#branch-naming)
* [Examples](#examples)
* [FAQ](#faq)

<a id="roles"></a>
## Roles
_Contributor_: an [IMSGlobal](https://github.com/IMSGlobal) organization
[team](https://help.github.com/articles/organizing-members-into-teams/) member
granted read access to one or more IMS repositories. Contributors typically
author changes in their personal forked copies of [IMSGlobal](https://github.com/IMSGlobal)
repositories. They then open a pull request against the upstream IMS repository,
which signals to designated committers that a change request has been initiated.

_Committer_: an [IMSGlobal](https://github.com/IMSGlobal) organization team
member granted write access to an IMS repository in
order to review and apply changes in the form of pull requests.

<a id="contributor"></a>
### Becoming a contributor
Contributors are typically individuals affiliated with an IMS contributing
member organization. Each contributor must sign an IMS
[individual contributor agreement](https://www.imsglobal.org/SOMEPATH) before
their pull requests can be reviewed and accepted.

<a id="committer"></a>
### Becoming a committer
Each IMS working group has a smaller set of designated committers. IMS staff
and the working group chairs jointly share responsibility for populating the
committer team.

A contributor interested in serving as a project committer must demonstrate
the following abilities:

* knowledge of the relevant specification and other supporting documentation
and reference implementation code
* familiarity with working group policies and practices, and code and document
styles
* knowledge of Git and Github
* ability to collaborate with other working group members
* willingness to participate actively in pull request reviews and merging
* coding and/or document writing proficiency as evidenced by 10+ pull requests
accepted and merged to one or more working group managed [IMSGlobal]
(https://github.com/IMSGlobal) repositories

<a id="branching"></a>
## Branching
The use of branches follows the general approach of Git Flow: the `master` branch
contains the official release history while the `develop` branch with associated
feature branches contains drafts of the "next" version of the specification
or reference implementation under development.

### The master branch
The `master` branch contains only specification document(s) that have been released
as IMS Final, or a reference implementation that has been tagged and made
available to the public.

Specification documents are stored in
[one of the available document formats](README.md#tools), and represent an exact
copy of the documents published on [imsglobal.org](https://www.imsglobal.org/),
albeit in a pre-rendered state. (What "pre-rendered" means varies depending on
which document format you are using.)

Reference implementation repositories contain code and other assets released
to the public for prototyping and other experimental purposes.

Each release on the `master` branch is tagged using the conventions laid out in
[Tag naming](#tag-naming) below. (Note also the maintenance of the [errata](#errata)
on the master branch.)

_Note - as opposed to Git Flow, we do not utilize dedicated release branches._

### The develop branch and feature branches
The `develop` branch serves as an integration branch for new development. In
the case of specification or document-oriented repositories `develop` contains
document(s) in a pre-Final state (i.e. documents that are to be or have been
published as Base Document or Candidate Final). For reference implementation
repositories `develop` contains new or refactored code targeting the next
release.  Each release on the `develop` branch is tagged using the conventions
laid out in [Tag naming](#tag-naming) below.

Just like in Git Flow, work on a new version of a specification or a
reference implementation targets the `develop` branch. Each new feature (or
substantive change) should be developed on a dedicated feature branch off the
`develop` branch.  Merging of features into develop is done as the working group
accepts the feature for inclusion, and/or (in the case of document repositories)
as a new Base Document or Candidate Final release is being prepared.

Some contributions to the `develop` branch do not qualify as features, e.g. a
set of typo corrections, or the initial commit of a document stub. In these
cases, the pull request does not need to come off a dedicated feature
branch, but can be issued directly against `develop`.

Note that developers maintaining local feature branches are responsible for
refreshing their work regularly with changes that have been merged to the
upstream IMSGlobal `develop` branch.  The goal is to avoid stale
branches, clean pull requests free of merge conflicts, and happy committers.

### Hotfix branches
Each [specification Document Set](document-set.md) has a shared errata that is
used to document erratum registered for normative members (see
[Versioning and Errata](versioning-errata.md) for more information).

If document errors are discovered in a published specification a "hotfix" branch
must be created off of `master`.  Once the errata update is ready (remember: the
errata is documenting non-substantive in-place edits to normative documents),
merge the `hotfix` branch to `master` and then, if relevant, to `develop` as
well. `master` must then be tagged per the [Tag naming](#tag-naming)
conventions described below.

Likewise, if a "bug" is discovered in a tagged reference implementation, patching
is also performed using a "hotfix" branch created off of `master`.  Once the fix
is ready, it should be merged from the `hotfix` branch to `master` and then, if
relevant, to `develop` as well. `master` must then be tagged per
[Tag naming](#tag-naming) conventions described below.

The following graph shows a specification development branching workflow that
primarily utilizes feature branches for development against the master and develop branches.
Tags (the white boxes) are used to denote Base, Candidate and Final releases.
Hotfix branches are used for errata (on master) and hotfixes (on develop).

![Graph of specification development branching workflow based on feature branches](images/branching1.svg)

The following graph shows a simplified specification development workflow in terms of
branching, where feature branches are not in use. Tags (the white boxes) are still used as required
to denote releases.

![Graph of specification development branching workflow without feature branches](images/branching2.svg)



<a id="forking"></a>
## Forking
Contributors typically conduct their work by _forking_ the
[IMSGlobal](https://github.com/IMSGlobal) repository, creating a copy attached
to their personal Github account. (Note: in standard workflows we do not _clone_ a repository directly.)

As described in more detail below, once a project is cloned, new branches must
be created to encapsulate work on a new feature or bug fix.  New files can then
be added, existing files edited, changes committed, and updates pulled or pushed.
As described below, changes pushed to a contributor's personal account can then
be submitted to IMS via a pull request (PR).

<a id="pullrequests"></a>
## Pull Requests
All document and/or code contributions targeting project branches are
submitted using pull requests.  Each pull request will be reviewed by one or
more designated [committers](#committer). Approving, requesting changes, or
rejecting a contributor's pull request is at the discretion of the reviewing
committer(s). If a committer submits a pull request it must be reviewed by another
committer except in cases where the committer is the lone maintainer of a
repository.  Again, unless explicitly exempted, merging one's own pull
request is not permitted.

<a id="tracker"></a>
## Issue Tracking
The repository issue tracker is seen as the single source of truth for any and all
open issues or action items pertaining to the specification or reference
implementation being developed. If it's not in the tracker, the issue doesn't
exist.

IMS staff, working group chairs, and committers are collectively responsible
for maintaining the tracker in a healthy state, including ensuring that issues
are opened for all ongoing work streams, and closed as the work is completed.

It is recommended that issues are tagged using multi-dimensional labels so that
they can be sorted properly. An initial set of labels (that working groups may
elect to extend) is:

* Type dimension: `bug`, `feature request`, `question`
* Status dimension: `accepted`, `duplicate`, `wontfix`, `deferred`
* Problem area dimension: `api`, `schema`, `cert`, `spec`

Milestones _must_ also be used to denote for which release a resolution is
targeted, unless the issue has been labelled as deferred.

Any active branch off `develop` must have an issue associated with it. That is,
before starting work on a pull request in a feature branch, contributors must
open an issue and discuss the proposal with the working group, documenting
the discussion in the issue.

If working groups use add-on project management features (e.g. ZenHub, Waffle.io
or Git Projects), then that will naturally have an impact on the use of labels.
The use of any project management features should be noted in the README file in
the project [root](#root to help orient new users.

Issues that need extended discussion and input from individuals or groups that
do not participate in the day-to-day activities of the working group should be
cross-posted to the IMS Forums.

<a id="root"></a>
## Root Files
All branches of each repository must contain a set of "root files". These are:

__README.md__: contains an introduction to the purpose of the repository,
including links to contact persons (staff, chairs), copyright information and
any additional information needed to consume the contents of the repository
correctly.The file also contains participant information while the specification is
under development. This file also links to LICENSE.md, and if relevant, NOTICE.md.

__LICENSE.md__: contains copy of the license applied to the project. The specification
license is required for final specifications.

_INPROGRESS-SPECLICENSE.md_: contains copy of license and participation details of
specifications under development.

__.editorconfig__: contains editor configurations for various editors. Read more
in [editor-config](editor-config.md)

The following root files are optional:

__CONTRIBUTING.md__: describes contributor instructions.

__NOTICE.md__: Contains additional licensing information where necessary, for
example to clarify a dual licensing scenario.

_Template root files are provided in the [rootfiles](./rootfiles/) directory
of this repository. An .editorconfig file is available in the root of this
repository._

<a id="repo-naming"></a>
## Repository naming
IMS uses a naming convention for repositories to facilitate easy location. By
default, the convention uses two segments; additional segments can be
appended if needed.

The first segment is the specification [shortName](urls-names.md#shortnames),
followed by a type designator, where the type is typically the document or
application type.

Examples:

`cc-spec`

`caliper-implguide`

`oneroster-certguide`

`clr-ontology`

Some working groups will have a large set of repositories, and may want to have
a repository dedicated to coordinate activities across these repositories. In such
cases the recommended type designator is "central", e.g:

`caliper-central`

<a id="tag-naming"></a>
## Tag naming

The way we name tags differ between document repositories and code repositories.

### For document repositories
#### Tags on master

`2.0-final`: denotes the release of version 2.0 in Final state

`2.0-errata.01`: denotes the first errata release for version 2.0

`2.0-errata.02`: denotes the second errata release for version 2.0

`2.1-final`: denotes the release of version 2.1 in Final state

#### Tags on develop
`2.0-base.01`: denotes the first release of version 2.0 in Base Document state

`2.0-candidate.01`: denotes the first release of version 2.0 in Candidate Final state

`2.0-candidate.02`: denotes the second release of version 2.0 in Candidate Final state

_(Note: the third `.nn` segment is included in tag names whenever the same type
  of release may occur multiple times for a given version of a document)_

### For code repositories

Code repositories typically utilize semver.org-based names for tags.



<a id="branch-naming"></a>
## Branch naming
The `master` and `develop` branches are statically named and used as defined
above in all projects. Feature branches off develop follow the convention of a
`feature` or `hotfix` prefix, followed by an issue reference. (Note that this
means that before starting to work on a feature proposal, you must populate the
tracker with an issue.)

Examples:

`hotfix/123`

`feature/456`

<a id="examples"></a>
## Examples

### Starting a new project
TBD
### Releasing a Base document
TBD
### Releasing a Candidate Final document
TBD
### Releasing a Final document
TBD
### Issuing an Errata
TBD
### Starting work on a new revision

<a id="faq"></a>
## FAQ

__Do we have to use Git from day one of our spec development project?__

For the earlier stages of the specification development process, working groups
are free to use any authoring platform that best suit their style of collaboration.
For example, it is viable to initially use e.g. online word processing services
such as Google Docs if this is preferred. But no later than at the time of publication
of the first Base Document, the work needs to be re-located to the Git repository,
and transformed to use [one of the available document formats](README.md#tools).

In any event, the Issue Tracker of the project should be used from day one.

__Can we use MarkDown to author and store the specification text in the repo?__

For the initial stages of the specification development, this is an option. Note
however that as you approach publication of the first Base Document, you will need
to convert the content into [one of the available document formats](README.md#tools).

(If you are using the Respec tool, there is
[a way to transclude MarkDown](respec-usage.md#transclusion) into the
Respec HTML document, which provides a way to support prolonged use of MarkDown
for certain document fragments if this is desired. IMS however does recommend to
use native HTML5 in Respec as it allows for richer markup that natively supports
the [structure guidelines](structure-guidelines.md). See also [markdown-notes](markdown-notes.md)
for known issues with Markdown+Respec use.)

__Do we put the main spec, implementation guide and cert guide in the same repo or different repos?__

Informative members of the [document set](document-set.md) (e.g. the
implementation guide) are typically maintained in separate individual repos, as
they can be re-released without the main specification being re-released. Sharing
a repo between normative and informative documents would make version handling
overly complex and confusing.

Normative members of the document set (e.g. main spec, cert guide, schemas) may be
maintained in the same repo, as their release cycles are synchronized. Working groups
that elect to use different repos for normative members should provide an interweb
of links in each repo README.md file to associate the repos with each other.

__When we are about to create a new version of a spec, do we create a new repo for it?__

No. Specification versions are denoted using tags on the master branch. The new
version of the spec is developed in the `develop` branch of the same repo, and
eventually (once Final) merged into `master` with a new [tag](#tag-naming).