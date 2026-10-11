## Aquery Options

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

Options relating to query output and semantics:

`--aspect_deps=<off, conservative or precise>` default: "conservative"
:   How to resolve aspect dependencies when the output format is one of {xml,proto,record}. 'off' means no aspect dependencies are resolved, 'conservative' (the default) means all declared aspect dependencies are added regardless of whether they are given the rule class of direct dependencies, 'precise' means that only those aspects are added that are possibly active given the rule class of the direct dependencies. Note that precise mode requires loading other packages to evaluate a single target thus making it slower than the other modes. Also note that even precise mode is not completely precise: the decision whether to compute an aspect is decided in the analysis phase, which is not run during 'bazel query'.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]consistent_labels` default: "false"
:   If enabled, every query command emits labels as if by the Starlark <code>str</code> function applied to a <code>Label</code> instance. This is useful for tools that need to match the output of different query commands and/or labels emitted by rules. If not enabled, output formatters are free to emit apparent repository names (relative to the main repository) instead to make the output more readable.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]deduplicate_depsets` default: "true"
:   De-duplicate non-leaf children of a dep\_set\_of\_files in the final proto/textproto/json output. This does not deduplicate depsets that don't share an immediate parent. This does not affect the final effective list of input artifacts of the actions.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]graph:factored` default: "true"
:   If true, then the graph will be emitted 'factored', i.e. topologically-equivalent nodes will be merged together and their labels concatenated. This option is only applicable to --output=graph.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--graph:node_limit=<an integer>` default: "512"
:   The maximum length of the label string for a graph node in the output. Longer labels will be truncated; -1 means no truncation. This option is only applicable to --output=graph.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]implicit_deps` default: "true"
:   If enabled, implicit dependencies will be included in the dependency graph over which the query operates. An implicit dependency is one that is not explicitly specified in the BUILD file but added by bazel. For cquery, this option controls filtering resolved toolchains.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]include_artifacts` default: "true"
:   Includes names of the action inputs and outputs in the output (potentially large).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_aspects` default: "true"
:   aquery, cquery: whether to include aspect-generated actions in the output. query: no-op (aspects are always followed).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_commandline` default: "true"
:   Includes the content of the action command lines in the output (potentially large).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_file_write_contents` default: "false"
:   Include the file contents for the FileWrite and SourceSymlinkManifest actions (potentially large).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_param_files` default: "false"
:   Include the content of the param files used in the command (potentially large). Note: Enabling this flag will automatically enable the --include\_commandline flag.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]incompatible_display_source_file_location` default: "true"
:   True by default, displays the target of the source file. If true, displays the location of line 1 of source files in location outputs. This flag only exists for migration purposes.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_package_group_includes_double_slash` default: "true"
:   If enabled, when outputting package\_group's `packages` attribute, the leading `//` will not be omitted.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]infer_universe_scope` default: "false"
:   If set and --universe\_scope is unset, then a value of --universe\_scope will be inferred as the list of unique target patterns in the query expression. Note that the --universe\_scope value inferred for a query expression that uses universe-scoped functions (e.g.`allrdeps`) may not be what you want, so you should use this option only if you know what you are doing. See https://bazel.build/reference/query#sky-query for details and examples. If --universe\_scope is set, then this option's value is ignored. Note: this option applies only to `query` (i.e. not `cquery`).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]line_terminator_null` default: "false"
:   Whether each format is terminated with \0 instead of newline.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]nodep_deps` default: "true"
:   If enabled, deps from "nodep" attributes will be included in the dependency graph over which the query operates. A common example of a "nodep" attribute is "visibility". Run and parse the output of `info build-language` to learn about all the "nodep" attributes in the build language.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--output=<a string>` default: "text"
:   The format in which the aquery results should be printed. Allowed values for aquery are: text, textproto, proto, jsonproto.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:default_values` default: "true"
:   If true, attributes whose value is not explicitly specified in the BUILD file are included; otherwise they are omitted. This option is applicable to --output=proto
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:definition_stack` default: "false"
:   Populate the definition\_stack proto field, which records for each rule instance the Starlark call stack at the moment the rule's class was defined.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:flatten_selects` default: "true"
:   If enabled, configurable attributes created by select() are flattened. For list types the flattened representation is a list containing each value of the select map exactly once. Scalar types are flattened to null.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]proto:include_synthetic_attribute_hash` default: "false"
:   Whether or not to calculate and populate the $internal\_attr\_hash attribute.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:instantiation_stack` default: "false"
:   Populate the instantiation call stack of each rule. Note that this requires the stack to be present
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:locations` default: "true"
:   Whether to output location information in proto output at all.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--proto:output_rule_attrs=<comma-separated list of options>` default: "all"
:   Comma separated list of attributes to include in output. Defaults to all attributes. Set to empty string to not output any attribute. This option is applicable to --output=proto.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:rule_inputs_and_outputs` default: "true"
:   Whether or not to populate the rule\_input and rule\_output fields.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--query_file=<a string>` default: ""
:   If set, query will read the query from the file named here, rather than on the command line. It is an error to specify a file here as well as a command-line query.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]relative_locations` default: "false"
:   If true, the location of BUILD files in xml and proto outputs will be relative. By default, the location output is an absolute path and will not be consistent across machines. You can set this option to true to have a consistent result across machines.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]skyframe_state` default: "false"
:   Without performing extra analysis, dump the current Action Graph from Skyframe. Note: Specifying a target with --skyframe\_state is currently not supported. This flag is only available with --output=proto or --output=textproto.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]tool_deps` default: "true"
:   Query: If disabled, dependencies on 'host configuration' or 'execution' targets will not be included in the dependency graph over which the query operates. A 'host configuration' dependency edge, such as the one from any 'proto\_library' rule to the Protocol Compiler, usually points to a tool executed during the build rather than a part of the same 'target' program.
    Cquery: If disabled, filters out all configured targets which cross a host or execution transition from the top-level target that discovered this configured target. That means if the top-level target is in the target configuration, only configured targets also in the target configuration will be returned. If the top-level target is in the host configuration, only host configured targets will be returned. This option will NOT exclude resolved toolchains.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--universe_scope=<comma-separated list of options>` default: ""
:   A comma-separated set of target patterns (additive and subtractive). The query may be performed in the universe defined by the transitive closure of the specified targets. This option is used for the query and cquery commands.
    For cquery, the input to this option is the targets all answers are built under and so this option may affect configurations and transitions. If this option is not specified, the top-level targets are assumed to be the targets parsed from the query expression. Note: For cquery, not specifying this option may cause the build to break if targets parsed from the query expression are not buildable with top-level options.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

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

`--override_repository=<an equals-separated mapping of repository name to path>` multiple uses are accumulated
:   Override a repository with a local path in the form of <repository name>=<path>. If the given path is an absolute path, it will be used as it is. If the given path is a relative path, it is relative to the current working directory. If the given path starts with '%workspace%, it is relative to the workspace root, which is the output of `bazel info workspace`

Options that control build execution:

