---
eip: 1
title: PIP Purpose and Guidelines
status: Active
type: Meta
author: Martin Becze <mb@ethereum.org>, Hudson Jameson <hudson@ethereum.org>, and others
        https://github.com/ethereum/PIPs/blob/master/PIPS/eip-1.md
created: 2015-10-27
updated: 2015-12-07, 2016-02-01, 2018-03-21, 2018-05-29, 2018-10-17, 2019-05-19, 2019-12-04
---

## What is an PIP?

PIP stands for Pie Improvement Proposal. An PIP is a design document providing information to the Ethereum community, or describing a new feature for Ethereum or its processes or environment. The PIP should provide a concise technical specification of the feature and a rationale for the feature. The PIP author is responsible for building consensus within the community and documenting dissenting opinions.

## PIP Rationale

We intend PIPs to be the primary mechanisms for proposing new features, for collecting community technical input on an issue, and for documenting the design decisions that have gone into Ethereum. Because the PIPs are maintained as text files in a versioned repository, their revision history is the historical record of the feature proposal.

For Ethereum implementers, PIPs are a convenient way to track the progress of their implementation. Ideally each implementation maintainer would list the PIPs that they have implemented. This will give end users a convenient way to know the current status of a given implementation or library.

## PIP Types

There are three types of PIP:

