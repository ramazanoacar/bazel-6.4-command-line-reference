## Mobile-install Options

Inherits all options from [build](#build).

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

`--mode=<classic, classic_internal_test_do_not_use or skylark>` default: "classic"
:   Select how to run mobile-install. "classic" runs the current version of mobile-install. "skylark" uses the new Starlark version, which has support for android\_test.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

Options that configure the toolchain used for action execution:

`--adb=<a string>` default: ""
:   adb binary to use for the 'mobile-install' command. If unspecified, the one in the Android SDK specified by the --android\_sdk command line option (or the default SDK if --android\_sdk is not specified) is used.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Options that control the output of the command:

`--[no]incremental` default: "false"
:   Whether to do an incremental install. If true, try to avoid unnecessary additional work by reading the state of the device the code is to be installed on and using that information to avoid unnecessary work. If false (the default), always do a full install.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]split_apks` default: "false"
:   Whether to use split apks to install and update the application on the device. Works only with devices with Marshmallow or later
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

Options that let the user configure the intended output, affecting its value, as opposed to its existence:

`--adb_arg=<a string>` multiple uses are accumulated
:   Extra arguments to pass to adb. Usually used to designate a device to install to.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--debug_app`
:   Whether to wait for the debugger before starting the app.
      
    Expands to:  
      `--start=DEBUG`  
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--device=<a string>` default: ""
:   The adb device serial number. If not specified, the first device will be used.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--start=<no, cold, warm or debug>` default: "NO"
:   How the app should be started after installing it. Set to WARM to preserve and restore application state on incremental installs.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--start_app`
:   Whether to start the app after installing it.
      
    Expands to:  
      `--start=COLD`  
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

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

`--incremental_install_verbosity=<a string>` default: ""
:   The verbosity for incremental install. Set to 1 for debug logging.
      
    Tags:
    [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

Options specifying or altering a generic input to a Bazel command that does not fall into other categories.:

`--experimental_resolved_file_instead_of_workspace=<a string>` default: ""
:   If non-empty read the specified resolved file instead of the WORKSPACE file
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Remote caching and execution options:

`--experimental_downloader_config=<a string>` default: see description
:   Specify a file to configure the remote downloader with. This file consists of lines, each of which starts with a directive (`allow`, `block` or `rewrite`) followed by either a host name (for `allow` and `block`) or two patterns, one to match against, and one to use as a substitute URL, with back-references starting from `$1`. It is possible for multiple `rewrite` directives for the same URL to be give, and in this case multiple URLs will be returned.

Miscellaneous options, not otherwise categorized.:

`--override_repository=<an equals-separated mapping of repository name to path>` multiple uses are accumulated
:   Override a repository with a local path in the form of <repository name>=<path>. If the given path is an absolute path, it will be used as it is. If the given path is a relative path, it is relative to the current working directory. If the given path starts with '%workspace%, it is relative to the workspace root, which is the output of `bazel info workspace`