`--[no]experimental_inprocess_symlink_creation` default: "false"
:   Whether to make direct file system calls to create symlink trees
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_remotable_source_manifests` default: "false"
:   Whether to make source manifest actions remotable
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_split_coverage_postprocessing` default: "false"
:   If true, then Bazel will run coverage postprocessing for test in a new spawn.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_strict_fileset_output` default: "false"
:   If this option is enabled, filesets will treat all output artifacts as regular files. They will not traverse directories or be sensitive to symlinks.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--modify_execution_info=<regex=[+-]key,regex=[+-]key,...>` default: ""
:   Add or remove keys from an action's execution info based on action mnemonic. Applies only to actions which support execution info. Many common actions support execution info, e.g. Genrule, CppCompile, Javac, StarlarkAction, TestRunner. When specifying multiple values, order matters because many regexes may apply to the same mnemonic.
    Syntax: "regex=[+-]key,regex=[+-]key,...".
    Examples:
    '.\*=+x,.\*=-y,.\*=+z' adds 'x' and 'z' to, and removes 'y' from, the execution info for all actions.
    'Genrule=+requires-x' adds 'requires-x' to the execution info for all Genrule actions.
    '(?!Genrule).\*=-requires-x' removes 'requires-x' from the execution info for all non-Genrule actions.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--persistent_android_dex_desugar`
:   Enable persistent Android dex and desugar actions by using workers.
      
    Expands to:  
      `--internal_persistent_android_dex_desugar`  
      `--strategy=Desugar=worker`  
      `--strategy=DexBuilder=worker`  
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--persistent_android_resource_processor`
:   Enable persistent Android resource processor by using workers.
      
    Expands to:  
      `--internal_persistent_busybox_tools`  
      `--strategy=AaptPackage=worker`  
      `--strategy=AndroidResourceParser=worker`  
      `--strategy=AndroidResourceValidator=worker`  
      `--strategy=AndroidResourceCompiler=worker`  
      `--strategy=RClassGenerator=worker`  
      `--strategy=AndroidResourceLink=worker`  
      `--strategy=AndroidAapt2=worker`  
      `--strategy=AndroidAssetMerger=worker`  
      `--strategy=AndroidResourceMerger=worker`  
      `--strategy=AndroidCompiledResourceMerger=worker`  
      `--strategy=ManifestMerger=worker`  
      `--strategy=AndroidManifestMerger=worker`  
      `--strategy=Aapt2Optimize=worker`  
      `--strategy=AARGenerator=worker`  
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--persistent_multiplex_android_dex_desugar`
:   Enable persistent multiplexed Android dex and desugar actions by using workers.
      
    Expands to:  
      `--persistent_android_dex_desugar`  
      `--internal_persistent_multiplex_android_dex_desugar`  
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--persistent_multiplex_android_resource_processor`
:   Enable persistent multiplexed Android resource processor by using workers.
      
    Expands to:  
      `--persistent_android_resource_processor`  
      `--modify_execution_info=AaptPackage=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidResourceParser=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidResourceValidator=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidResourceCompiler=+supports-multiplex-workers`  
      `--modify_execution_info=RClassGenerator=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidResourceLink=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidAapt2=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidAssetMerger=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidResourceMerger=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidCompiledResourceMerger=+supports-multiplex-workers`  
      `--modify_execution_info=ManifestMerger=+supports-multiplex-workers`  
      `--modify_execution_info=AndroidManifestMerger=+supports-multiplex-workers`  
      `--modify_execution_info=Aapt2Optimize=+supports-multiplex-workers`  
      `--modify_execution_info=AARGenerator=+supports-multiplex-workers`  
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--persistent_multiplex_android_tools`
:   Enable persistent and multiplexed Android tools (dexing, desugaring, resource processing).
      
    Expands to:  
      `--internal_persistent_multiplex_busybox_tools`  
      `--persistent_multiplex_android_resource_processor`  
      `--persistent_multiplex_android_dex_desugar`  
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

Options that configure the toolchain used for action execution:

`--android_compiler=<a string>` default: see description
:   The Android target compiler.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--android_crosstool_top=<a build target label>` default: "//external:android/crosstool"
:   The location of the C++ compiler used for Android builds.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--android_grte_top=<a label>` default: see description
:   The Android target grte\_top.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--android_manifest_merger=<legacy, android or force_android>` default: "android"
:   Selects the manifest merger to use for android\_binary rules. Flag to help thetransition to the Android manifest merger from the legacy merger.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--android_platforms=<a build target label>` default: ""
:   Sets the platforms that android\_binary targets use. If multiple platforms are specified, then the binary is a fat APKs, which contains native binaries for each specified target platform.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--android_sdk=<a build target label>` default: "@bazel\_tools//tools/android:sdk"
:   Specifies Android SDK/platform that is used to build Android applications.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--apple_compiler=<a string>` default: see description
:   The Apple target compiler. Useful for selecting variants of a toolchain (e.g. xcode-beta).
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--apple_crosstool_top=<a build target label>` default: "@bazel\_tools//tools/cpp:toolchain"
:   The label of the crosstool package to be used in Apple and Objc rules and their dependencies.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--apple_grte_top=<a build target label>` default: see description
:   The Apple target grte\_top.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--cc_output_directory_tag=<a string>` default: ""
:   Specifies a suffix to be added to the configuration directory.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`explicit_in_output_path`](#metadata_tag_EXPLICIT_IN_OUTPUT_PATH)

`--compiler=<a string>` default: see description
:   The C++ compiler to use for compiling the target.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION)

`--coverage_output_generator=<a build target label>` default: "@bazel\_tools//tools/test:lcov\_merger"
:   Location of the binary that is used to postprocess raw coverage reports. This must currently be a filegroup that contains a single file, the binary. Defaults to '//tools/test:lcov\_merger'.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--coverage_report_generator=<a build target label>` default: "@bazel\_tools//tools/test:coverage\_report\_generator"
:   Location of the binary that is used to generate coverage reports. This must currently be a filegroup that contains a single file, the binary. Defaults to '//tools/test:coverage\_report\_generator'.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--coverage_support=<a build target label>` default: "@bazel\_tools//tools/test:coverage\_support"
:   Location of support files that are required on the inputs of every test action that collects code coverage. Defaults to '//tools/test:coverage\_support'.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--crosstool_top=<a build target label>` default: "@bazel\_tools//tools/cpp:toolchain"
:   The label of the crosstool package to be used for compiling C++ code.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--custom_malloc=<a build target label>` default: see description
:   Specifies a custom malloc implementation. This setting overrides malloc attributes in build rules.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_add_exec_constraints_to_targets=<a '<RegexFilter>=<label1>[,<label2>,...]' assignment>` multiple uses are accumulated
:   List of comma-separated regular expressions, each optionally prefixed by - (negative expression), assigned (=) to a list of comma-separated constraint value targets. If a target matches no negative expression and at least one positive expression its toolchain resolution will be performed as if it had declared the constraint values as execution constraints. Example: //demo,-test=@platforms//cpus:x86\_64 will add 'x86\_64' to any target under //demo except for those whose name contains 'test'.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_enable_objc_cc_deps` default: "true"
:   Allows objc\_\* rules to depend on cc\_library and causes any objc dependencies to be built with --cpu set to "ios\_<--ios\_cpu>" for any values in --ios\_multi\_cpu.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]experimental_include_xcode_execution_requirements` default: "false"
:   If set, add a "requires-xcode:{version}" execution requirement to every Xcode action. If the xcode version has a hyphenated label, also add a "requires-xcode-label:{version\_label}" execution requirement.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_prefer_mutual_xcode` default: "true"
:   If true, use the most recent Xcode that is available both locally and remotely. If false, or if there are no mutual available versions, use the local Xcode version selected via xcode-select.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--extra_execution_platforms=<comma-separated list of options>` multiple uses are accumulated
:   The platforms that are available as execution platforms to run actions. Platforms can be specified by exact target, or as a target pattern. These platforms will be considered before those declared in the WORKSPACE file by register\_execution\_platforms().
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--extra_toolchains=<comma-separated list of options>` multiple uses are accumulated
:   The toolchain rules to be considered during toolchain resolution. Toolchains can be specified by exact target, or as a target pattern. These toolchains will be considered before those declared in the WORKSPACE file by register\_toolchains().
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--grte_top=<a label>` default: see description
:   A label to a checked-in libc library. The default value is selected by the crosstool toolchain, and you almost never need to override it.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_compiler=<a string>` default: see description
:   The C++ compiler to use for host compilation. It is ignored if --host\_crosstool\_top is not set.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION)

