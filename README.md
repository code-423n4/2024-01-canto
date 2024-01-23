# ✨ So you want to run an audit

This `README.md` contains a set of checklists for our audit collaboration.

Your audit will use two repos: 
- **an _audit_ repo** (this one), which is used for scoping your audit and for providing information to wardens
- **a _findings_ repo**, where issues are submitted (shared with you after the audit) 

Ultimately, when we launch the audit, this repo will be made public and will contain the smart contracts to be reviewed and all the information needed for audit participants. The findings repo will be made public after the audit report is published and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the audit sponsor (⭐️)**.

---

# Audit setup

## 🐺 C4: Set up repos
- [ ] Create a new private repo named `YYYY-MM-sponsorname` using this repo as a template.
- [ ] Rename this repo to reflect audit date (if applicable)
- [ ] Rename auditt H1 below
- [ ] Update pot sizes
- [ ] Fill in start and end times in audit bullets below
- [ ] Add link to submission form in audit details below
- [ ] Add the information from the scoping form to the "Scoping Details" section at the bottom of this readme.
- [ ] Add matching info to the Code4rena site
- [ ] Add sponsor to this private repo with 'maintain' level access.
- [ ] Send the sponsor contact the url for this repo to follow the instructions below and add contracts here. 
- [ ] Delete this checklist.

# Repo setup

## ⭐️ Sponsor: Add code to this repo

- [ ] Create a PR to this repo with the below changes:
- [ ] Provide a self-contained repository with working commands that will build (at least) all in-scope contracts, and commands that will run tests producing gas reports for the relevant contracts.
- [ ] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 48 business hours prior to audit start time.**
- [ ] Be prepared for a 🚨code freeze🚨 for the duration of the audit — important because it establishes a level playing field. We want to ensure everyone's looking at the same code, no matter when they look during the audit. (Note: this includes your own repo, since a PR can leak alpha to our wardens!)


---

## ⭐️ Sponsor: Edit this `README.md` file

