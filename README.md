
Capture
==================

  - [About](#about)
  - [Usage](#usage)
    - [IOS](#ios)
    - [Android](#android)
  - [Links](#license)


## About

Capture makes reporting bugs easy, which increases the productivity of your test engineers; standardized reporting enables your developers to focus on fixing the bug instead of finding and reproducing it.

Capture greatly improves your mobile testing processes.
Just shake the phone to report a bug and be amazed how
easy it can be.


## Usage
**It's really simple!**

- If your **`git remote`** `origin` refers to your GitHub repo, just go to your project folder and run:

		github_changelog_generator

-  Or, run this from anywhere:
    - `github_changelog_generator -u github_username -p github_project`
    - `github_changelog_generator  github_username/github_project`

This generates a changelog to the `CHANGELOG.md` file, with pretty markdown formatting.

###IOS:

####Static Lib Requirements :

1) Turn off App Transportation Security

2) Target -> Build Settings -> Write “other linker flag” to search and add -ObjC -all_load to the related place

####To AppDelegate.m file

```
#import "MobvenBugReporter.h"
``` 
import in this way. 
```
didFinishLaunchingWithOptions
```
add the following code in the method above:

```
[MobvenBugReporter initializeAppSecret:@"1" appId:@"1" projectId:@"1" in- vokeTypes:@[@(Shake), @(FloatingButton)]];
```

####Usage of Embedded Framework//Objective C // ----------

1) Target-> General -> Embedded Binaries
Add MobvenBugKit.framework

2) Target -> Build Settings -> Write "Bitcode" to search and set the related place as 'YES'

3) Turn off App Transportation Security

####To the AppDelegate.m File:
```
#import <MobvenBugKit/MobvenBugKit.h>
didFinishLaunchingWithOptions
```
add the following code in the method above: 
```
[MobvenBugReporter initializeAppSecret:@"1" appId:@"1" projectId:@"1" in- vokeTypes:@[@(Shake), @(FloatingButton)]];
```

####Usage of Embedded Framework//Swift // —————

1) Target-> General -> Embedded Binaries
Add MobvenBugKit.framework

2) Target -> Build Settings -> Write "Bitcode" to Search and set the related place as 'YES'

3) Turn off App Transportation Security

####To the AppDelegate file:
```
import MobvenBugKit
didFinishLaunchingWithOptions
```
add the following code to the method above:
```
let types = [NSNumber(unsignedInteger:InvocationType.Shake.rawValue),NSNumber(un- signedInteger:InvocationType.FloatingButton.rawValue)]
MobvenBugReporter.initializeAppSecret("1", appId: "1", projectId: "1", in- vokeTypes:types)
```

### For Android
In your project root, you can put a params file named `.github_changelog_generator` to override default params:

Example:
```
unreleased=false
future-release=5.0.0
since-tag=1.0.0
```

### GitHub token

GitHub only allows only 50 unauthenticated requests per hour. 
Therefore, it's recommended to run this script with authentication by using a **token**.

Here's how:

