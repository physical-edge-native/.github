# Contributing to Physical-Edge Native projects

Thank you for your interest. This guide applies to every repository of the
[physical-edge-native](https://github.com/physical-edge-native) organization that does not have its own
`CONTRIBUTING.md`. A repository's own file, if it has one, comes first.

The projects are maintained by one person, so replies may take a few days (usually within a week).
Issues and pull requests may be written in English or Japanese.

## Before you start

- **Questions** ("how do I…?"): ask in [GitHub Discussions](https://github.com/physical-edge-native/dyne/discussions)
  or on Discord (see [SUPPORT.md](SUPPORT.md)).
- **Bugs**: open an Issue in the repository where the bug is.
- **Changes**: open an Issue first, unless the change is a small fix (a typo, a broken link). Say what you want to
  change and why, so we can agree on the approach before you spend time on it. Issues labelled
  `good first issue` are a good place to start.

## How a change gets in

Issue → branch → pull request → CI → review → merge.

1. An Issue describes the problem or the idea.
2. You make the change on a branch in your fork.
3. You open a pull request that says `Closes #<issue number>`.
4. CI (the automatic checks) runs. **For pull requests from forks, CI starts only after the maintainer approves
   it**, so do not worry if the checks wait at first.
5. The maintainer reviews the pull request and may ask for changes.
6. When CI passes and the review is done, the maintainer merges it.

## Step by step: your first pull request

You need a GitHub account and [Git](https://git-scm.com/downloads). Replace `<repo>` with the repository name
(for example `dyne`) and `<you>` with your GitHub user name.

1. **Fork**: open the repository on GitHub and press **Fork** (top right). This makes your own copy,
   `https://github.com/<you>/<repo>`.
2. **Clone your fork** to your computer:

   ```sh
   git clone https://github.com/<you>/<repo>.git
   cd <repo>
   git remote add upstream https://github.com/physical-edge-native/<repo>.git
   ```

3. **Make a branch** named `<issue number>-<short-description>`:

   ```sh
   git switch -c 12-fix-typo-in-readme
   ```

4. **Change the files**, then run the repository's checks if it has them (its README says how; for dyne,
   `bash scripts/ci-check.sh`).
5. **Commit** with a short English message that says what changed:

   ```sh
   git add <the files you changed>
   git commit -m "Fix a typo in the README (#12)"
   ```

6. **Push** the branch to your fork:

   ```sh
   git push -u origin 12-fix-typo-in-readme
   ```

7. **Open the pull request**: GitHub shows a **Compare & pull request** button on your fork. Fill in the
   template and press **Create pull request**.
8. **Update it if asked**: commit and push to the same branch again; the pull request updates by itself.
   If the main branch moved on, bring your branch up to date:

   ```sh
   git fetch upstream
   git rebase upstream/main
   git push --force-with-lease
   ```

## Never commit secrets or personal information

The repositories are public, and anything committed stays in the history. Do **not** commit:

- Wi-Fi names and passwords, API keys, tokens, private keys;
- personal information (e-mail addresses, home addresses, names of people who did not agree);
- **real MAC addresses** of devices. In examples and recorded data, use locally administered addresses such as
  `02:00:00:00:00:01`.

Keep local settings in files that Git ignores (each repository's README names them). GitHub also blocks pushes
that contain known kinds of secrets. If you committed a secret by mistake, tell the maintainer privately (see
[SECURITY.md](SECURITY.md)) and change the secret; deleting the file in a later commit is not enough.

## License of contributions

The repositories are licensed under either of MIT or Apache-2.0, at your option. Unless you explicitly state
otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the
Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.

No sign-off line and no contributor license agreement are needed.

## Using AI tools

You may use AI coding assistants. Say so in the pull request, and check what they wrote: you are responsible for
the change, and numerical results must still pass the repository's checks.

## Code of conduct

Everyone taking part follows the [Code of Conduct](CODE_OF_CONDUCT.md).
