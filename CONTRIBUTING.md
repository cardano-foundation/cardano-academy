# Contributing

## Folder organization & conventions

- [x] Courses are placed in their own directory, under a top-level directory [_courses_](./courses).
- [x] Longer courses can be divided into _modules_ and _units_. A module is a collection of units.
- [x] Units shall be placed in their own directory, with a single `README.md` file as the content.
- [x] Diagrams or illustrations shall be nested in units' directories under `assets`.
- [x] Modules and units must be numbered, starting from 1. They shall also have a title.
- [x] Prefer underscores over spaces in folders and filenames.
- [x] Modules and units shall be named as `{number}-{title}`. e.g. `1-blockchain_overview`

## Feedback

Feedback is welcome, whether it be a suggestion, contributing an improved infographic, or maybe some questions that you have. It helps in improving the course(s) over time and these are the best kind of contributions to start with.

Do not hesitate to add *thumbs up* 👍 on suggestions you support to show your interest.

Any updates, typo fixes, or expansion of the course content is more than welcome. **Note however that courses are generally targeted at a specific audience, generally beginner, intermediate, advanced. We often cover the same topic in more detail in later course(s).**

Pull requests are welcome, but we do recommend you open an issue to bring any idea to discussion first! Especially if the pull request will end up very large, any significant changes should be discussed up front with the maintainers. This avoids awkward situations where someone puts in a bunch of work to ultimately have the pull request closed due to a potential variety of unforeseen reasons.

The content is in 'markdown' format, a cheatsheet is available [here](https://www.markdownguide.org/cheat-sheet/).

## License and attribution

All contributions must be properly licensed and attributed. If you are contributing your own original work, then you are offering it under a [CC-BY 4.0](./LICENSE).

If you are sourcing a contribution from somewhere else, it must carry a compatible license. You need to indicate the original source and original license, by including an comment above your contribution in this suggested format:

```
Source: https://example.com/originaltext
License: CC-BY 4.0
Added by: @joebloggs
```

## Changelog

We keep changelogs for each course. Please add an entry into their corresponding _CHANGELOG.md_ when submitting changes. This let's us keep track of unreleased changes for future course iterations. Each changelog must abide by the following format:

```
## {version} - {YYYY-MM-DD}

### Added

- some new thing

### Changed

- fixed or updated something

### Removed

- something is gone now
```

> [!TIP]
>
> When not-yet-release, use `unreleased` as a version and date.

## Discussions

💡 Do you have an Idea to propose, or a question to ask? ❓<br>
...Feel free to [Start a discussion](https://github.com/cardano-foundation/cardano-academy/discussions/new/choose)

## Thanks
As Cardano constantly evolves, feedback and contributions are welcome, and indeed needed. We are very grateful for the support of the entire Cardano community. Thank you!

*Contact us:* <academy@cardanofoundation.org>