- A **Standard Track PIP** describes any change that affects most or all Ethereum implementations, such as a change to the network protocol, a change in block or transaction validity rules, proposed application standards/conventions, or any change or addition that affects the interoperability of applications using Ethereum. Furthermore Standard PIPs can be broken down into the following categories. Standards Track PIPs consist of three parts, a design document, implementation, and finally if warranted an update to the [formal specification].
  - **Core** - improvements requiring a consensus fork (e.g. [PIP5], [PIP101]), as well as changes that are not necessarily consensus critical but may be relevant to [“core dev” discussions](https://github.com/ethereum/pm) (for example, [PIP90], and the miner/node strategy changes 2, 3, and 4 of [PIP86]).
  - **Networking** - includes improvements around [devp2p] ([PIP8]) and [Light Ethereum Subprotocol], as well as proposed improvements to network protocol specifications of [whisper] and [swarm].
  - **Interface** - includes improvements around client [API/RPC] specifications and standards, and also certain language-level standards like method names ([PIP6]) and [contract ABIs]. The label “interface” aligns with the [interfaces repo] and discussion should primarily occur in that repository before an PIP is submitted to the PIPs repository.
  - **ERC** - application-level standards and conventions, including contract standards such as token standards ([ERC20]), name registries ([ERC26], [ERC137]), URI schemes ([ERC67]), library/package formats ([PIP82]), and wallet formats ([PIP75], [PIP85]).
- A **Meta PIP** describes a process surrounding Ethereum or proposes a change to (or an event in) a process. Process PIPs are like Standards Track PIPs but apply to areas other than the Ethereum protocol itself. They may propose an implementation, but not to Ethereum's codebase; they often require community consensus; unlike Informational PIPs, they are more than recommendations, and users are typically not free to ignore them. Examples include procedures, guidelines, changes to the decision-making process, and changes to the tools or environment used in Ethereum development. Any meta-PIP is also considered a Process PIP.
- An **Informational PIP** describes an Ethereum design issue, or provides general guidelines or information to the Ethereum community, but does not propose a new feature. Informational PIPs do not necessarily represent Ethereum community consensus or a recommendation, so users and implementers are free to ignore Informational PIPs or follow their advice.

It is highly recommended that a single PIP contain a single key proposal or new idea. The more focused the PIP, the more successful it tends to be. A change to one client doesn't require an PIP; a change that affects multiple clients, or defines a standard for multiple apps to use, does.

An PIP must meet certain minimum criteria. It must be a clear and complete description of the proposed enhancement. The enhancement must represent a net improvement. The proposed implementation, if applicable, must be solid and must not complicate the protocol unduly.

### Special requirements for Core PIPs

If a **Core** PIP mentions or proposes changes to the EVM (Ethereum Virtual Machine), it should refer to the instructions by their mnemonics and define the opcodes of those mnemonics at least once. A preferred way is the following:
```
REVERT (0xfe)
```

## PIP Work Flow

### Shepherding an PIP

Parties involved in the process are you, the champion or *PIP author*, the [*PIP editors*](#eip-editors), and the [*Ethereum Core Developers*](https://github.com/ethereum/pm).

Before you begin writing a formal PIP, you should vet your idea. Ask the Ethereum community first if an idea is original to avoid wasting time on something that will be be rejected based on prior research. It is thus recommended to open a discussion thread on [the Ethereum Magicians forum] to do this, but you can also use [one of the Ethereum Gitter chat rooms], [the Ethereum subreddit] or [the Issues section of this repository]. 

In addition to making sure your idea is original, it will be your role as the author to make your idea clear to reviewers and interested parties, as well as inviting editors, developers and community to give feedback on the aforementioned channels. You should try and gauge whether the interest in your PIP is commensurate with both the work involved in implementing it and how many parties will have to conform to it. For example, the work required for implementing a Core PIP will be much greater than for an ERC and the PIP will need sufficient interest from the Ethereum client teams. Negative community feedback will be taken into consideration and may prevent your PIP from moving past the Draft stage.

### Core PIPs

For Core PIPs, given that they require client implementations to be considered **Final** (see "PIPs Process" below), you will need to either provide an implementation for clients or convince clients to implement your PIP. 

The best way to get client implementers to review your PIP is to present it on an AllCoreDevs call. You can request to do so by posting a comment linking your PIP on an [AllCoreDevs agenda GitHub Issue].  

The AllCoreDevs call serve as a way for client implementers to do three things. First, to discuss the technical merits of PIPs. Second, to gauge what other clients will be implementing. Third, to coordinate PIP implementation for network upgrades.

These calls generally result in a "rough consensus" around what PIPs should be implemented. This "rough consensus" rests on the assumptions that PIPs are not contentious enough to cause a network split and that they are technically sound.

:warning: The PIPs process and AllCoreDevs call were not designed to address contentious non-technical issues, but, due to the lack of other ways to address these, often end up entangled in them. This puts the burden on client implementers to try and gauge community sentiment, which hinders the technical coordination function of PIPs and AllCoreDevs calls. If you are shepherding an PIP, you can make the process of building community consensus easier by making sure that [the Ethereum Magicians forum] thread for your PIP includes or links to as much of the community discussion as possible and that various stakeholders are well-represented.

*In short, your role as the champion is to write the PIP using the style and format described below, shepherd the discussions in the appropriate forums, and build community consensus around the idea.* 

### PIP Process 

Following is the process that a successful non-Core PIP will move along:

```
[ WIP ] -> [ DRAFT ] -> [ LAST CALL ] -> [ FINAL ]
```

Following is the process that a successful Core PIP will move along:

```
[ IDEA ] -> [ DRAFT ] -> [ LAST CALL ] -> [ ACCEPTED ] -> [ FINAL ]
```

Each status change is requested by the PIP author and reviewed by the PIP editors. Use a pull request to update the status. Please include a link to where people should continue discussing your PIP. The PIP editors will process these requests as per the conditions below.

* **Idea** -- Once the champion has asked the Ethereum community whether an idea has any chance of support, they will write a draft PIP as a [pull request]. Consider including an implementation if this will aid people in studying the PIP.
  * :arrow_right: Draft -- If agreeable, PIP editor will assign the PIP a number (generally the issue or PR number related to the PIP) and merge your pull request. The PIP editor will not unreasonably deny an PIP.
  * :x: Draft -- Reasons for denying draft status include being too unfocused, too broad, duplication of effort, being technically unsound, not providing proper motivation or addressing backwards compatibility, or not in keeping with the [Ethereum philosophy](https://github.com/ethereum/wiki/wiki/White-Paper#philosophy).
* **Draft** -- Once the first draft has been merged, you may submit follow-up pull requests with further changes to your draft until such point as you believe the PIP to be mature and ready to proceed to the next status. An PIP in draft status must be implemented to be considered for promotion to the next status (ignore this requirement for core PIPs).
  * :arrow_right: Last Call -- If agreeable, the PIP editor will assign Last Call status and set a review end date (`review-period-end`), normally 14 days later.
  * :x: Last Call -- A request for Last Call status will be denied if material changes are still expected to be made to the draft. We hope that PIPs only enter Last Call once, so as to avoid unnecessary noise on the RSS feed.
* **Last Call** -- This PIP will listed prominently on the https://eips.ethereum.org/ website (subscribe via RSS at [last-call.xml](/last-call.xml)).
  * :x: -- A Last Call which results in material changes or substantial unaddressed technical complaints will cause the PIP to revert to Draft.
  * :arrow_right: Accepted (Core PIPs only) -- A successful Last Call without material changes or unaddressed technical complaints will become Accepted.
  * :arrow_right: Final (Non-Core PIPs) -- A successful Last Call without material changes or unaddressed technical complaints will become Final.
* **Accepted (Core PIPs only)** -- This status signals that material changes are unlikely and Ethereum client developers should consider this PIP for inclusion. Their process for deciding whether to encode it into their clients as part of a hard fork is not part of the PIP process.
  * :arrow_right: Draft -- The Core Devs can decide to move this PIP back to the Draft status at their discretion. E.g. a major, but correctable, flaw was found in the PIP.
  * :arrow_right: Rejected -- The Core Devs can decide to mark this PIP as Rejected at their discretion. E.g. a major, but uncorrectable, flaw was found in the PIP.
  * :arrow_right: Final -- Standards Track Core PIPs must be implemented in at least three viable Ethereum clients before it can be considered Final. When the implementation is complete and adopted by the community, the status will be changed to “Final”.
* **Final** -- This PIP represents the current state-of-the-art. A Final PIP should only be updated to correct errata.

Other exceptional statuses include:

* **Active** -- Some Informational and Process PIPs may also have a status of “Active” if they are never meant to be completed. E.g. PIP 1 (this PIP).
* **Abandoned** -- This PIP is no longer pursued by the original authors or it may not be a (technically) preferred option anymore.
  * :arrow_right: Draft -- Authors or new champions wishing to pursue this PIP can ask for changing it to Draft status.
* **Rejected** -- An PIP that is fundamentally broken or a Core PIP that was rejected by the Core Devs and will not be implemented. An PIP cannot move on from this state.
* **Superseded** -- An PIP which was previously Final but is no longer considered state-of-the-art. Another PIP will be in Final status and reference the Superseded PIP. An PIP cannot move on from this state.

## What belongs in a successful PIP?

Each PIP should have the following parts:

- Preamble - RFC 822 style headers containing metadata about the PIP, including the PIP number, a short descriptive title (limited to a maximum of 44 characters), and the author details. See [below](https://github.com/ethereum/PIPs/blob/master/PIPS/eip-1.md#eip-header-preamble) for details.
- Abstract - A short (~200 word) description of the technical issue being addressed.
- Motivation (*optional) - The motivation is critical for PIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the PIP solves. PIP submissions without sufficient motivation may be rejected outright.
- Specification - The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Ethereum platforms (cpp-ethereum, go-ethereum, parity, ethereumJ, ethereumjs-lib, [and others](https://github.com/ethereum/wiki/wiki/Clients).
- Rationale - The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.
- Backwards Compatibility - All PIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The PIP must explain how the author proposes to deal with these incompatibilities. PIP submissions without a sufficient backwards compatibility treatise may be rejected outright.
- Test Cases - Test cases for an implementation are mandatory for PIPs that are affecting consensus changes. Other PIPs can choose to include links to test cases if applicable.
- Implementations - The implementations must be completed before any PIP is given status “Final”, but it need not be completed before the PIP is merged as draft. While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of “rough consensus and running code” is still useful when it comes to resolving many discussions of API details.
- Security Considerations - All PIPs must contain a section that discusses the security implications/considerations relevant to the proposed change. Include information that might be important for security discussions, surfaces risks and can be used throughout the life cycle of the proposal. E.g. include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks and how they are being addressed. PIP submissions missing the "Security Considerations" section will be rejected. An PIP cannot proceed to status "Final" without a Security Considerations discussion deemed sufficient by the reviewers.
- Copyright Waiver - All PIPs must be in the public domain. See the bottom of this PIP for an example copyright waiver.

## PIP Formats and Templates

PIPs should be written in [markdown] format.
Image files should be included in a subdirectory of the `assets` folder for that PIP as follows: `assets/eip-N` (where **N** is to be replaced with the PIP number). When linking to an image in the PIP, use relative links such as `../assets/eip-1/image.png`.

## PIP Header Preamble

Each PIP must begin with an [RFC 822](https://www.ietf.org/rfc/rfc822.txt) style header preamble, preceded and followed by three hyphens (`---`). This header is also termed ["front matter" by Jekyll](https://jekyllrb.com/docs/front-matter/). The headers must appear in the following order. Headers marked with "*" are optional and are described below. All other headers are required.

` eip:` *PIP number* (this is determined by the PIP editor)

` title:` *PIP title*

` author:` *a list of the author's or authors' name(s) and/or username(s), or name(s) and email(s). Details are below.*

` * discussions-to:` *a url pointing to the official discussion thread*

` status:` *Draft | Last Call | Accepted | Final | Active | Abandoned | Rejected | Superseded*

`* review-period-end:` *date review period ends*

` type:` *Standards Track | Informational | Meta*

` * category:` *Core | Networking | Interface | ERC* (Standards Track PIPs only)

` created:` *date created on*

` * updated:` *comma separated list of dates*

` * requires:` *PIP number(s)*

` * replaces:` *PIP number(s)*

` * superseded-by:` *PIP number(s)*

` * resolution:` *a url pointing to the resolution of this PIP*

Headers that permit lists must separate elements with commas.

Headers requiring dates will always do so in the format of ISO 8601 (yyyy-mm-dd).

#### `author` header

The `author` header optionally lists the names, email addresses or usernames of the authors/owners of the PIP. Those who prefer anonymity may use a username only, or a first name and a username. The format of the author header value must be:

> Random J. User &lt;address@dom.ain&gt;

or

> Random J. User (@username)

if the email address or GitHub username is included, and

> Random J. User

if the email address is not given.

#### `resolution` header

The `resolution` header is required for Standards Track PIPs only. It contains a URL that should point to an email message or other web resource where the pronouncement about the PIP is made.

#### `discussions-to` header

While an PIP is a draft, a `discussions-to` header will indicate the mailing list or URL where the PIP is being discussed. As mentioned above, examples for places to discuss your PIP include [Ethereum topics on Gitter](https://gitter.im/ethereum/topics), an issue in this repo or in a fork of this repo, [Ethereum Magicians](https://ethereum-magicians.org/) (this is suitable for PIPs that may be contentious or have a strong governance aspect), and [Reddit r/ethereum](https://www.reddit.com/r/ethereum/).

No `discussions-to` header is necessary if the PIP is being discussed privately with the author.

As a single exception, `discussions-to` cannot point to GitHub pull requests.

#### `type` header

The `type` header specifies the type of PIP: Standards Track, Meta, or Informational. If the track is Standards please include the subcategory (core, networking, interface, or ERC).

#### `category` header

The `category` header specifies the PIP's category. This is required for standards-track PIPs only.

#### `created` header

The `created` header records the date that the PIP was assigned a number. Both headers should be in yyyy-mm-dd format, e.g. 2001-08-14.

#### `updated` header

The `updated` header records the date(s) when the PIP was updated with "substantial" changes. This header is only valid for PIPs of Draft and Active status.

#### `requires` header

PIPs may have a `requires` header, indicating the PIP numbers that this PIP depends on.

#### `superseded-by` and `replaces` headers

PIPs may also have a `superseded-by` header indicating that an PIP has been rendered obsolete by a later document; the value is the number of the PIP that replaces the current document. The newer PIP must have a `replaces` header containing the number of the PIP that it rendered obsolete.

## Auxiliary Files

PIPs may include auxiliary files such as diagrams. Such files must be named PIP-XXXX-Y.ext, where “XXXX” is the PIP number, “Y” is a serial number (starting at 1), and “ext” is replaced by the actual file extension (e.g. “png”).

## Transferring PIP Ownership

It occasionally becomes necessary to transfer ownership of PIPs to a new champion. In general, we'd like to retain the original author as a co-author of the transferred PIP, but that's really up to the original author. A good reason to transfer ownership is because the original author no longer has the time or interest in updating it or following through with the PIP process, or has fallen off the face of the 'net (i.e. is unreachable or isn't responding to email). A bad reason to transfer ownership is because you don't agree with the direction of the PIP. We try to build consensus around an PIP, but if that's not possible, you can always submit a competing PIP.

If you are interested in assuming ownership of an PIP, send a message asking to take over, addressed to both the original author and the PIP editor. If the original author doesn't respond to email in a timely manner, the PIP editor will make a unilateral decision (it's not like such decisions can't be reversed :)).

## PIP Editors

The current PIP editors are

` * Nick Johnson (@arachnid)`

` * Casey Detrio (@cdetrio)`

` * Hudson Jameson (@Souptacular)`

` * Vitalik Buterin (@vbuterin)`

` * Nick Savers (@nicksavers)`

` * Martin Becze (@wanderer)`

` * Greg Colvin (@gcolvin)`

` * Alex Beregszaszi (@axic)`

## PIP Editor Responsibilities

For each new PIP that comes in, an editor does the following:

- Read the PIP to check if it is ready: sound and complete. The ideas must make technical sense, even if they don't seem likely to get to final status.
- The title should accurately describe the content.
- Check the PIP for language (spelling, grammar, sentence structure, etc.), markup (GitHub flavored Markdown), code style

If the PIP isn't ready, the editor will send it back to the author for revision, with specific instructions.

Once the PIP is ready for the repository, the PIP editor will:

- Assign an PIP number (generally the PR number or, if preferred by the author, the Issue # if there was discussion in the Issues section of this repository about this PIP)

- Merge the corresponding pull request

- Send a message back to the PIP author with the next step.

Many PIPs are written and maintained by developers with write access to the Ethereum codebase. The PIP editors monitor PIP changes, and correct any structure, grammar, spelling, or markup mistakes we see.

The editors don't pass judgment on PIPs. We merely do the administrative & editorial part.

## History

This document was derived heavily from [Bitcoin's BIP-0001] written by Amir Taaki which in turn was derived from [Python's PEP-0001]. In many places text was simply copied and modified. Although the PEP-0001 text was written by Barry Warsaw, Jeremy Hylton, and David Goodger, they are not responsible for its use in the Ethereum Improvement Process, and should not be bothered with technical questions specific to Ethereum or the PIP. Please direct all comments to the PIP editors.

December 7, 2015: PIP 1 has been improved and will be placed as a PR.

February 1, 2016: PIP 1 has added editors, made draft improvements to process, and has merged with Master stream.

March 21, 2018: Minor edits to accommodate the new automatically-generated PIP directory on [eips.ethereum.org](https://eips.ethereum.org/).

May 29, 2018: A last call process was added.

Oct 17, 2018: The `updated` header was introduced.

May 19, 2019: The **Abandoned** status was introduced.

Dec 4, 2019: The "Security Considerations" section was introduced.

See [the revision history for further details](https://github.com/ethereum/PIPs/commits/master/PIPS/eip-1.md), which is also available by clicking on the History button in the top right of the PIP.

### Bibliography

[PIP5]: https://github.com/ethereum/PIPs/blob/master/PIPS/eip-5.md
[PIP101]: https://github.com/ethereum/PIPs/issues/28
[PIP90]: https://github.com/ethereum/PIPs/issues/90
[PIP86]: https://github.com/ethereum/PIPs/issues/86#issue-145324865
[devp2p]: https://github.com/ethereum/wiki/wiki/%C3%90%CE%9EVp2p-Wire-Protocol
[PIP8]: https://github.com/ethereum/PIPs/blob/master/PIPS/eip-8.md
[Light Ethereum Subprotocol]: https://github.com/ethereum/wiki/wiki/Light-client-protocol
[whisper]: https://github.com/ethereum/go-ethereum/wiki/Whisper-Overview
[swarm]: https://github.com/ethereum/go-ethereum/pull/2959
[API/RPC]: https://github.com/ethereum/wiki/wiki/JSON-RPC
[PIP6]: https://github.com/ethereum/PIPs/blob/master/PIPS/eip-6.md
[contract ABIs]: https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI
[interfaces repo]: https://github.com/ethereum/interfaces
[ERC20]: https://github.com/ethereum/PIPs/issues/20
[ERC26]: https://github.com/ethereum/PIPs/issues/26
[ERC137]: https://github.com/ethereum/PIPs/issues/137
[ERC67]: https://github.com/ethereum/PIPs/issues/67
[PIP82]: https://github.com/ethereum/PIPs/issues/82
[PIP75]: https://github.com/ethereum/PIPs/issues/75
[PIP85]: https://github.com/ethereum/PIPs/issues/85
[the Ethereum subreddit]: https://www.reddit.com/r/ethereum/
[one of the Ethereum Gitter chat rooms]: https://gitter.im/ethereum/
[pull request]: https://github.com/ethereum/PIPs/pulls
[formal specification]: https://github.com/ethereum/yellowpaper
[the Issues section of this repository]: https://github.com/ethereum/PIPs/issues
[markdown]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[Bitcoin's BIP-0001]: https://github.com/bitcoin/bips
[Python's PEP-0001]: https://www.python.org/dev/peps/
[the Ethereum Magicians forum]: https://ethereum-magicians.org/
[AllCoreDevs agenda GitHub Issue]: https://github.com/ethereum/pm/issues

## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