`--host_crosstool_top=<a build target label>` default: see description
:   By default, the --crosstool\_top and --compiler options are also used for the host configuration. If this flag is provided, Bazel uses the default libc and compiler for the given crosstool\_top.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_grte_top=<a label>` default: see description
:   If specified, this setting overrides the libc top-level directory (--grte\_top) for the host configuration.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_platform=<a build target label>` default: ""
:   The label of a platform rule that describes the host system.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]incompatible_disable_expand_if_all_available_in_flag_set` default: "true"
:   If true, Bazel will not allow specifying expand\_if\_all\_available in flag\_sets(see https://github.com/bazelbuild/bazel/issues/7008 for migration instructions).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_dont_enable_host_nonhost_crosstool_features` default: "true"
:   If true, Bazel will not enable 'host' and 'nonhost' features in the c++ toolchain (see https://github.com/bazelbuild/bazel/issues/7407 for more information).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_enable_android_toolchain_resolution` default: "false"
:   Use toolchain resolution to select the Android SDK for android rules (Starlark and native)
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_enable_apple_toolchain_resolution` default: "false"
:   Use toolchain resolution to select the Apple SDK for apple rules (Starlark and native)
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_make_thinlto_command_lines_standalone` default: "true"
:   If true, Bazel will not reuse C++ link action command lines for lto indexing command lines (see https://github.com/bazelbuild/bazel/issues/6791 for more information).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remove_cpu_and_compiler_attributes_from_cc_toolchain` default: "true"
:   If true, Bazel will complain when cc\_toolchain.cpu and cc\_toolchain.compiler attributes are set (see https://github.com/bazelbuild/bazel/issues/7075 for migration instructions).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remove_legacy_whole_archive` default: "true"
:   If true, Bazel will not link library dependencies as whole archive by default (see https://github.com/bazelbuild/bazel/issues/7362 for migration instructions).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_require_ctx_in_configure_features` default: "true"
:   If true, Bazel will require 'ctx' parameter in to cc\_common.configure\_features (see https://github.com/bazelbuild/bazel/issues/7793 for more information).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]interface_shared_objects` default: "true"
:   Use interface shared objects if supported by the toolchain. All ELF toolchains currently support this setting.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--ios_sdk_version=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Specifies the version of the iOS SDK to use to build iOS applications. If unspecified, uses default iOS SDK version from 'xcode\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--macos_sdk_version=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Specifies the version of the macOS SDK to use to build macOS applications. If unspecified, uses default macOS SDK version from 'xcode\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--minimum_os_version=<a string>` default: see description
:   The minimum OS version which your compilation targets.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--platform_mappings=<a relative path>` default: ""
:   The location of a mapping file that describes which platform to use if none is set or which flags to set when a platform already exists. Must be relative to the main workspace root. Defaults to 'platform\_mappings' (a file directly under the workspace root).
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--platforms=<a build target label>` default: ""
:   The labels of the platform rules describing the target platforms for the current command.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--python2_path=<a string>` default: see description
:   Deprecated, no-op. Disabled by `--incompatible\_use\_python\_toolchains`.
      
    Tags:
    [`no_op`](#effect_tag_NO_OP), [`deprecated`](#metadata_tag_DEPRECATED)

`--python3_path=<a string>` default: see description
:   Deprecated, no-op. Disabled by `--incompatible\_use\_python\_toolchains`.
      
    Tags:
    [`no_op`](#effect_tag_NO_OP), [`deprecated`](#metadata_tag_DEPRECATED)

`--python_path=<a string>` default: see description
:   The absolute path of the Python interpreter invoked to run Python targets on the target platform. Deprecated; disabled by --incompatible\_use\_python\_toolchains.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--python_top=<a build target label>` default: see description
:   The label of a py\_runtime representing the Python interpreter invoked to run Python targets on the target platform. Deprecated; disabled by --incompatible\_use\_python\_toolchains.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--target_platform_fallback=<a build target label>` default: "@local\_config\_platform//:host"
:   The label of a platform rule that should be used if no target platform is set and no platform mapping matches the current set of flags.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--tvos_sdk_version=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Specifies the version of the tvOS SDK to use to build tvOS applications. If unspecified, uses default tvOS SDK version from 'xcode\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--watchos_sdk_version=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Specifies the version of the watchOS SDK to use to build watchOS applications. If unspecified, uses default watchOS SDK version from 'xcode\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--xcode_version=<a string>` default: see description
:   If specified, uses Xcode of the given version for relevant build actions. If unspecified, uses the executor default version of Xcode.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--xcode_version_config=<a build target label>` default: "@bazel\_tools//tools/cpp:host\_xcodes"
:   The label of the xcode\_config rule to be used for selecting the Xcode version in the build configuration.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

Options that control the output of the command:

`--[no]apple_enable_auto_dsym_dbg` default: "false"
:   Whether to force enable generating debug symbol(.dSYM) file(s) for dbg builds.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--[no]apple_generate_dsym` default: "false"
:   Whether to generate debug symbol(.dSYM) file(s).
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--[no]build_runfile_links` default: "true"
:   If true, build runfiles symlink forests for all targets. If false, write only manifests when possible.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]build_runfile_manifests` default: "true"
:   If true, write runfiles manifests for all targets. If false, omit them. Local tests will fail to run when false.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]build_test_dwp` default: "false"
:   If enabled, when building C++ tests statically and with fission the .dwp file for the test binary will be automatically built as well.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--cc_proto_library_header_suffixes=<comma-separated list of options>` default: ".pb.h"
:   Sets the prefixes of header files that a cc\_proto\_library creates.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--cc_proto_library_source_suffixes=<comma-separated list of options>` default: ".pb.cc"
:   Sets the prefixes of source files that a cc\_proto\_library creates.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_proto_descriptor_sets_include_source_info` default: "false"
:   Run extra actions for alternative Java api versions in a proto\_library.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_proto_extra_actions` default: "false"
:   Run extra actions for alternative Java api versions in a proto\_library.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_save_feature_state` default: "false"
:   Save the state of enabled and requested feautres as an output of compilation.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--fission=<a set of compilation modes>` default: "no"
:   Specifies which compilation modes use fission for C++ compilations and links. May be any combination of {'fastbuild', 'dbg', 'opt'} or the special values 'yes' to enable all modes and 'no' to disable all modes.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]incompatible_always_include_files_in_data` default: "true"
:   If true, native rules add <code>DefaultInfo.files</code> of data dependencies to their runfiles, which matches the recommended behavior for Starlark rules (https://bazel.build/extending/rules#runfiles\_features\_to\_avoid).
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]legacy_external_runfiles` default: "true"
:   If true, build runfiles symlink forests for external repositories under .runfiles/wsname/external/repo (in addition to .runfiles/repo).
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]objc_generate_linkmap` default: "false"
:   Specifies whether to generate a linkmap file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]save_temps` default: "false"
:   If set, temporary outputs from gcc will be saved. These include .s files (assembler code), .i files (preprocessed C) and .ii files (preprocessed C++).
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

Options that let the user configure the intended output, affecting its value, as opposed to its existence:

`--action_env=<a 'name=value' assignment with an optional value part>` multiple uses are accumulated
:   Specifies the set of environment variables available to actions with target configuration. Variables can be either specified by name, in which case the value will be taken from the invocation environment, or by the name=value pair which sets the value independent of the invocation environment. This option can be used multiple times; for options given for the same variable, the latest wins, options for different variables accumulate.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--android_cpu=<a string>` default: "armeabi-v7a"
:   The Android target CPU.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]android_databinding_use_androidx` default: "false"
:   Generate AndroidX-compatible data-binding files. This is only used with databinding v2.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]android_databinding_use_v3_4_args` default: "false"
:   Use android databinding v2 with 3.4.0 argument
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--android_dynamic_mode=<off, default or fully>` default: "off"
:   Determines whether C++ deps of Android rules will be linked dynamically when a cc\_binary does not explicitly create a shared library. 'default' means bazel will choose whether to link dynamically. 'fully' means all libraries will be linked dynamically. 'off' means that all libraries will be linked in mostly static mode.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--android_manifest_merger_order=<alphabetical, alphabetical_by_configuration or dependency>` default: "alphabetical"
:   Sets the order of manifests passed to the manifest merger for Android binaries. ALPHABETICAL means manifests are sorted by path relative to the execroot. ALPHABETICAL\_BY\_CONFIGURATION means manifests are sorted by paths relative to the configuration directory within the output directory. DEPENDENCY means manifests are ordered with each library's manifest coming before the manifests of its dependencies.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`execution`](#effect_tag_EXECUTION)

`--[no]android_resource_shrinking` default: "false"
:   Enables resource shrinking for android\_binary APKs that use ProGuard.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--apple_bitcode=<'mode' or 'platform=mode', where 'mode' is none, embedded_markers or embedded, and 'platform' is ios, visionos, watchos, tvos, macos or catalyst>` multiple uses are accumulated
:   Specify the Apple bitcode mode for compile steps targeting device architectures. Values are of the form '[platform=]mode', where the platform (which must be 'ios', 'macos', 'tvos', or 'watchos') is optional. If provided, the bitcode mode is applied for that platform specifically; if omitted, it is applied for all platforms. The mode must be 'none', 'embedded\_markers', or 'embedded'. This option may be provided multiple times.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]build_python_zip` default: "auto"
:   Build python executable zip; on on Windows, off on other platforms
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--catalyst_cpus=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of architectures for which to build Apple Catalyst binaries.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]collect_code_coverage` default: "false"
:   If specified, Bazel will instrument code (using offline instrumentation where possible) and will collect coverage information during tests. Only targets that match --instrumentation\_filter will be affected. Usually this option should not be specified directly - 'bazel coverage' command should be used instead.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--compilation_mode=<fastbuild, dbg or opt>` [`-c`] default: "fastbuild"
:   Specify the mode the binary will be built in. Values: 'fastbuild', 'dbg', 'opt'.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`explicit_in_output_path`](#metadata_tag_EXPLICIT_IN_OUTPUT_PATH)

`--conlyopt=<a string>` multiple uses are accumulated
:   Additional option to pass to gcc when compiling C source files.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--copt=<a string>` multiple uses are accumulated
:   Additional options to pass to gcc.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--cpu=<a string>` default: ""
:   The target CPU.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`explicit_in_output_path`](#metadata_tag_EXPLICIT_IN_OUTPUT_PATH)

`--cs_fdo_absolute_path=<a string>` default: see description
:   Use CSFDO profile information to optimize compilation. Specify the absolute path name of the zip file containing the profile file, a raw or an indexed LLVM profile file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--cs_fdo_instrument=<a string>` default: see description
:   Generate binaries with context sensitive FDO instrumentation. With Clang/LLVM compiler, it also accepts the directory name under which the raw profile file(s) will be dumped at runtime.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--cs_fdo_profile=<a build target label>` default: see description
:   The cs\_fdo\_profile representing the context sensitive profile to be used for optimization.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--cxxopt=<a string>` multiple uses are accumulated
:   Additional option to pass to gcc when compiling C++ source files.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--define=<a 'name=value' assignment>` multiple uses are accumulated
:   Each --define option specifies an assignment for a build variable.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--dynamic_mode=<off, default or fully>` default: "default"
:   Determines whether C++ binaries will be linked dynamically. 'default' means Bazel will choose whether to link dynamically. 'fully' means all libraries will be linked dynamically. 'off' means that all libraries will be linked in mostly static mode.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]enable_fdo_profile_absolute_path` default: "true"
:   If set, use of fdo\_absolute\_profile\_path will raise an error.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]enable_runfiles` default: "auto"
:   Enable runfiles symlink tree; By default, it's off on Windows, on on other platforms.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_action_listener=<a build target label>` multiple uses are accumulated
:   Deprecated in favor of aspects. Use action\_listener to attach an extra\_action to existing build actions.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_android_compress_java_resources` default: "false"
:   Compress Java resources in APKs
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_android_databinding_v2` default: "false"
:   Use android databinding v2
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_android_resource_shrinking` default: "false"
:   Enables resource shrinking for android\_binary APKs that use ProGuard.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_android_rewrite_dexes_with_rex` default: "false"
:   use rex tool to rewrite dex files
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_collect_code_coverage_for_generated_files` default: "false"
:   If specified, Bazel will also generate collect coverage information for generated files.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_objc_fastbuild_options=<comma-separated list of options>` default: "-O0,-DDEBUG=1"
:   Uses these strings as objc fastbuild compiler options.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--[no]experimental_omitfp` default: "false"
:   If true, use libunwind for stack unwinding, and compile with -fomit-frame-pointer and -fasynchronous-unwind-tables.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_platform_in_output_dir` default: "false"
:   If true, the target platform is used in the output directory name instead of the CPU.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_use_llvm_covmap` default: "false"
:   If specified, Bazel will generate llvm-cov coverage map information rather than gcov when collect\_code\_coverage is enabled.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--fat_apk_cpu=<comma-separated list of options>` default: "armeabi-v7a"
:   Setting this option enables fat APKs, which contain native binaries for all specified target architectures, e.g., --fat\_apk\_cpu=x86,armeabi-v7a. If this flag is specified, then --android\_cpu is ignored for dependencies of android\_binary rules.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]fat_apk_hwasan` default: "false"
:   Whether to create HWASAN splits.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--fdo_instrument=<a string>` default: see description
:   Generate binaries with FDO instrumentation. With Clang/LLVM compiler, it also accepts the directory name under which the raw profile file(s) will be dumped at runtime.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--fdo_optimize=<a string>` default: see description
:   Use FDO profile information to optimize compilation. Specify the name of a zip file containing a .gcda file tree, an afdo file containing an auto profile, or an LLVM profile file. This flag also accepts files specified as labels (e.g. `//foo/bar:file.afdo` - you may need to add an `exports\_files` directive to the corresponding package) and labels pointing to `fdo\_profile` targets. This flag will be superseded by the `fdo\_profile` rule.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--fdo_prefetch_hints=<a build target label>` default: see description
:   Use cache prefetch hints.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--fdo_profile=<a build target label>` default: see description
:   The fdo\_profile representing the profile to be used for optimization.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--features=<a string>` multiple uses are accumulated
:   The given features will be enabled or disabled by default for targets built in the target configuration. Specifying -<feature> will disable the feature. Negative features always override positive ones. See also --host\_features
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]force_pic` default: "false"
:   If enabled, all C++ compilations produce position-independent code ("-fPIC"), links prefer PIC pre-built libraries over non-PIC libraries, and links produce position-independent executables ("-pie").
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_action_env=<a 'name=value' assignment with an optional value part>` multiple uses are accumulated
:   Specifies the set of environment variables available to actions with host or execution configurations. Variables can be either specified by name, in which case the value will be taken from the invocation environment, or by the name=value pair which sets the value independent of the invocation environment. This option can be used multiple times; for options given for the same variable, the latest wins, options for different variables accumulate.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--host_compilation_mode=<fastbuild, dbg or opt>` default: "opt"
:   Specify the mode the tools used during the build will be built in. Values: 'fastbuild', 'dbg', 'opt'.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--host_conlyopt=<a string>` multiple uses are accumulated
:   Additional option to pass to gcc when compiling C source files for host tools.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_copt=<a string>` multiple uses are accumulated
:   Additional options to pass to gcc for host tools.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_cpu=<a string>` default: ""
:   The host CPU.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_cxxopt=<a string>` multiple uses are accumulated
:   Additional options to pass to gcc for host tools.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_features=<a string>` multiple uses are accumulated
:   The given features will be enabled or disabled by default for targets built in the exec configuration. Specifying -<feature> will disable the feature. Negative features always override positive ones.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_force_python=<PY2 or PY3>` default: see description
:   Overrides the Python version for the host configuration. Can be "PY2" or "PY3".
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_linkopt=<a string>` multiple uses are accumulated
:   Additional option to pass to gcc when linking host tools.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_macos_minimum_os=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Minimum compatible macOS version for host targets. If unspecified, uses 'macos\_sdk\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--host_per_file_copt=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths followed by an @ and a comma separated list of options>` multiple uses are accumulated
:   Additional options to selectively pass to the C/C++ compiler when compiling certain files in the host or exec configurations. This option can be passed multiple times. Syntax: regex\_filter@option\_1,option\_2,...,option\_n. Where regex\_filter stands for a list of include and exclude regular expression patterns (Also see --instrumentation\_filter). option\_1 to option\_n stand for arbitrary command line options. If an option contains a comma it has to be quoted with a backslash. Options can contain @. Only the first @ is used to split the string. Example: --host\_per\_file\_copt=//foo/.\*\.cc,-//foo/bar\.cc@-O0 adds the -O0 command line option to the gcc command line of all cc files in //foo/ except bar.cc.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--host_swiftcopt=<a string>` multiple uses are accumulated
:   Additional options to pass to swiftc for host tools.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]incompatible_avoid_conflict_dlls` default: "true"
:   If enabled, all C++ dynamic linked libraries (DLLs) generated by cc\_library on Windows will be renamed to name\_{hash}.dll where hash is calculated based on the RepositoryName and the DLL's package path. This option is useful when you have one package which depends on severals cc\_library with the same name (e.g //foo/bar1:utils and //foo/bar2:utils).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_merge_genfiles_directory` default: "true"
:   If true, the genfiles directory is folded into the bin directory.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_use_host_features` default: "false"
:   If true, use --features only for the target configuration and --host\_features for the exec configuration.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_use_platforms_repo_for_constraints` default: "true"
:   If true, constraint settings from @bazel\_tools are removed.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]instrument_test_targets` default: "false"
:   When coverage is enabled, specifies whether to consider instrumenting test rules. When set, test rules included by --instrumentation\_filter are instrumented. Otherwise, test rules are always excluded from coverage instrumentation.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--instrumentation_filter=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths>` default: "-/javatests[/:],-/test/java[/:]"
:   When coverage is enabled, only rules with names included by the specified regex-based filter will be instrumented. Rules prefixed with '-' are excluded instead. Note that only non-test rules are instrumented unless --instrument\_test\_targets is enabled.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--ios_minimum_os=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Minimum compatible iOS version for target simulators and devices. If unspecified, uses 'ios\_sdk\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--ios_multi_cpus=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of architectures to build an ios\_application with. The result is a universal binary containing all specified architectures.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]legacy_whole_archive` default: "true"
:   Deprecated, superseded by --incompatible\_remove\_legacy\_whole\_archive (see https://github.com/bazelbuild/bazel/issues/7362 for details). When on, use --whole-archive for cc\_binary rules that have linkshared=True and either linkstatic=True or '-static' in linkopts. This is for backwards compatibility only. A better alternative is to use alwayslink=1 where required.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`deprecated`](#metadata_tag_DEPRECATED)

`--linkopt=<a string>` multiple uses are accumulated
:   Additional option to pass to gcc when linking.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--ltobackendopt=<a string>` multiple uses are accumulated
:   Additional option to pass to the LTO backend step (under --features=thin\_lto).
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--ltoindexopt=<a string>` multiple uses are accumulated
:   Additional option to pass to the LTO indexing step (under --features=thin\_lto).
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--macos_cpus=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of architectures for which to build Apple macOS binaries.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--macos_minimum_os=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Minimum compatible macOS version for targets. If unspecified, uses 'macos\_sdk\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]objc_debug_with_GLIBCXX` default: "false"
:   If set, and compilation mode is set to 'dbg', define GLIBCXX\_DEBUG, GLIBCXX\_DEBUG\_PEDANTIC and GLIBCPP\_CONCEPT\_CHECKS.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--[no]objc_enable_binary_stripping` default: "false"
:   Whether to perform symbol and dead-code strippings on linked binaries. Binary strippings will be performed if both this flag and --compilation\_mode=opt are specified.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--objccopt=<a string>` multiple uses are accumulated
:   Additional options to pass to gcc when compiling Objective-C/C++ source files.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--per_file_copt=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths followed by an @ and a comma separated list of options>` multiple uses are accumulated
:   Additional options to selectively pass to gcc when compiling certain files. This option can be passed multiple times. Syntax: regex\_filter@option\_1,option\_2,...,option\_n. Where regex\_filter stands for a list of include and exclude regular expression patterns (Also see --instrumentation\_filter). option\_1 to option\_n stand for arbitrary command line options. If an option contains a comma it has to be quoted with a backslash. Options can contain @. Only the first @ is used to split the string. Example: --per\_file\_copt=//foo/.\*\.cc,-//foo/bar\.cc@-O0 adds the -O0 command line option to the gcc command line of all cc files in //foo/ except bar.cc.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--per_file_ltobackendopt=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths followed by an @ and a comma separated list of options>` multiple uses are accumulated
:   Additional options to selectively pass to LTO backend (under --features=thin\_lto) when compiling certain backend objects. This option can be passed multiple times. Syntax: regex\_filter@option\_1,option\_2,...,option\_n. Where regex\_filter stands for a list of include and exclude regular expression patterns. option\_1 to option\_n stand for arbitrary command line options. If an option contains a comma it has to be quoted with a backslash. Options can contain @. Only the first @ is used to split the string. Example: --per\_file\_ltobackendopt=//foo/.\*\.o,-//foo/bar\.o@-O0 adds the -O0 command line option to the LTO backend command line of all o files in //foo/ except bar.o.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--platform_suffix=<a string>` default: see description
:   Specifies a suffix to be added to the configuration directory.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--propeller_optimize=<a build target label>` default: see description
:   Use Propeller profile information to optimize the build target.A propeller profile must consist of at least one of two files, a cc profile and a ld profile. This flag accepts a build label which must refer to the propeller profile input files. For example, the BUILD file that defines the label, in a/b/BUILD:propeller\_optimize( name = "propeller\_profile", cc\_profile = "propeller\_cc\_profile.txt", ld\_profile = "propeller\_ld\_profile.txt",)An exports\_files directive may have to be added to the corresponding package to make these files visible to Bazel. The option must be used as: --propeller\_optimize=//a/b:propeller\_profile
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--propeller_optimize_absolute_cc_profile=<a string>` default: see description
:   Absolute path name of cc\_profile file for Propeller Optimized builds.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--propeller_optimize_absolute_ld_profile=<a string>` default: see description
:   Absolute path name of ld\_profile file for Propeller Optimized builds.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--run_under=<a prefix in front of command>` default: see description
:   Prefix to insert before the executables for the 'test' and 'run' commands. If the value is 'foo -bar', and the execution command line is 'test\_binary -baz', then the final command line is 'foo -bar test\_binary -baz'.This can also be a label to an executable target. Some examples are: 'valgrind', 'strace', 'strace -c', 'valgrind --quiet --num-callers=20', '//package:target', '//package:target --options'.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--[no]share_native_deps` default: "true"
:   If true, native libraries that contain identical functionality will be shared among different targets
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]stamp` default: "false"
:   Stamp binaries with the date, username, hostname, workspace information, etc.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--strip=<always, sometimes or never>` default: "sometimes"
:   Specifies whether to strip binaries and shared libraries (using "-Wl,--strip-debug"). The default value of 'sometimes' means strip iff --compilation\_mode=fastbuild.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--stripopt=<a string>` multiple uses are accumulated
:   Additional options to pass to strip when generating a '<name>.stripped' binary.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--swiftcopt=<a string>` multiple uses are accumulated
:   Additional options to pass to Swift compilation.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--tvos_cpus=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of architectures for which to build Apple tvOS binaries.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--tvos_minimum_os=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Minimum compatible tvOS version for target simulators and devices. If unspecified, uses 'tvos\_sdk\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--visionos_cpus=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of architectures for which to build Apple visionOS binaries.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--watchos_cpus=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of architectures for which to build Apple watchOS binaries.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--watchos_minimum_os=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   Minimum compatible watchOS version for target simulators and devices. If unspecified, uses 'watchos\_sdk\_version'.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--xbinary_fdo=<a build target label>` default: see description
:   Use XbinaryFDO profile information to optimize compilation. Specify the name of default cross binary profile. When the option is used together with --fdo\_instrument/--fdo\_optimize/--fdo\_profile, those options will always prevail as if xbinary\_fdo is never specified.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

Options that affect how strictly Bazel enforces valid build inputs (rule definitions, flag combinations, etc.):

`--auto_cpu_environment_group=<a build target label>` default: ""
:   Declare the environment\_group to use for automatically mapping cpu values to target\_environment values.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]check_licenses` default: "false"
:   Check that licensing constraints imposed by dependent packages do not conflict with distribution modes of the targets being built. By default, licenses are not checked.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]check_visibility` default: "true"
:   If disabled, visibility errors in target dependencies are demoted to warnings.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]desugar_for_android` default: "true"
:   Whether to desugar Java 8 bytecode before dexing.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]desugar_java8_libs` default: "false"
:   Whether to include supported Java 8 libraries in apps for legacy devices.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]enforce_constraints` default: "true"
:   Checks the environments each target is compatible with and reports errors if any target has dependencies that don't support the same environments
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]experimental_allow_android_library_deps_without_srcs` default: "false"
:   Flag to help transition from allowing to disallowing srcs-less android\_library rules with deps. The depot needs to be cleaned up to roll this out by default.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_check_desugar_deps` default: "true"
:   Whether to double-check correct desugaring at Android binary level.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--experimental_import_deps_checking=<off, warning or error>` default: "OFF"
:   When enabled, check whether the dependencies of an aar\_import are complete. This enforcement can break the build, or can just result in warnings.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--experimental_strict_java_deps=<off, warn, error, strict or default>` default: "default"
:   If true, checks that a Java target explicitly declares all directly used targets as dependencies.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--[no]incompatible_check_testonly_for_output_files` default: "false"
:   If enabled, check testonly for prerequisite targets that are output files by looking up the testonly of the generating rule. This matches visibility checking.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disable_native_android_rules` default: "false"
:   If enabled, direct usage of the native Android rules is disabled. Please use the Starlark Android rules from https://github.com/bazelbuild/rules\_android
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disable_native_apple_binary_rule` default: "false"
:   No-op. Kept here for backwards compatibility.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_force_strict_header_check_from_starlark` default: "true"
:   If enabled, set strict header checking in the Starlark API
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_validate_top_level_header_inclusions` default: "true"
:   If true, Bazel will also validate top level directory header inclusions (see https://github.com/bazelbuild/bazel/issues/10047 for more information).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]strict_filesets` default: "false"
:   If this option is enabled, filesets crossing package boundaries are reported as errors. It does not work when check\_fileset\_dependencies\_recursively is disabled.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--strict_proto_deps=<off, warn, error, strict or default>` default: "error"
:   Unless OFF, checks that a proto\_library target explicitly declares all directly used targets as dependencies.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--strict_public_imports=<off, warn, error, strict or default>` default: "off"
:   Unless OFF, checks that a proto\_library target explicitly declares all targets used in 'import public' as exported.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]strict_system_includes` default: "false"
:   If true, headers found through system include paths (-isystem) are also required to be declared.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--target_environment=<a build target label>` multiple uses are accumulated
:   Declares this build's target environment. Must be a label reference to an "environment" rule. If specified, all top-level targets must be compatible with this environment.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Options that affect the signing outputs of a build:

`--apk_signing_method=<v1, v2, v1_v2 or v4>` default: "v1\_v2"
:   Implementation to use to sign APKs
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]device_debug_entitlements` default: "true"
:   If set, and compilation mode is not 'opt', objc apps will include debug entitlements when signing.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--ios_signing_cert_name=<a string>` default: see description
:   Certificate name to use for iOS signing. If not set will fall back to provisioning profile. May be the certificate's keychain identity preference or (substring) of the certificate's common name, as per codesign's man page (SIGNING IDENTITIES).
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

This option affects semantics of the Starlark language or the build API accessible to BUILD files, .bzl files, or WORKSPACE files.:

`--[no]incompatible_disallow_legacy_py_provider` default: "true"
:   No-op, will be removed soon.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

Options that govern the behavior of the test environment or test runner:

`--[no]allow_analysis_failures` default: "false"
:   If true, an analysis failure of a rule target results in the target's propagation of an instance of AnalysisFailureInfo containing the error description, instead of resulting in a build failure.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--analysis_testing_deps_limit=<an integer>` default: "2000"
:   Sets the maximum number of transitive dependencies through a rule attribute with a for\_analysis\_testing configuration transition. Exceeding this limit will result in a rule error.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]break_build_on_parallel_dex2oat_failure` default: "false"
:   If true dex2oat action failures will cause the build to break instead of executing dex2oat during test runtime.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_android_use_parallel_dex2oat` default: "false"
:   Use dex2oat in parallel to possibly speed up android\_test.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]ios_memleaks` default: "false"
:   Enable checking for memory leaks in ios\_test targets.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--ios_simulator_device=<a string>` default: see description
:   The device to simulate when running an iOS application in the simulator, e.g. 'iPhone 6'. You can get a list of devices by running 'xcrun simctl list devicetypes' on the machine the simulator will be run on.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--ios_simulator_version=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   The version of iOS to run on the simulator when running or testing. This is ignored for ios\_test rules if a target device is specified in the rule.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--runs_per_test=<a positive integer or test_regex@runs. This flag may be passed more than once>` multiple uses are accumulated
:   Specifies number of times to run each test. If any of those attempts fail for any reason, the whole test is considered failed. Normally the value specified is just an integer. Example: --runs\_per\_test=3 will run all tests 3 times. Alternate syntax: regex\_filter@runs\_per\_test. Where runs\_per\_test stands for an integer value and regex\_filter stands for a list of include and exclude regular expression patterns (Also see --instrumentation\_filter). Example: --runs\_per\_test=//foo/.\*,-//foo/bar/.\*@3 runs all tests in //foo/ except those under foo/bar three times. This option can be passed multiple times. The most recently passed argument that matches takes precedence. If nothing matches, the test is only run once.

`--test_env=<a 'name=value' assignment with an optional value part>` multiple uses are accumulated
:   Specifies additional environment variables to be injected into the test runner environment. Variables can be either specified by name, in which case its value will be read from the Bazel client environment, or by the name=value pair. This option can be used multiple times to specify several variables. Used only by the 'bazel test' command.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--test_timeout=<a single integer or comma-separated list of 4 integers>` default: "-1"
:   Override the default test timeout values for test timeouts (in secs). If a single positive integer value is specified it will override all categories. If 4 comma-separated integers are specified, they will override the timeouts for short, moderate, long and eternal (in that order). In either form, a value of -1 tells blaze to use its default timeouts for that category.