- [ ] Modify the contents of this `README.md` file. Describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. (Here are two well-constructed examples: [Ajna Protocol](https://github.com/code-423n4/2023-05-ajna) and [Maia DAO Ecosystem](https://github.com/code-423n4/2023-05-maia))
- [ ] Review the Gas award pool amount. This can be adjusted up or down, based on your preference - just flag it for Code4rena staff so we can update the pool totals across all comms channels.
- [ ] Optional / nice to have: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] [This checklist in Notion](https://code4rena.notion.site/Key-info-for-Code4rena-sponsors-f60764c4c4574bbf8e7a6dbd72cc49b4#0cafa01e6201462e9f78677a39e09746) provides some best practices for Code4rena audits.

## ⭐️ Sponsor: Final touches
- [ ] Review and confirm the details in the section titled "Scoping details" and alert Code4rena staff of any changes.
- [ ] Review and confirm the list of in-scope files in the `scope.txt` file in this directory.  Any files not listed as "in scope" will be considered out of scope for the purposes of judging, even if the file will be part of the deployed contracts.
- [ ] Check that images and other files used in this README have been uploaded to the repo as a file and then linked in the README using absolute path (e.g. `https://github.com/code-423n4/yourrepo-url/filepath.png`)
- [ ] Ensure that *all* links and image/file paths in this README use absolute paths, not relative paths
- [ ] Check that all README information is in markdown format (HTML does not render on Code4rena.com)
- [ ] Remove any part of this template that's not relevant to the final version of the README (e.g. instructions in brackets and italic)
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Canto Invitational audit details
- Total Prize Pool: $16,425 USDC 
  - HM awards: $12,285 in USDC 
  - Analysis awards: $683 in USDC 
  - QA awards: $341 in USDC 
  - Gas awards: $341 in USDC 
  - Judge awards: $2,275 in USDC 
  - Scout awards: $500 in USDC 
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2024-01-canto-invitational/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts January 25, 2024 20:00 UTC 
- Ends January 29,2024 20:00 UTC 

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2024-01-canto/blob/main/4naly3er-report.md).

_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

Risks deemed acceptable:
- Everything related to governance / centralization abuse: We assume that governance is non-malicious. 

# Overview

## Links

- **Previous audits:** https://code4rena.com/audits/2023-08-verwa
- **Documentation:** https://code4rena.com/audits/2023-08-verwa and below


# Scope

[ ⭐️ SPONSORS: add scoping and technical details here ]

- [ ] In the table format shown below, provide the name of each contract and:
  - [ ] source lines of code (excluding blank lines and comments) in each *For line of code counts, we recommend running prettier with a 100-character line length, and using [cloc](https://github.com/AlDanial/cloc).* 
  - [ ] external contracts called in each
  - [ ] libraries used in each

*List all files in scope in the table below (along with hyperlinks) -- and feel free to add notes here to emphasize areas of focus.*

| Contract | SLOC | Purpose | Libraries used |  
| ----------- | ----------- | ----------- | ----------- |
| [src/LendingLedger.sol](https://github.com/code-423n4/2024-01-canto/blob/src/LendingLedger.sol) | 106 | Implements the bookkeeping for the rewards and is used for claiming. Moreover, provides data for third-party contracts that want to use this information for secondary rewards | [`@openzeppelin/*`](https://openzeppelin.com/contracts/) |

## Out of scope

All other contracts.

# Additional Context

Since the previous audit, the `LendingLedger` logic was completely rewritten. We now use an approach that is very similar to [MasterChef / Synthetix](https://www.rareskills.io/post/staking-algorithm). The main motivation for doing that was to enable users to claim accrued rewards whenever they want (instead of only after a week / epoch has passed). Moreover, we also introduced the field `secRewardDebt`. The idea of this field is to enable any lending platforms that are integrated with Neofinance Coordinator to send their own rewards based on this value (or rather the difference of this value since the last time secondary rewards were sent) and their own emission schedule for the tokens.

The code will only be deployed to CANTO.

The only trusted role is the governance address. Only this address can set the rewards per block.

## Attack ideas (Where to look for bugs)
Miscalculations / significant rounding errors

## Main invariants
The total rewards that are sent for one block should never be higher than the rewards that were configured for this block.

## Scoping Details 

```
- If you have a public code repo, please share it here:  
- How many contracts are in scope?:   1
- Total SLoC for these contracts?:  107
- How many external imports are there?: 4 
- How many separate interfaces and struct definitions are there for the contracts within scope?:  2
- Does most of your code generally use composition or inheritance?:   Composition
- How many external calls?:   1
- What is the overall line coverage percentage provided by your tests?: 94
- Is this an upgrade of an existing system?: True - LendingLedger of the already audited veRWA (https://code4rena.com/audits/2023-08-verwa) was rewritten. It now supports per-block claiming (vs. per-epoch previously) and we expose data in the contract that enables secondary rewards (i.e. for other systems to incentivize deposits with their own tokens)
- Check all that apply (e.g. timelock, NFT, AMM, ERC20, rollups, etc.): 
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?:   True
- Please describe required context:  The changes since the last audit only affect one contract and are isolated, but it can be helpful for context to look at the overall system, which was described in the previous audit (https://code4rena.com/audits/2023-08-verwa) 
- Does it use an oracle?:  No
- Describe any novel or unique curve logic or mathematical models your code uses: The staking logic is adapted from Sushi / Synthetix: https://www.rareskills.io/post/staking-algorithm
- Is this either a fork of or an alternate implementation of another project?:   True
- Does it use a side-chain?: 
- Describe any specific areas you would like addressed:
```

# Tests

```npm install && forge test``````

## Miscellaneous

Canto contributors that were involved in the creation of Neofinance Coordinator and their family members are ineligible to participate in this audit.
