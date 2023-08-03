<!-- SPDX-License-Identifier: CC0-1.0 -->
<!-- written in 2022 by The Foundation for Public Code <info@publiccode.net> -->
# Releasing a new version of the Governance Game

1. Review state of the 'develop' branch
    - Ensure all changes intended for release are merged
    - Invite a proofread of the current state of the branch
2. Create a release branch
    - From 'develop', `git switch -c "release-$MAJOR.$MINOR.$PATCH"`
    - Push the branch, `git push -u origin release-$MAJOR.$MINOR.$PATCH`
3. Update the new release
    - [ ] Update version number in `cards/rules-about.tex` and `README.md`
        - Note: the version on the box is updated by the release script
    - [ ] Update [`AUTHORS.md`](../AUTHORS.md) with new contributors
    - [ ] Update [`CHANGELOG.md`](../CHANGELOG.md)
    - [ ] Perform extra pass on diff to the 'main' branch
        - Run `make view-all`
        - Run `make check`
        - If needed, commit fixes and repeat extra pass
    - [ ] Push branch, open a pull request to the 'main' branch
        - Request review
        - Reviewers will create issues for shortcomings found which would not prevent release
        - If needed for release, reviewers may create pull requests to resolve issues
        - Re-request reviews if additional pull requests are merged into release branch
    - [ ] Once reviews are complete, merge to 'main'
4. Create GitHub release with the release notes and version number
    - [ ] Wait for tests to "go green" on GitHub for the main branch
    - [ ] Switch to the 'main' branch, `git pull` and `git status`
    - [ ] `git tag $MAJOR.$MINOR.$PATCH`
    - [ ] `git push --tags`
        - This should generate the release, with changelog bullets
5. Update 'develop' with a merge from 'main'
6. Rebuild the GitHub Pages
    - [ ] Navigate to the [GitHub action](https://github.com/publiccodenet/governance-game/actions/workflows/pages/pages-build-deployment)
        - Select the latest run
        - Click "Re-run all jobs"
7. [Send the files for print to the printer](PRINTING.md)