`--tvos_simulator_device=<a string>` default: see description
:   The device to simulate when running a tvOS application in the simulator, e.g. 'Apple TV 1080p'. You can get a list of devices by running 'xcrun simctl list devicetypes' on the machine the simulator will be run on.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--tvos_simulator_version=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   The version of tvOS to run on the simulator when running or testing.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--watchos_simulator_device=<a string>` default: see description
:   The device to simulate when running a watchOS application in the simulator, e.g. 'Apple Watch - 38mm'. You can get a list of devices by running 'xcrun simctl list devicetypes' on the machine the simulator will be run on.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--watchos_simulator_version=<a dotted version (for example '2.3' or '3.3alpha2.4')>` default: see description
:   The version of watchOS to run on the simulator when running or testing.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--[no]zip_undeclared_test_outputs` default: "true"
:   If true, undeclared test outputs will be archived in a zip file.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

Options relating to query output and semantics:

`--aspect_deps=<off, conservative or precise>` default: "conservative"
:   How to resolve aspect dependencies when the output format is one of {xml,proto,record}. 'off' means no aspect dependencies are resolved, 'conservative' (the default) means all declared aspect dependencies are added regardless of whether they are given the rule class of direct dependencies, 'precise' means that only those aspects are added that are possibly active given the rule class of the direct dependencies. Note that precise mode requires loading other packages to evaluate a single target thus making it slower than the other modes. Also note that even precise mode is not completely precise: the decision whether to compute an aspect is decided in the analysis phase, which is not run during 'bazel query'.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]consistent_labels` default: "false"
:   If enabled, every query command emits labels as if by the Starlark <code>str</code> function applied to a <code>Label</code> instance. This is useful for tools that need to match the output of different query commands and/or labels emitted by rules. If not enabled, output formatters are free to emit apparent repository names (relative to the main repository) instead to make the output more readable.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]deduplicate_depsets` default: "true"
:   De-duplicate non-leaf children of a dep\_set\_of\_files in the final proto/textproto/json output. This does not deduplicate depsets that don't share an immediate parent. This does not affect the final effective list of input artifacts of the actions.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]graph:factored` default: "true"
:   If true, then the graph will be emitted 'factored', i.e. topologically-equivalent nodes will be merged together and their labels concatenated. This option is only applicable to --output=graph.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--graph:node_limit=<an integer>` default: "512"
:   The maximum length of the label string for a graph node in the output. Longer labels will be truncated; -1 means no truncation. This option is only applicable to --output=graph.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]implicit_deps` default: "true"
:   If enabled, implicit dependencies will be included in the dependency graph over which the query operates. An implicit dependency is one that is not explicitly specified in the BUILD file but added by bazel. For cquery, this option controls filtering resolved toolchains.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]include_artifacts` default: "true"
:   Includes names of the action inputs and outputs in the output (potentially large).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_aspects` default: "true"
:   aquery, cquery: whether to include aspect-generated actions in the output. query: no-op (aspects are always followed).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_commandline` default: "true"
:   Includes the content of the action command lines in the output (potentially large).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_file_write_contents` default: "false"
:   Include the file contents for the FileWrite and SourceSymlinkManifest actions (potentially large).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]include_param_files` default: "false"
:   Include the content of the param files used in the command (potentially large). Note: Enabling this flag will automatically enable the --include\_commandline flag.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]incompatible_display_source_file_location` default: "true"
:   True by default, displays the target of the source file. If true, displays the location of line 1 of source files in location outputs. This flag only exists for migration purposes.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_package_group_includes_double_slash` default: "true"
:   If enabled, when outputting package\_group's `packages` attribute, the leading `//` will not be omitted.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]infer_universe_scope` default: "false"
:   If set and --universe\_scope is unset, then a value of --universe\_scope will be inferred as the list of unique target patterns in the query expression. Note that the --universe\_scope value inferred for a query expression that uses universe-scoped functions (e.g.`allrdeps`) may not be what you want, so you should use this option only if you know what you are doing. See https://bazel.build/reference/query#sky-query for details and examples. If --universe\_scope is set, then this option's value is ignored. Note: this option applies only to `query` (i.e. not `cquery`).
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]line_terminator_null` default: "false"
:   Whether each format is terminated with \0 instead of newline.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]nodep_deps` default: "true"
:   If enabled, deps from "nodep" attributes will be included in the dependency graph over which the query operates. A common example of a "nodep" attribute is "visibility". Run and parse the output of `info build-language` to learn about all the "nodep" attributes in the build language.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--output=<a string>` default: "text"
:   The format in which the aquery results should be printed. Allowed values for aquery are: text, textproto, proto, jsonproto.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:default_values` default: "true"
:   If true, attributes whose value is not explicitly specified in the BUILD file are included; otherwise they are omitted. This option is applicable to --output=proto
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:definition_stack` default: "false"
:   Populate the definition\_stack proto field, which records for each rule instance the Starlark call stack at the moment the rule's class was defined.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:flatten_selects` default: "true"
:   If enabled, configurable attributes created by select() are flattened. For list types the flattened representation is a list containing each value of the select map exactly once. Scalar types are flattened to null.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]proto:include_synthetic_attribute_hash` default: "false"
:   Whether or not to calculate and populate the $internal\_attr\_hash attribute.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:instantiation_stack` default: "false"
:   Populate the instantiation call stack of each rule. Note that this requires the stack to be present
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:locations` default: "true"
:   Whether to output location information in proto output at all.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--proto:output_rule_attrs=<comma-separated list of options>` default: "all"
:   Comma separated list of attributes to include in output. Defaults to all attributes. Set to empty string to not output any attribute. This option is applicable to --output=proto.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]proto:rule_inputs_and_outputs` default: "true"
:   Whether or not to populate the rule\_input and rule\_output fields.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--query_file=<a string>` default: ""
:   If set, query will read the query from the file named here, rather than on the command line. It is an error to specify a file here as well as a command-line query.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]relative_locations` default: "false"
:   If true, the location of BUILD files in xml and proto outputs will be relative. By default, the location output is an absolute path and will not be consistent across machines. You can set this option to true to have a consistent result across machines.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]skyframe_state` default: "false"
:   Without performing extra analysis, dump the current Action Graph from Skyframe. Note: Specifying a target with --skyframe\_state is currently not supported. This flag is only available with --output=proto or --output=textproto.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]tool_deps` default: "true"
:   Query: If disabled, dependencies on 'host configuration' or 'execution' targets will not be included in the dependency graph over which the query operates. A 'host configuration' dependency edge, such as the one from any 'proto\_library' rule to the Protocol Compiler, usually points to a tool executed during the build rather than a part of the same 'target' program.
    Cquery: If disabled, filters out all configured targets which cross a host or execution transition from the top-level target that discovered this configured target. That means if the top-level target is in the target configuration, only configured targets also in the target configuration will be returned. If the top-level target is in the host configuration, only host configured targets will be returned. This option will NOT exclude resolved toolchains.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--universe_scope=<comma-separated list of options>` default: ""
