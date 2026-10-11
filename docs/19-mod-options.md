## Mod Options

Options that appear before the command and are parsed by the client:

`--distdir=<a path>` multiple uses are accumulated
:   Additional places to search for archives before accessing the network to download them.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--[no]experimental_repository_cache_hardlinks` default: "false"
:   If set, the repository cache will hardlink the file in case of a cache hit, rather than copying. This is intended to save disk space.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--[no]experimental_repository_cache_urls_as_default_canonical_id` default: "false"
:   If true, use a string derived from the URLs of repository downloads as the canonical\_id if not specified. This causes a change in the URLs to result in a redownload even if the cache contains a download with the same hash. This can be used to verify that URL changes don't result in broken repositories being masked by the cache.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_repository_disable_download` default: "false"
:   If set, downloading external repositories is not allowed.
      
    Tags:
    [`experimental`](#metadata_tag_EXPERIMENTAL)

`--experimental_repository_downloader_retries=<an integer>` default: "0"
:   The maximum number of attempts to retry a download error. If set to 0, retries are disabled.
      
    Tags:
    [`experimental`](#metadata_tag_EXPERIMENTAL)

`--experimental_scale_timeouts=<a double>` default: "1.0"
:   Scale all timeouts in Starlark repository rules by this factor. In this way, external repositories can be made working on machines that are slower than the rule author expected, without changing the source code
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--http_timeout_scaling=<a double>` default: "1.0"
:   Scale all timeouts related to http downloads by the given factor
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--repository_cache=<a path>` default: see description
:   Specifies the cache location of the downloaded values obtained during the fetching of external repositories. An empty string as argument requests the cache to be disabled.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

Options that control build execution:

`--[no]keep_going` [`-k`] default: "false"
:   Continue as much as possible after an error. While the target that failed and those that depend on it cannot be analyzed, other prerequisites of these targets can be.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--loading_phase_threads=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` default: "auto"
:   Number of parallel threads to use for the loading/analysis phase.Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". "auto" sets a reasonable default based on host resources. Must be at least 1.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

Options that affect how strictly Bazel enforces valid build inputs (rule definitions, flag combinations, etc.):

`--experimental_repository_hash_file=<a string>` default: ""
:   If non-empty, specifies a file containing a resolved value, against which the repository directory hashes should be verified
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--experimental_verify_repository_rules=<a string>` multiple uses are accumulated
:   If list of repository rules for which the hash of the output directory should be verified, provided a file is specified by --experimental\_repository\_hash\_file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

This option affects semantics of the Starlark language or the build API accessible to BUILD files, .bzl files, or WORKSPACE files.:

`--[no]experimental_allow_top_level_aspects_parameters` default: "true"
:   No-op
      
    Tags:
    [`no_op`](#effect_tag_NO_OP), [`deprecated`](#metadata_tag_DEPRECATED), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]incompatible_config_setting_private_default_visibility` default: "false"
:   If incompatible\_enforce\_config\_setting\_visibility=false, this is a noop. Else, if this flag is false, any config\_setting without an explicit visibility attribute is //visibility:public. If this flag is true, config\_setting follows the same visibility logic as all other rules. See https://github.com/bazelbuild/bazel/issues/12933.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_enforce_config_setting_visibility` default: "true"
:   If true, enforce config\_setting visibility restrictions. If false, every config\_setting is visible to every target. See https://github.com/bazelbuild/bazel/issues/12932.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

Options relating to the output and semantics of the `mod` subcommand:

`--base_module=<"<root>" for the root module; <module>@<version> for a specific version of a module; <module> for all versions of a module; @<name> for a repo with the given apparent name; or @@<name> for a repo with the given canonical name>` default: "<root>"
:   Specify a module relative to which the specified target repos will be interpreted.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--charset=<utf8 or ascii>` default: "utf8"
:   Chooses the character set to use for the tree. Only affects text output. Valid values are "utf8" or "ascii". Default is "utf8"
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]cycles` default: "false"
:   Points out dependency cycles inside the displayed tree, which are normally ignored by default.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--depth=<an integer>` default: "-1"
:   Maximum display depth of the dependency tree. A depth of 1 displays the direct dependencies, for example. For tree, path and all\_paths it defaults to Integer.MAX\_VALUE, while for deps and explain it defaults to 1 (only displays direct deps of the root besides the target leaves and their parents).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--extension_filter=<a comma-separated list of <extension>s>` default: see description
:   Only display the usages of these module extensions and the repos generated by them if their respective flags are set. If set, the result graph will only include paths that contain modules using the specified extensions. An empty list disables the filter, effectively specifying all possible extensions.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--extension_info=<hidden, usages, repos or all>` default: "hidden"
:   Specify how much detail about extension usages to include in the query result. "Usages" will only show the extensions names, "repos" will also include repos imported with use\_repo, and "all" will also show the other repositories generated by extensions.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--extension_usages=<a comma-separated list of <module>s>` default: ""
:   Specify modules whose extension usages will be displayed in the show\_extension query.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--from=<a comma-separated list of <module>s>` default: "<root>"
:   The module(s) starting from which the dependency graph query will be displayed. Check each query’s description for the exact semantics. Defaults to <root>.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_builtin` default: "false"
:   Include built-in modules in the dependency graph. Disabled by default because it is quite noisy.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_unused` default: "false"
:   The queries will also take into account and display the unused modules, which are not present in the module resolution graph after selection (due to the Minimal-Version Selection or override rules). This can have different effects for each of the query types i.e. include new paths in the all\_paths command, or extra dependants in the explain command.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--output=<text, json or graph>` default: "text"
:   The format in which the query results should be printed. Allowed values for query are: text, json, graph
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]verbose` default: "false"
:   The queries will also display the reason why modules were resolved to their current version (if changed). Defaults to true only for the explain query.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

Options relating to Bzlmod output and semantics:

`--allow_yanked_versions=<a string>` multiple uses are accumulated
:   Specified the module versions in the form of `<module1>@<version1>,<module2>@<version2>` that will be allowed in the resolved dependency graph even if they are declared yanked in the registry where they come from (if they are not coming from a NonRegistryOverride). Otherwise, yanked versions will cause the resolution to fail. You can also define allowed yanked version with the `BZLMOD\_ALLOW\_YANKED\_VERSIONS` environment variable. You can disable this check by using the keyword 'all' (not recommended).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--check_bazel_compatibility=<error, warning or off>` default: "error"
:   Check bazel version compatibility of Bazel modules. Valid values are `error` to escalate it to a resolution failure, `off` to disable the check, or `warning` to print a warning when mismatch detected.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--check_direct_dependencies=<off, warning or error>` default: "warning"
:   Check if the direct `bazel\_dep` dependencies declared in the root module are the same versions you get in the resolved dependency graph. Valid values are `off` to disable the check, `warning` to print a warning when mismatch detected or `error` to escalate it to a resolution failure.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]ignore_dev_dependency` default: "false"
:   If true, Bazel ignores `bazel\_dep` and `use\_extension` declared as `dev\_dependency` in the MODULE.bazel of the root module. Note that, those dev dependencies are always ignored in the MODULE.bazel if it's not the root module regardless of the value of this flag.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--lockfile_mode=<off, update or error>` default: "off"
:   Specifies how and whether or not to use the lockfile. Valid values are `update` to use the lockfile and update it if there are changes, `error` to use the lockfile but throw an error if it's not up-to-date, or `off` to neither read from or write to the lockfile.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--override_module=<an equals-separated mapping of module name to path>` multiple uses are accumulated
:   Override a module with a local path in the form of <module name>=<path>. If the given path is an absolute path, it will be used as it is. If the given path is a relative path, it is relative to the current working directory. If the given path starts with '%workspace%, it is relative to the workspace root, which is the output of `bazel info workspace`

`--registry=<a string>` multiple uses are accumulated
:   Specifies the registries to use to locate Bazel module dependencies. The order is important: modules will be looked up in earlier registries first, and only fall back to later registries when they're missing from the earlier ones.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Options that affect the verbosity, format or location of logging:

`--[no]experimental_record_metrics_for_all_mnemonics` default: "false"
:   By default the number of action types is limited to the 20 mnemonics with the largest number of executed actions. Setting this option will write statistics for all mnemonics.

Options specifying or altering a generic input to a Bazel command that does not fall into other categories.:

`--experimental_resolved_file_instead_of_workspace=<a string>` default: ""
:   If non-empty read the specified resolved file instead of the WORKSPACE file
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Remote caching and execution options:

`--experimental_downloader_config=<a string>` default: see description
:   Specify a file to configure the remote downloader with. This file consists of lines, each of which starts with a directive (`allow`, `block` or `rewrite`) followed by either a host name (for `allow` and `block`) or two patterns, one to match against, and one to use as a substitute URL, with back-references starting from `$1`. It is possible for multiple `rewrite` directives for the same URL to be give, and in this case multiple URLs will be returned.

Miscellaneous options, not otherwise categorized.:

`--deleted_packages=<comma-separated list of package names>` default: ""
:   A comma-separated list of names of packages which the build system will consider non-existent, even if they are visible somewhere on the package path.
    Use this option when deleting a subpackage 'x/y' of an existing package 'x'. For example, after deleting x/y/BUILD in your client, the build system may complain if it encounters a label '//x:y/z' if that is still provided by another package\_path entry. Specifying --deleted\_packages x/y avoids this problem.

`--override_repository=<an equals-separated mapping of repository name to path>` multiple uses are accumulated
:   Override a repository with a local path in the form of <repository name>=<path>. If the given path is an absolute path, it will be used as it is. If the given path is a relative path, it is relative to the current working directory. If the given path starts with '%workspace%, it is relative to the workspace root, which is the output of `bazel info workspace`

`--package_path=<colon-separated list of options>` default: "%workspace%"
:   A colon-separated list of where to look for packages. Elements beginning with '%workspace%' are relative to the enclosing workspace. If omitted or empty, the default is the output of 'bazel info default-package-path'.

`--[no]show_loading_progress` default: "true"
:   If enabled, causes Bazel to print "Loading package:" messages.
