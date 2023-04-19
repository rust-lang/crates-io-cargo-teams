- Start Date: 2019-03-22
- RFC PR: (leave this blank)
- cargo/crates.io issue: (leave this blank)

# Summary

This describes the RFC process for the crates.io and Cargo teams, separate from
the general RFC process. While it is expected that the majority of RFCs opened
here would come from members of the crates.io or cargo teams, new RFCs and
discussion from others is both welcomed and encouraged.

# Motivation

The goal of creating a separate RFC repo and process for these teams is to
increase communication, while decreasing noise in the main RFC repo. A large
number of changes would benefit from going through the RFC process, but either
only affect the two teams, or are irrelevant to the majority of Rust's users.

By providing our own RFC repo, we are able to give a better process to propose
changes which affect both teams, and give users who are interested in lower
level changes a single repo to watch that doesn't include noise from bug fixes,
etc.

Finally, this allows us to propose changes which we wish to give users a chance
to chime in on, without requiring them to attend a team meeting. This also
reduces reliance on synchronous meetings for members of the teams, which are
becoming increasingly distributed.

# Impact on both teams

Many things which are currently only discussed in issues/PRs or team meetings
would be expected to go through an RFC in this repo. RFCs opened against the
main repo assigned to either team may be closed if they are better suited to be
opened here.

Many RFCs should still be opened on the main repo. When it's unclear where it
belongs, it's left to the discretion of the teams to decide which location is
more appropriate.

Once an RFC is opened, the process would be broadly the same as the main RFC
repo. One or both teams will be tagged, and any member of either team can
propose an FCP for an RFC. Entering FCP requries sign-off from all members of
all assigned teams. After an FCP period of 1 week, a reprensentative from each
of the assigned teams will indicate whether any comments raised during FCP
justify returning to development mode, or following through on the disposition
of the FCP. This does not require full sign-off from the teams, and it is
expected that the team representative is reporting on the consensus from the
last team meeting.

# Impact on cargo

## Things which should have an RFC in the main RFCs repo

- Changes which affect a substantial portion of the users of Cargo
  - Whether a feature is "high profile" enough to justify landing on the main
    repo is up to the discretion of the Cargo team. A good rule of thumb is that
    if a "guide level explanation" is an important part of the RFC, it should
    not be in this repo
- Changes that affect how Cargo interacts with the compiler

## Things which should have an RFC in this repo

- Changes which require implementation on crates.io
  - For example, publishing precompiled binaries
- Changes which affect the expected format of the index
  - For example, adding new fields, squashing the index, changing the
    capabilities of config.json
- Changes which do not affect crates.io, but should have visibility on the
  crates.io team
  - For example, changes to when errors are reported to users, substantial
    changes to the requests sent by Cargo
- User facing features which are not expected to affect a substantial portion of
  users of Cargo, which do not affect the compiler

## Things which do not require an RFC

- Changes which do not impact users of Cargo, the index, or crates.io
- Changes being made for security reasons

# Impact on crates.io

## Things which should have an RFC in the main RFCs repo

- Policy changes which are expected to gather a large amount of external
  feedback
  - Whether a change falls under this umbrella is left to the discretion of the
    crates.io team
  - Examples of this would be policies affecting crate ownership, or removal of
    crates.
- UI changes which affect the greater Rust ecosystem
  - Whether a change falls under this umbrella is left to the discretion of the
    crates.io team
  - Examples include changing the default search order, major changes to
    discoverability of crates.
- UI changes or new features which are expected to gather a large amount of
  external feedback
  - Examples include a redesign of the website

## This which should have an RFC in this repo

- API changes which affect Cargo
  - Examples include changing how publish works, what endpoints are accessible,
    or anything else which requires implementation on the Cargo side
- Changes to how the index works
  - Examples include increasing the potential delay between a crate being
    published and when it appears in the index, changes to the format of the
    index, changes to the capabilities of config.json
- Changes impacting alternative registries
  - Examples include introducing a new version of an existing capability,
    deprecating an endpoint, introducing new capabilities that alternative
    registries are expected to implement.
  - Note that this only applies to changes that an alternative registry would
    need to make to their code base to continue to be supported by Cargo. It is
    not intended to set the expectation that the crates.io codebase is a
    turn-key solution for spinning up an alternative registry
- Policy changes which are legally required
  - This applies to changes which we know we are going to do one way or another,
    regarless of user feedback, but want to discuss specific details
  - Examples include changes to required information for DMCA details

## Things which do not require an RFC

- Operational changes which are time sensitive
  - Examples include changes to rate limiting or blocked traffic forms to combat
    recent or ongoing incidents
- Minor new features
  - Whether a feature falls under this umbrella is left to the discretion of the
    crates.io team
- Any changes which do not impact users

# Drawbacks

This introduces a lot of ceremony around things which the teams were previously
able to do uninhibited. This can be seen as either a good thing or a drawback,
depending on your perspective.

# Rationale and alternatives

The only real alternative is to continue to rely on team meetings and issues for
cross-team communication.

For a member of one team to use meetings to propose changes to the other, this
now requires them to attend multiple synchronous meetings in a week, which is
prohibitive for many people's schedules, and restricts participation from folks
in other time zones.

Issues and PRs serve a purpose, but it's difficult for a member of one team to
follow the other's repo, as the majority of issues and pull requests don't
affect them. It becomes difficult to separate out the issues they need to care
about.

While it will likely slow some new features down, it will also reduce the amount
of cases where the teams step on each others toes. It also allows the teams to
operate more openly, and allow interested parties to better follow the changes
happening to these parts of the Rust ecosystem.

By requiring RFCs for cross-team concerns, we will reduce the number of
incidents of an issue/PR on one team's repo surprising members of the other
team, or features landing without discussion of additional steps that should be
taken on both sides.