:   A comma-separated set of target patterns (additive and subtractive). The query may be performed in the universe defined by the transitive closure of the specified targets. This option is used for the query and cquery commands.
    For cquery, the input to this option is the targets all answers are built under and so this option may affect configurations and transitions. If this option is not specified, the top-level targets are assumed to be the targets parsed from the query expression. Note: For cquery, not specifying this option may cause the build to break if targets parsed from the query expression are not buildable with top-level options.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

Options that trigger optimizations of the build time:

`--[no]collapse_duplicate_defines` default: "false"
:   When enabled, redundant --defines will be removed early in the build. This avoids unnecessary loss of the analysis cache for certain types of equivalent builds.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]experimental_filter_library_jar_with_program_jar` default: "false"
:   Filter the ProGuard ProgramJar to remove any classes also present in the LibraryJar.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

`--[no]experimental_inmemory_dotd_files` default: "true"
:   If enabled, C++ .d files will be passed through in memory directly from the remote build nodes instead of being written to disk.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_inmemory_jdeps_files` default: "true"
:   If enabled, the dependency (.jdeps) files generated from Java compilations will be passed through in memory directly from the remote build nodes instead of being written to disk.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_objc_include_scanning` default: "false"
:   Whether to perform include scanning for objective C/C++.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION), [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]experimental_parse_headers_skipped_if_corresponding_srcs_found` default: "false"
:   If enabled, the parse\_headers feature does not create a separate header compile action if a source with the same basename is found in the same target.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_retain_test_configuration_across_testonly` default: "false"
:   When enabled, --trim\_test\_configuration will not trim the test configuration for rules marked testonly=1. This is meant to reduce action conflict issues when non-test rules depend on cc\_test rules. No effect if --trim\_test\_configuration is false.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]experimental_starlark_cc_import` default: "false"
:   If enabled, the Starlark version of cc\_import can be used.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_unsupported_and_brittle_include_scanning` default: "false"
:   Whether to narrow inputs to C/C++ compilation by parsing #include lines from input files. This can improve performance and incrementality by decreasing the size of compilation input trees. However, it can also break builds because the include scanner does not fully implement C preprocessor semantics. In particular, it does not understand dynamic #include directives and ignores preprocessor conditional logic. Use at your own risk. Any issues relating to this flag that are filed will be closed.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`execution`](#effect_tag_EXECUTION), [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]incremental_dexing` default: "true"
:   Does most of the work for dexing separately for each Jar file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]objc_use_dotd_pruning` default: "true"
:   If set, .d files emitted by clang will be used to prune the set of inputs passed into objc compiles.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]process_headers_in_dependencies` default: "false"
:   When building a target //a:a, process headers in all targets that //a:a depends on (if header processing is enabled for the toolchain).
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]trim_test_configuration` default: "true"
:   When enabled, test-related options will be cleared below the top level of the build. When this flag is active, tests cannot be built as dependencies of non-test rules, but changes to test-related options will not cause non-test rules to be re-analyzed.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]use_singlejar_apkbuilder` default: "true"
:   This option is a deprecated. It is now a no-op and will be removed soon.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