- [Generate a token here](https://github.com/settings/tokens/new?description=GitHub%20Changelog%20Generator%20token) - you only need "repo" scope for private repositories
- Either:
    - Run the script with `--token <your-40-digit-token>`; **OR**
    - Set the `CHANGELOG_GITHUB_TOKEN` environment variable to your 40 digit token

You can set an environment variable by running the following command at the prompt, or by adding it to your shell profile (e.g., `~/.bash_profile` or `~/.zshrc`):

        export CHANGELOG_GITHUB_TOKEN="«your-40-digit-github-token»"

So, if you got an error like this:
>! /Library/Ruby/Gems/2.0.0/gems/github_api-0.12.2/lib/github_api/response/raise_error.rb:14:in `on_complete'

It's time to create this token! (Or, wait an hour for GitHub to reset your unauthenticated request limit.)

## Migrating from a manual changelog

Knowing how dedicated you are to your project, you probably haven't been waiting for `github-changelog-generator` to keep a changelog.
But you probably don't want your project's open issues and PRs for all past features listed in your historic changelog, either.

That's where `--base <your-manual-changelog.md>` comes in handy!
This option lets append your old manual changelog to the end of the generated entries.

If you have a `HISTORY.md` file in your project, it will automatically be picked as the static historical changelog and appended.

### Rake task

You love `rake`? We do, too! So, we've made it even easier for you: 
we've provided a `rake` task library for your changelog generation.

Just put something like this in your `Rakefile`:

```ruby
GitHubChangelogGenerator::RakeTask.new :changelog do |config|
  config.since_tag = '0.1.14'
  config.future_release = '0.2.0'
end
```

All command line options can be passed to the `rake` task as `config` parameters. And since you're naming the `rake` task yourself, you can create as many as you want.

## Features and advantages of this project
- Generate canonical, neat change log file, followed by [basic change log guidelines](http://keepachangelog.com) :gem:
- Optionally generate **Unreleased** changes (closed issues that have not released yet) :dizzy:
- **GitHub Enterprise support** via command line options! :factory:
- Flexible format **customization**:
    - **Customize** issues that **should be added** to changelog :eight_spoked_asterisk:
    - **Custom date formats** supported (but keep [ISO 8601](http://xkcd.com/1179/) in mind!) :date:
    - Manually specify the version that fixed an issue (for cases when the issue's Closed date doesn't match) by giving the issue's `milestone` the same name as the tag of version :pushpin:
    - Automatically **exclude specific issues** that are irrelevant to your changelog (by default, any issue labeled `question`, `duplicate`, `invalid`, or `wontfix`) :scissors:
- **Distinguish** issues **by labels**. :mag_right:
    - Merged pull requests (all merged pull-requests) :twisted_rightwards_arrows:
    - Bug fixes (issues labeled `bug`) :beetle:
    - Enhancements (issues labeled `enhancement`) :star2:
    - Issues (closed issues with no labels) :non-potable_water:

- Manually include or exclude issues by labels :wrench:
- Customize lots more! Tweak the changelog to fit your preferences :tophat:
(*See `github_changelog_generator --help`  for details)*


###Alternatives
Here is a [wikipage list of alternatives](https://github.com/skywinder/Github-Changelog-Generator/wiki/Alternatives) that I found. But none satisfied my requirements.

*If you know other projects, feel free to edit this Wiki page!*


### Projects using this library
Here's a [wikipage list of projects](https://github.com/skywinder/Github-Changelog-Generator/wiki/Projects-using-Github-Changelog-Generator).

If you've used this project in a live app, please let me know! Nothing makes me happier than seeing someone else take my work and go wild with it.

*If you are using `github_changelog_generator` to generate your project's changelog, or know of other projects using it, please [add it to this list] (https://github.com/skywinder/Github-Changelog-Generator/wiki/Projects-using-Github-Changelog-Generator).*

## Am I missing some essential feature?

- **Nothing is impossible!**

- Open an [issue](https://github.com/skywinder/Github-Changelog-Generator/issues/new) and let's make the generator better together!

- *Bug reports, feature requests, patches, and well-wishes are always welcome.* :heavy_exclamation_mark:

## FAQ

- ***I already use GitHub Releases. Why do I need this?***

GitHub Releases is a very good thing. And it's very good practice to maintain it. (Not a lot of people are using it yet!) :congratulations:

*BTW: I would like to support GitHub Releases in [next releases](https://github.com/skywinder/github-changelog-generator/issues/56) ;)*

I'm not trying to compare the quality of handwritten and auto-generated logs. That said....

An auto-generated changelog really helps, even if you manually fill in the release notes!

For example:

When I saw a resolved bug, it's very useful to know on which release it's been fixed. 
In this case, you can easily find the issue by \# in `CHANGELOG.md`.

- it's not quite as easy to find this in handwritten releases notes
- a generated file saves you the trouble of remembering everything;
  sometimes people forget to add things to a handwritten file

Ultimately, I think GitHub Releases is ideal for end-users. 
Meanwhile, `CHANGELOG.md` lives right in the repository, with its detailed list of changes, which is handy for developers.
Finally, there's nothing wrong with using GitHub Releases alongside `CHANGELOG.md` in this combination.

- ***I received a warning: "GitHub API rate limit exceed"  What does this mean?***

GitHub [limits the number of API requests](https://developer.github.com/v3/#rate-limiting) you can make in an hour. You can make up to 5,000 requests per hour. For unauthenticated requests, the rate limit is only up to 60 requests per hour. Unauthenticated requests are associated with your IP address (not the user making requests).

If you're seeing this warning, please do the following:

1. Make sure you're providing an OAuth token, so you're not making requests anonymously. Using an OAuth token increases your hourly request maximum from 60 to 5000.
2. If you have a large repo with lots of issues/PRs, you can use `--max-issues NUM` to limit the number of issues that are pulled back. For example: `--max-issues 1000`

## Contributing

1. Create an issue and describe your idea
2. [Fork it] (https://github.com/skywinder/Github-Changelog-Generator/fork)
3. Create your feature branch (`git checkout -b my-new-feature`)
4. Commit your changes (`git commit -am 'Add some feature'`)
5. Publish the branch (`git push origin my-new-feature`)
6. Create a new Pull Request
7. Profit! :white_check_mark:

*To test your workflow with changelog generator, you can use [test repo](https://github.com/skywinder/changelog_test/)*

## License

Github Changelog Generator is released under the [MIT License](http://www.opensource.org/licenses/MIT).
