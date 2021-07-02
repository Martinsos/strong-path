# StrongPath

[![CI](https://img.shields.io/github/workflow/status/wasp-lang/strong-path/CI/master)](https://github.com/wasp-lang/strong-path/actions/workflows/ci.yaml?query=branch%3Amaster)
[![Hackage](https://img.shields.io/hackage/v/strong-path.svg)](https://hackage.haskell.org/package/strong-path)
[![Stackage LTS](http://stackage.org/package/strong-path/badge/lts)](http://stackage.org/lts/package/strong-path)
[![Stackage Nightly](http://stackage.org/package/strong-path/badge/nightly)](http://stackage.org/nightly/package/strong-path)

Strongly typed file paths in Haskell.

This library provides a strongly typed representation of file paths, providing more safety during compile time while also making code more readable, compared to the standard solution (`FilePath`, which is really just `String`).

Without `StrongPath`:
```hs
getGitConfigPath :: IO FilePath
generateHtmlFromMarkdown :: FilePath -> IO FilePath
```

With `StrongPath`:
```hs
getGitConfigPath :: IO (Path System (Rel HomeDir) (File GitConfigFile))
generateHtmlFromMarkdown :: Path System (Rel HomeDir) (File MarkdownFile) -> IO (Path System Abs (File HtmlFile))
```

Simple but complete example:
```hs
import StrongPath (Path, System, Abs, Rel, File, Dir, (</>), parseAbsDir)

data HomeDir

getHomeDirPath :: IO (Path System Abs (Dir HomeDir))
getHomeDirPath = getLine >>= fromJust . parseAbsDir
```

Check [documentation](https://hackage.haskell.org/package/strong-path/docs/StrongPath.html) for more details!

## Documentation
Detailed documentation, including rich examples and API is written via Haddock.

Check out the latest documentation on Hackage: [Documentation](https://hackage.haskell.org/package/strong-path/docs/StrongPath.html).

You can also build and view the Haddock documentation yourself if you wish, by running `stack haddock --open`.

## Contributing / development
We are using `ormolu` for code formatting. In order for the PR to pass, it needs to be formatted by `ormolu`.

`strong-path` is `Stack` project, so make sure you have `stack` installed on your machine.

`stack build` to build the project, `stack test` to run the tests.

`stack build --file-watch --haddock` to rebuild documentation as you change it.

### Publishing to Hackage

`stack sdist` to build publishable .tar.gz., and then we need to upload it manually.

Make sure to update the version of package in package.yaml.

We should also tag the commit in git with version tag (e.g. v1.0.0.0) so we know which version of code was used to produce that release.