Options that affect the verbosity, format or location of logging:

`--toolchain_resolution_debug=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths>` default: "-.\*"
:   Print debug information during toolchain resolution. The flag takes a regex, which is checked against toolchain types and specific targets to see which to debug. Multiple regexes may be separated by commas, and then each regex is checked separately. Note: The output of this flag is very complex and will likely only be useful to experts in toolchain resolution.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

Options specifying or altering a generic input to a Bazel command that does not fall into other categories.:

`--flag_alias=<a 'name=value' flag alias>` multiple uses are accumulated
:   Sets a shorthand name for a Starlark flag. It takes a single key-value pair in the form "<key>=<value>" as an argument.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]incompatible_default_to_explicit_init_py` default: "false"
:   This flag changes the default behavior so that \_\_init\_\_.py files are no longer automatically created in the runfiles of Python targets. Precisely, when a py\_binary or py\_test target has legacy\_create\_init set to "auto" (the default), it is treated as false if and only if this flag is set. See https://github.com/bazelbuild/bazel/issues/10076.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_py2_outputs_are_suffixed` default: "true"
:   If true, targets built in the Python 2 configuration will appear under an output root that includes the suffix '-py2', while targets built for Python 3 will appear in a root with no Python-related suffix. This means that the `bazel-bin` convenience symlink will point to Python 3 targets rather than Python 2. If you enable this option it is also recommended to enable `--incompatible\_py3\_is\_default`.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_py3_is_default` default: "true"
:   If true, `py\_binary` and `py\_test` targets that do not set their `python\_version` (or `default\_python\_version`) attribute will default to PY3 rather than to PY2. If you set this flag it is also recommended to set `--incompatible\_py2\_outputs\_are\_suffixed`.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_use_python_toolchains` default: "true"
:   If set to true, executable native Python rules will use the Python runtime specified by the Python toolchain, rather than the runtime given by legacy flags like --python\_top.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--python_version=<PY2 or PY3>` default: see description
:   The Python major version mode, either `PY2` or `PY3`. Note that this is overridden by `py\_binary` and `py\_test` targets (even if they don't explicitly specify a version) so there is usually not much reason to supply this flag.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`explicit_in_output_path`](#metadata_tag_EXPLICIT_IN_OUTPUT_PATH)

Miscellaneous options, not otherwise categorized.:

`--[no]cache_test_results` [`-t`] default: "auto"
:   If set to 'auto', Bazel reruns a test if and only if: (1) Bazel detects changes in the test or its dependencies, (2) the test is marked as external, (3) multiple test runs were requested with --runs\_per\_test, or(4) the test previously failed. If set to 'yes', Bazel caches all test results except for tests marked as external. If set to 'no', Bazel does not cache any test results.

`--[no]experimental_cancel_concurrent_tests` default: "false"
:   If true, then Blaze will cancel concurrently running tests on the first successful run. This is only useful in combination with --runs\_per\_test\_detects\_flakes.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_fetch_all_coverage_outputs` default: "false"
:   If true, then Bazel fetches the entire coverage data directory for each test during a coverage run.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_generate_llvm_lcov` default: "false"
:   If true, coverage for clang will generate an LCOV report.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_j2objc_header_map` default: "true"
:   Whether to generate J2ObjC header map in parallel of J2ObjC transpilation.

