<!-- This file was automatically generated by the `build-harness`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

[![Cloud Posse](https://cloudposse.com/logo-300x69.png)](https://cloudposse.com)

# copyright-header  [![Build Status](https://travis-ci.org/cloudposse/copyright-header.svg?branch=master)](https://travis-ci.org/cloudposse/copyright-header) [![Latest Release](https://img.shields.io/github/release/cloudposse/copyright-header.svg)](https://github.com/cloudposse/copyright-header/releases) [![Slack Community](https://slack.cloudposse.com/badge.svg)](https://slack.cloudposse.com)


Copyright Header is a utility to manipulate licenses on source code.

Features
--------

* Add/remove a copyright headers recursively on source files
* Customize the syntax configuration for how to write out comments
* Built-in support for GPL3 and MIT licenses
* Supports custom licenes with `--license-file` argument
* ERB template support

Caveats
-------
* Will only remove headers to files that have exactly the same header as the one we added
* Will only add headers to files which do not contain the case-sensitive pattern `/[Cc]opyright|[Lc]icense/` in the first `N` lines
* Will not properly format arguments that contain new-line ("`\n`") characters.

Requirements
------------

* Ruby 1.9.2 (supported version, might work with older rubies but not guaranteed)

Installation
------------

Install Copyright Header from RubyForge:

    gem install copyright-header


---

This project is part of our comprehensive ["SweetOps"](https://docs.cloudposse.com) approach towards DevOps. 


It's 100% Open Source and licensed under the [APACHE2](LICENSE).




## Usage

Full list of supported arguments:

    Usage: copyright-header options [file]
        -n, --dry-run                    Output the parsed files to STDOUT
        -o, --output-dir DIR             Use DIR as output directory
            --license-file FILE          Use FILE as header (instead of using --license argument)
            --license [AGPL3|ASL2|BSD-2-CLAUSE|BSD-3-CLAUSE|BSD-4-CLAUSE|GPL3|MIT]
                                         Use LICENSE as header
            --copyright-software NAME    The common name for this piece of software (e.g. "Copyright Header")
            --copyright-software-description DESC
                                         The detailed description for this piece of software (e.g. "A utility to manipulate copyright headers on source code files")
            --copyright-holder NAME      The legal owner of the copyright for the software. (e.g. "Erik Osterman <e@osterman.com>"). Repeat argument for multiple names.
            --copyright-year YEAR        The years for which the copyright exists (e.g. "2012-2017"). Repeat argument for multiple years.
        -w, --word-wrap LEN              Maximum number of characters per line for license (default: 80)
        -a, --add-path PATH              Recursively insert header in all files found in path (allows multiple paths separated by platform path-separator ":")
        -r, --remove-path PATH           Recursively remove header in all files found in path (allows multiple paths separated by platform path-separator ":")
        -g, --guess-extension            Use the GitHub Linguist gem to guess the extension of the source code when no extension can be determined (experimental).
        -c, --syntax FILE                Syntax configuration file
        -V, --version                    Display version information
        -h, --help                       Display this screen




## Examples

Discover available parameters by passing the `--help` argument

    copyright-header --help

Add a GPL3 License header to a file:

    copyright-header --add-path /tmp/test.rb \
                     --license GPL3 \
                     --copyright-holder 'Joe Shmoe' \
                     --copyright-software 'Example Software' \
                     --copyright-software-description "This is the description of the software." \
                     --copyright-year 2012-2017 \
                     --output-dir /tmp \
                     --dry-run

Remove the header created in the previous step (without --dry-run argument):

    copyright-header --remove-path /tmp/test.rb \
                     --license GPL3 \
                     --copyright-holder 'Joe Shmoe' \
                     --copyright-software 'Example Software' \
                     --copyright-software-description 'This is the description of the software.' \
                     --copyright-year 2012-2017 \
                     --output-dir /tmp \
                     --dry-run

Command used to generate copyright headers for this script:

    copyright-header  --license GPL3  \
                      --add-path lib/:bin/ \
                      --guess-extension \
                      --copyright-holder 'Erik Osterman <e@osterman.com>' \
                      --copyright-software 'Copyright Header' \
                      --copyright-software-description "A utility to manipulate copyright headers on source code files" \
                      --copyright-year 2012-2017 \
                      --word-wrap 100 \
                      --output-dir ./


Paths can be either files or directories. It will recursively traverse the directory tree ignoring all dot files.

You can specify an alternative syntax configuration file using the `--syntax` argument.

Rake
----

The above example can be performed as rake task inside a Rakefile:

    task :headers do
      require 'rubygems'
      require 'copyright_header'

      args = {
        :license => 'GPL3',
        :copyright_software => 'Copyright Header',
        :copyright_software_description => "A utility to manipulate copyright headers on source code files",
        :copyright_holders => ['Erik Osterman <e@osterman.com>'],
        :copyright_years => ['2012-2017'],
        :add_path => 'lib',
        :output_dir => '.'
      }

      command_line = CopyrightHeader::CommandLine.new( args )
      command_line.execute
    end

## Docker

```
docker run --rm --volume `pwd`:/usr/src/ osterman/copyright-header:latest \
  --license GPL3 \
  --add-path . \
  --guess-extension \
  --copyright-holder 'Erik Osteman <e@osterman.com>' \
  --copyright-software 'Copyright Header' \
  --copyright-software-description 'A utility to manipulate copyright headers on source code files' \
  --copyright-year 2012-2017 \
  --word-wrap 100 \
  --output-dir /usr/src/
```

## Make

Here is how we typically use it in our [`Makefile`](Makefile).

Check out the Cloud Posse [`build-harness`](https://github.com/cloudposse/build-harness/) for other neat tricks.



## Makefile Targets
```
Available targets:

  help                                This help screen
  help/all                            Display help for all targets
  lint                                Lint terraform code

```



## Help

**Got a question?**

File a GitHub [issue](https://github.com/cloudposse/copyright-header/issues), send us an [email][email] or join our [Slack Community][slack].

## Commerical Support

Work directly with our team of DevOps experts via email, slack, and video conferencing. 

We provide *commercial support* for all of our [Open Source][github] projects. As a *Dedicated Support* customer, you have access to our team of subject matter experts at a fraction of the cost of a fulltime engineer. 

- **Questions.** We'll use a Shared Slack channel between your team and ours.
- **Troubleshooting.** We'll help you triage why things aren't working.
- **Code Reviews.** We'll review your Pull Requests and provide constructive feedback.
- **Bug Fixes.** We'll rapidly work to fix any bugs in our projects.
- **Build New Terraform Modules.** We'll develop original modules to provision infrastructure.
- **Cloud Architecture.** We'll assist with your cloud strategy and design.
- **Implementation.** We'll provide hands on support to implement our reference architectures. 

## Community Forum

Get access to our [Open Source Community Forum][slack] on Slack. It's **FREE** to join for everyone! Our "SweetOps" community is where you get to talk with others who share a similar vision for how to rollout and manage infrastructure. This is the best place to talk shop, ask questions, solicit feedback, and work together as a community to build *sweet* infrastructure.

## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/cloudposse/copyright-header/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing this project or [help out](https://github.com/orgs/cloudposse/projects/3) with our other projects, we would love to hear from you! Shoot us an [email](mailto:hello@cloudposse.com).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!

## Copyright

Copyright © 2017-2018 [Cloud Posse, LLC](https://cloudposse.com)


## License 

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) 

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.


## Trademarks

All other trademarks referenced herein are the property of their respective owners.

## About

This project is maintained and funded by [Cloud Posse, LLC][website]. Like it? Please let us know at <hello@cloudposse.com>

[![Cloud Posse](https://cloudposse.com/logo-300x69.png)](https://cloudposse.com)

We're a [DevOps Professional Services][hire] company based in Los Angeles, CA. We love [Open Source Software](https://github.com/cloudposse/)!

We offer paid support on all of our projects.  

Check out [our other projects][github], [apply for a job][jobs], or [hire us][hire] to help with your cloud strategy and implementation.

  [docs]: https://docs.cloudposse.com/
  [website]: https://cloudposse.com/
  [github]: https://github.com/cloudposse/
  [jobs]: https://cloudposse.com/jobs/
  [hire]: https://cloudposse.com/contact/
  [slack]: https://slack.cloudposse.com/
  [linkedin]: https://www.linkedin.com/company/cloudposse
  [twitter]: https://twitter.com/cloudposse/
  [email]: mailto:hello@cloudposse.com


### Contributors

|  [![Erik Osterman][osterman_avatar]](osterman_homepage)<br/>[Erik Osterman][osterman_homepage] | [![Leo O'Donnell][leopoldodonnell_avatar]](leopoldodonnell_homepage)<br/>[Leo O'Donnell][leopoldodonnell_homepage] | [![Christian Meier][mkristian_avatar]](mkristian_homepage)<br/>[Christian Meier][mkristian_homepage] | [![Gabriel de Perthuis][g2p_avatar]](g2p_homepage)<br/>[Gabriel de Perthuis][g2p_homepage] | [![Thomas Russell Murphy][thomasrussellmurphy_avatar]](thomasrussellmurphy_homepage)<br/>[Thomas Russell Murphy][thomasrussellmurphy_homepage] | [![Kongqun Yang][kqyang_avatar]](kqyang_homepage)<br/>[Kongqun Yang][kqyang_homepage] | [![Vincent Billey][Fenntasy_avatar]](Fenntasy_homepage)<br/>[Vincent Billey][Fenntasy_homepage] | [![arximboldi][arximboldi_avatar]](arximboldi_homepage)<br/>[arximboldi][arximboldi_homepage] | [![David][TAGC_avatar]](TAGC_homepage)<br/>[David][TAGC_homepage] | [![Rafał Rzepecki][dividedmind_avatar]](dividedmind_homepage)<br/>[Rafał Rzepecki][dividedmind_homepage] | [![David Yip][yipdw_avatar]](yipdw_homepage)<br/>[David Yip][yipdw_homepage] | [![Daniel Freedman][azakus_avatar]](azakus_homepage)<br/>[Daniel Freedman][azakus_homepage] | [![Mitch Souders][crzysdrs_avatar]](crzysdrs_homepage)<br/>[Mitch Souders][crzysdrs_homepage] | [![Mads Bondo Dydensborg][mbd-dbc-dk_avatar]](mbd-dbc-dk_homepage)<br/>[Mads Bondo Dydensborg][mbd-dbc-dk_homepage] | [![Psy-Q][psy-q_avatar]](psy-q_homepage)<br/>[Psy-Q][psy-q_homepage] | [![Bryan][bstopp_avatar]](bstopp_homepage)<br/>[Bryan][bstopp_homepage] | [![Colin Dean][colindean_avatar]](colindean_homepage)<br/>[Colin Dean][colindean_homepage] | [![Wahaj Shamim][wshamim_avatar]](wshamim_homepage)<br/>[Wahaj Shamim][wshamim_homepage] | [![halo][halo_avatar]](halo_homepage)<br/>[halo][halo_homepage] | [![Lloyd Dewolf][lloydde_avatar]](lloydde_homepage)<br/>[Lloyd Dewolf][lloydde_homepage] |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

  [osterman_homepage]: https://github.com/osterman
  [osterman_avatar]: http://s.gravatar.com/avatar/88c480d4f73b813904e00a5695a454cb?s=144
  [leopoldodonnell_homepage]: https://github.com/leopoldodonnell
  [leopoldodonnell_avatar]: https://avatars1.githubusercontent.com/u/135395?s=460&v=4
  [mkristian_homepage]: https://github.com/mkristian
  [mkristian_avatar]: https://avatars3.githubusercontent.com/u/35058?s=460&v=4
  [g2p_homepage]: https://github.com/g2p
  [g2p_avatar]: https://avatars1.githubusercontent.com/u/61678?s=460&v=4
  [thomasrussellmurphy_homepage]: https://github.com/thomasrussellmurphy
  [thomasrussellmurphy_avatar]: https://avatars2.githubusercontent.com/u/2342884?s=460&v=4
  [kqyang_homepage]: https://github.com/kqyang
  [kqyang_avatar]: https://avatars1.githubusercontent.com/u/7329892?s=460&v=4
  [Fenntasy_homepage]: https://github.com/Fenntasy
  [Fenntasy_avatar]: https://avatars0.githubusercontent.com/u/1764664?s=460&v=4
  [arximboldi_homepage]: https://github.com/arximboldi
  [arximboldi_avatar]: https://avatars2.githubusercontent.com/u/4521138?s=460&v=4
  [TAGC_homepage]: https://github.com/TAGC
  [TAGC_avatar]: https://avatars0.githubusercontent.com/u/1588951?s=460&v=4
  [dividedmind_homepage]: https://github.com/dividedmind
  [dividedmind_avatar]: https://avatars2.githubusercontent.com/u/823636?s=460&v=4
  [yipdw_homepage]: https://github.com/yipdw
  [yipdw_avatar]: https://avatars3.githubusercontent.com/u/3859?s=460&v=4
  [azakus_homepage]: https://github.com/azakus
  [azakus_avatar]: https://avatars2.githubusercontent.com/u/46725?s=460&v=4
  [crzysdrs_homepage]: https://github.com/crzysdrs
  [crzysdrs_avatar]: https://avatars2.githubusercontent.com/u/3467368?s=460&v=4
  [mbd-dbc-dk_homepage]: https://github.com/mbd-dbc-dk
  [mbd-dbc-dk_avatar]: https://avatars3.githubusercontent.com/u/1001078?s=460&v=4
  [psy-q_homepage]: https://github.com/psy-q
  [psy-q_avatar]: https://avatars1.githubusercontent.com/u/87557?s=460&v=4
  [bstopp_homepage]: https://github.com/bstopp
  [bstopp_avatar]: https://avatars3.githubusercontent.com/u/6520270?s=460&v=4
  [colindean_homepage]: https://github.com/colindean
  [colindean_avatar]: https://avatars1.githubusercontent.com/u/197224?s=460&v=4
  [wshamim_homepage]: https://github.com/wshamim
  [wshamim_avatar]: https://avatars0.githubusercontent.com/u/12794050?s=460&v=4
  [halo_homepage]: https://github.com/halo
  [halo_avatar]: https://avatars1.githubusercontent.com/u/11441?s=460&v=4
  [lloydde_homepage]: https://github.com/lloydde
  [lloydde_avatar]: https://avatars3.githubusercontent.com/u/962387?s=460&v=4