`--[no]experimental_j2objc_shorter_header_path` default: "false"
:   Whether to generate with shorter header path (uses "\_ios" instead of "\_j2objc").
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_java_classpath=<off, javabuilder or bazel>` default: "javabuilder"
:   Enables reduced classpaths for Java compilations.

`--[no]experimental_limit_android_lint_to_android_constrained_java` default: "false"
:   Limit --experimental\_run\_android\_lint\_on\_java\_rules to Android-compatible libraries.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_run_android_lint_on_java_rules` default: "false"
:   Whether to validate java\_\* sources.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]explicit_java_test_deps` default: "false"
:   Explicitly specify a dependency to JUnit or Hamcrest in a java\_test instead of accidentally obtaining from the TestRunner's deps. Only works for bazel right now.

`--host_java_launcher=<a build target label>` default: see description
:   The Java launcher used by tools that are executed during a build.

`--host_javacopt=<a string>` multiple uses are accumulated
:   Additional options to pass to javac when building tools that are executed during a build.

`--host_jvmopt=<a string>` multiple uses are accumulated
:   Additional options to pass to the Java VM when building tools that are executed during the build. These options will get added to the VM startup options of each java\_binary target.

`--[no]incompatible_check_sharding_support` default: "false"
:   If true, Bazel will fail a sharded test if the test runner does not indicate that it supports sharding by touching the file at the path in TEST\_SHARD\_STATUS\_FILE. If false, a test runner that does not support sharding will lead to all tests running in each shard.
      
    Tags:
    [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_exclusive_test_sandboxed` default: "false"
:   If true, exclusive tests will run with sandboxed strategy. Add 'local' tag to force an exclusive test run locally
      
    Tags:
    [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_strict_action_env` default: "false"
:   If true, Bazel uses an environment with a static value for PATH and does not inherit LD\_LIBRARY\_PATH. Use --action\_env=ENV\_VARIABLE if you want to inherit specific environment variables from the client, but note that doing so can prevent cross-user caching if a shared cache is used.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--j2objc_translation_flags=<comma-separated list of options>` multiple uses are accumulated
:   Additional options to pass to the J2ObjC tool.

`--java_debug`
:   Causes the Java virtual machine of a java test to wait for a connection from a JDWP-compliant debugger (such as jdb) before starting the test. Implies -test\_output=streamed.
      
    Expands to:  
      `--test_arg=--wrapper_script_flag=--debug`  
      `--test_output=streamed`  
      `--test_strategy=exclusive`  
      `--test_timeout=9999`  
      `--nocache_test_results`

`--[no]java_deps` default: "true"
:   Generate dependency information (for now, compile-time classpath) per Java target.

`--[no]java_header_compilation` default: "true"
:   Compile ijars directly from source.

`--java_language_version=<a string>` default: "8"
:   The Java language version

`--java_launcher=<a build target label>` default: see description
:   The Java launcher to use when building Java binaries. If this flag is set to the empty string, the JDK launcher is used. The "launcher" attribute overrides this flag.

`--java_runtime_version=<a string>` default: "local\_jdk"
:   The Java runtime version

`--javacopt=<a string>` multiple uses are accumulated
:   Additional options to pass to javac.

`--jvmopt=<a string>` multiple uses are accumulated
:   Additional options to pass to the Java VM. These options will get added to the VM startup options of each java\_binary target.

`--legacy_main_dex_list_generator=<a build target label>` default: see description
:   Specifies a binary to use to generate the list of classes that must be in the main dex when compiling legacy multidex.

`--plugin=<a build target label>` multiple uses are accumulated
:   Plugins to use in the build. Currently works with java\_plugin.

`--proguard_top=<a build target label>` default: see description
:   Specifies which version of ProGuard to use for code removal when building a Java binary.

`--proto_compiler=<a build target label>` default: "@bazel\_tools//tools/proto:protoc"
:   The label of the proto-compiler.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--proto_toolchain_for_cc=<a build target label>` default: "@bazel\_tools//tools/proto:cc\_toolchain"
:   Label of proto\_lang\_toolchain() which describes how to compile C++ protos
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--proto_toolchain_for_j2objc=<a build target label>` default: "@bazel\_tools//tools/j2objc:j2objc\_proto\_toolchain"
:   Label of proto\_lang\_toolchain() which describes how to compile j2objc protos
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--proto_toolchain_for_java=<a build target label>` default: "@bazel\_tools//tools/proto:java\_toolchain"
:   Label of proto\_lang\_toolchain() which describes how to compile Java protos
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--proto_toolchain_for_javalite=<a build target label>` default: "@bazel\_tools//tools/proto:javalite\_toolchain"
:   Label of proto\_lang\_toolchain() which describes how to compile JavaLite protos
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--protocopt=<a string>` multiple uses are accumulated
:   Additional options to pass to the protobuf compiler.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]runs_per_test_detects_flakes` default: "false"
:   If true, any shard in which at least one run/attempt passes and at least one run/attempt fails gets a FLAKY status.

`--shell_executable=<a path>` default: see description
:   Absolute path to the shell executable for Bazel to use. If this is unset, but the BAZEL\_SH environment variable is set on the first Bazel invocation (that starts up a Bazel server), Bazel uses that. If neither is set, Bazel uses a hard-coded default path depending on the operating system it runs on (Windows: c:/tools/msys64/usr/bin/bash.exe, FreeBSD: /usr/local/bin/bash, all others: /bin/bash). Note that using a shell that is not compatible with bash may lead to build failures or runtime failures of the generated binaries.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--test_arg=<a string>` multiple uses are accumulated
:   Specifies additional options and arguments that should be passed to the test executable. Can be used multiple times to specify several arguments. If multiple tests are executed, each of them will receive identical arguments. Used only by the 'bazel test' command.

`--test_filter=<a string>` default: see description
:   Specifies a filter to forward to the test framework. Used to limit the tests run. Note that this does not affect which targets are built.

`--test_result_expiration=<an integer>` default: "-1"
:   This option is deprecated and has no effect.

`--[no]test_runner_fail_fast` default: "false"
:   Forwards fail fast option to the test runner. The test runner should stop execution upon first failure.

`--test_sharding_strategy=<explicit or disabled>` default: "explicit"
:   Specify strategy for test sharding: 'explicit' to only use sharding if the 'shard\_count' BUILD attribute is present. 'disabled' to never use test sharding.

`--tool_java_language_version=<a string>` default: "8"
:   The Java language version used to execute the tools that are needed during a build

`--tool_java_runtime_version=<a string>` default: "remotejdk\_11"
:   The Java runtime version used to execute tools during the build

`--[no]use_ijars` default: "true"
:   If enabled, this option causes Java compilation to use interface jars. This will result in faster incremental compilation, but error messages can be different.
