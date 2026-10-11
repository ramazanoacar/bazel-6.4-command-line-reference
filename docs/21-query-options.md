## Query Options

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

`--[no]incompatible_remote_dangling_symlinks` default: "true"
:   If set to true and --incompatible\_remote\_symlinks is also true, symlinks in action outputs are allowed to dangle.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remote_symlinks` default: "true"
:   If set to true, Bazel will represent symlinks in action outputs in the remote caching/execution protocol as such. Otherwise, symlinks will be followed and represented as files or directories. See #6631 for details.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]keep_going` [`-k`] default: "false"
:   Continue as much as possible after an error. While the target that failed and those that depend on it cannot be analyzed, other prerequisites of these targets can be.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--loading_phase_threads=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` default: "auto"
:   Number of parallel threads to use for the loading/analysis phase.Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". "auto" sets a reasonable default based on host resources. Must be at least 1.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

Options that let the user configure the intended output, affecting its value, as opposed to its existence:

`--bep_maximum_open_remote_upload_files=<an integer>` default: "-1"
:   Maximum number of open files allowed during BEP artifact upload.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--remote_download_minimal`
:   Does not download any remote build outputs to the local machine. This flag is a shortcut for flags: --experimental\_inmemory\_jdeps\_files, --experimental\_inmemory\_dotd\_files, --experimental\_action\_cache\_store\_output\_metadata and --remote\_download\_outputs=minimal.
      
    Expands to:  
      `--nobuild_runfile_links`  
      `--experimental_inmemory_jdeps_files`  
      `--experimental_inmemory_dotd_files`  
      `--experimental_action_cache_store_output_metadata`  
      `--remote_download_outputs=minimal`  
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--remote_download_outputs=<all, minimal or toplevel>` default: "all"
:   If set to 'minimal' doesn't download any remote build outputs to the local machine, except the ones required by local actions. If set to 'toplevel' behaves like'minimal' except that it also downloads outputs of top level targets to the local machine. Both options can significantly reduce build times if network bandwidth is a bottleneck.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--remote_download_symlink_template=<a string>` default: ""
:   Instead of downloading remote build outputs to the local machine, create symbolic links. The target of the symbolic links can be specified in the form of a template string. This template string may contain {hash} and {size\_bytes} that expand to the hash of the object and the size in bytes, respectively. These symbolic links may, for example, point to a FUSE file system that loads objects from the CAS on demand.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--remote_download_toplevel`
:   Only downloads remote outputs of top level targets to the local machine. This flag is a shortcut for flags: --experimental\_inmemory\_jdeps\_files, --experimental\_inmemory\_dotd\_files, --experimental\_action\_cache\_store\_output\_metadata and --remote\_download\_outputs=toplevel.
      
    Expands to:  
      `--experimental_inmemory_jdeps_files`  
      `--experimental_inmemory_dotd_files`  
      `--experimental_action_cache_store_output_metadata`  
      `--remote_download_outputs=toplevel`  
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

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

Options relating to query output and semantics:

`--aspect_deps=<off, conservative or precise>` default: "conservative"
:   How to resolve aspect dependencies when the output format is one of {xml,proto,record}. 'off' means no aspect dependencies are resolved, 'conservative' (the default) means all declared aspect dependencies are added regardless of whether they are given the rule class of direct dependencies, 'precise' means that only those aspects are added that are possibly active given the rule class of the direct dependencies. Note that precise mode requires loading other packages to evaluate a single target thus making it slower than the other modes. Also note that even precise mode is not completely precise: the decision whether to compute an aspect is decided in the analysis phase, which is not run during 'bazel query'.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]consistent_labels` default: "false"
:   If enabled, every query command emits labels as if by the Starlark <code>str</code> function applied to a <code>Label</code> instance. This is useful for tools that need to match the output of different query commands and/or labels emitted by rules. If not enabled, output formatters are free to emit apparent repository names (relative to the main repository) instead to make the output more readable.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]experimental_graphless_query` default: "auto"
:   If true, uses a Query implementation that does not make a copy of the graph. The new implementation only supports --order\_output=no, as well as only a subset of output formatters.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--graph:conditional_edges_limit=<an integer>` default: "4"
:   The maximum number of condition labels to show. -1 means no truncation and 0 means no annotation. This option is only applicable to --output=graph.
      
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

`--[no]include_aspects` default: "true"
:   aquery, cquery: whether to include aspect-generated actions in the output. query: no-op (aspects are always followed).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]incompatible_display_source_file_location` default: "true"
:   True by default, displays the target of the source file. If true, displays the location of line 1 of source files in location outputs. This flag only exists for migration purposes.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_lexicographical_output` default: "true"
:   If this option is set, sorts --order\_output=auto output in lexicographical order.
      
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

`--noorder_results`
:   Output the results in dependency-ordered (default) or unordered fashion. The unordered output is faster but only supported when --output is not minrank, maxrank, or graph.
      
    Expands to:  
      `--order_output=no`  
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--null`
:   Whether each format is terminated with \0 instead of newline.
      
    Expands to:  
      `--line_terminator_null=true`  
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--order_output=<no, deps, auto or full>` default: "auto"
:   Output the results unordered (no), dependency-ordered (deps), or fully ordered (full). The default is 'auto', meaning that results are output either dependency-ordered or fully ordered, depending on the output formatter (dependency-ordered for proto, minrank, maxrank, and graph, fully ordered for all others). When output is fully ordered, nodes are printed in a fully deterministic (total) order. First, all nodes are sorted alphabetically. Then, each node in the list is used as the start of a post-order depth-first search in which outgoing edges to unvisited nodes are traversed in alphabetical order of the successor nodes. Finally, nodes are printed in the reverse of the order in which they were visited.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--order_results`
:   Output the results in dependency-ordered (default) or unordered fashion. The unordered output is faster but only supported when --output is not minrank, maxrank, or graph.
      
    Expands to:  
      `--order_output=auto`  
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--output=<a string>` default: "label"
:   The format in which the query results should be printed. Allowed values for query are: build, graph, streamed\_jsonproto, label, label\_kind, location, maxrank, minrank, package, proto, xml.
      
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

`--[no]strict_test_suite` default: "false"
:   If true, the tests() expression gives an error if it encounters a test\_suite containing non-test targets.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

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

`--[no]xml:default_values` default: "false"
:   If true, rule attributes whose value is not explicitly specified in the BUILD file are printed; otherwise they are omitted.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]xml:line_numbers` default: "true"
:   If true, XML output contains line numbers. Disabling this option may make diffs easier to read. This option is only applicable to --output=xml.
      
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

`--experimental_repository_resolved_file=<a string>` default: ""
:   If non-empty, write a Starlark value with the resolved information of all Starlark repository rules that were executed.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--remote_print_execution_messages=<failure, success or all>` default: "failure"
:   Choose when to print remote execution messages. Valid values are `failure`, to print only on failures, `success` to print only on successes and `all` to print always.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

Options specifying or altering a generic input to a Bazel command that does not fall into other categories.:

`--experimental_resolved_file_instead_of_workspace=<a string>` default: ""
:   If non-empty read the specified resolved file instead of the WORKSPACE file
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Remote caching and execution options:

`--experimental_circuit_breaker_strategy=<failure>` default: see description
:   Specifies the strategy for the circuit breaker to use. Available strategies are "failure". On invalid value for the option the behavior same as the option is not set.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--experimental_downloader_config=<a string>` default: see description
:   Specify a file to configure the remote downloader with. This file consists of lines, each of which starts with a directive (`allow`, `block` or `rewrite`) followed by either a host name (for `allow` and `block`) or two patterns, one to match against, and one to use as a substitute URL, with back-references starting from `$1`. It is possible for multiple `rewrite` directives for the same URL to be give, and in this case multiple URLs will be returned.

`--[no]experimental_guard_against_concurrent_changes` default: "false"
:   Turn this off to disable checking the ctime of input files of an action before uploading it to a remote cache. There may be cases where the Linux kernel delays writing of files, which could cause false positives.

`--experimental_remote_build_event_upload=<all or minimal>` default: "all"
:   If set to 'all', all local outputs referenced by BEP are uploaded to remote cache.
    If set to 'minimal', local outputs referenced by BEP are not uploaded to the remote cache, except for files that are important to the consumers of BEP (e.g. test logs and timing profile). bytestream:// scheme is always used for the uri of files even if they are missing from remote cache.
    Default to 'all'.

`--[no]experimental_remote_cache_async` default: "false"
:   If true, remote cache I/O will happen in the background instead of taking place as the part of a spawn.

`--[no]experimental_remote_cache_compression` default: "false"
:   If enabled, compress/decompress cache blobs with zstd.

`--experimental_remote_capture_corrupted_outputs=<a path>` default: see description
:   A path to a directory where the corrupted outputs will be captured to.

`--[no]experimental_remote_discard_merkle_trees` default: "false"
:   If set to true, discard in-memory copies of the input root's Merkle tree and associated input mappings during calls to GetActionResult() and Execute(). This reduces memory usage significantly, but does require Bazel to recompute them upon remote cache misses and retries.

`--experimental_remote_downloader=<a string>` default: see description
:   A Remote Asset API endpoint URI, to be used as a remote download proxy. The supported schemas are grpc, grpcs (grpc with TLS enabled) and unix (local UNIX sockets). If no schema is provided Bazel will default to grpcs. See: https://github.com/bazelbuild/remote-apis/blob/master/build/bazel/remote/asset/v1/remote\_asset.proto

`--[no]experimental_remote_downloader_local_fallback` default: "false"
:   Whether to fall back to the local downloader if remote downloader fails.

`--[no]experimental_remote_execution_keepalive` default: "false"
:   Whether to use keepalive for remote execution calls.

`--experimental_remote_failure_rate_threshold=<an integer in 0-100 range>` default: "10"
:   Sets the allowed number of failure rate in percentage for a specific time window after which it stops calling to the remote cache/executor. By default the value is 10. Setting this to 0 means no limitation.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--experimental_remote_failure_window_interval=<An immutable length of time.>` default: "60s"
:   The interval in which the failure rate of the remote requests are computed. On zero or negative value the failure duration is computed the whole duration of the execution.Following units can be used: Days (d), hours (h), minutes (m), seconds (s), and milliseconds (ms). If the unit is omitted, the value is interpreted as seconds.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_remote_mark_tool_inputs` default: "false"
:   If set to true, Bazel will mark inputs as tool inputs for the remote executor. This can be used to implement remote persistent workers.

`--[no]experimental_remote_merkle_tree_cache` default: "false"
:   If set to true, Merkle tree calculations will be memoized to improve the remote cache hit checking speed. The memory foot print of the cache is controlled by --experimental\_remote\_merkle\_tree\_cache\_size.

`--experimental_remote_merkle_tree_cache_size=<a long integer>` default: "1000"
:   The number of Merkle trees to memoize to improve the remote cache hit checking speed. Even though the cache is automatically pruned according to Java's handling of soft references, out-of-memory errors can occur if set too high. If set to 0 the cache size is unlimited. Optimal value varies depending on project's size. Default to 1000.

`--[no]experimental_remote_require_cached` default: "false"
:   If set to true, enforce that all actions that can run remotely are cached, or else fail the build. This is useful to troubleshoot non-determinism issues as it allows checking whether actions that should be cached are actually cached without spuriously injecting new results into the cache.

`--[no]incompatible_remote_build_event_upload_respect_no_cache` default: "false"
:   If set to true, outputs referenced by BEP are not uploaded to remote cache if the generating action cannot be cached remotely.

`--[no]incompatible_remote_downloader_send_all_headers` default: "true"
:   Whether to send all values of a multi-valued header to the remote downloader instead of just the first.
      
    Tags:
    [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remote_output_paths_relative_to_input_root` default: "false"
:   If set to true, output paths are relative to input root instead of working directory.
      
    Tags:
    [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remote_results_ignore_disk` default: "true"
:   If set to true, --noremote\_upload\_local\_results and --noremote\_accept\_cached will not apply to the disk cache. If a combined cache is used:
    --noremote\_upload\_local\_results will cause results to be written to the disk cache, but not uploaded to the remote cache.
    --noremote\_accept\_cached will result in Bazel checking for results in the disk cache, but not in the remote cache.
    no-remote-exec actions can hit the disk cache.
    See #8216 for details.
      
    Tags:
    [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remote_use_new_exit_code_for_lost_inputs` default: "false"
:   If set to true, Bazel will use new exit code 39 instead of 34 if remote cache evicts blobs during the build.
      
    Tags:
    [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]remote_accept_cached` default: "true"
:   Whether to accept remotely cached action results.

`--remote_bytestream_uri_prefix=<a string>` default: see description
:   The hostname and instance name to be used in bytestream:// URIs that are written into build event streams. This option can be set when builds are performed using a proxy, which causes the values of --remote\_executor and --remote\_instance\_name to no longer correspond to the canonical name of the remote execution service. When not set, it will default to "${hostname}/${instance\_name}".

`--remote_cache=<a string>` default: see description
:   A URI of a caching endpoint. The supported schemas are http, https, grpc, grpcs (grpc with TLS enabled) and unix (local UNIX sockets). If no schema is provided Bazel will default to grpcs. Specify grpc://, http:// or unix: schema to disable TLS. See https://bazel.build/remote/caching

`--remote_cache_header=<a 'name=value' assignment>` multiple uses are accumulated
:   Specify a header that will be included in cache requests: --remote\_cache\_header=Name=Value. Multiple headers can be passed by specifying the flag multiple times. Multiple values for the same name will be converted to a comma-separated list.

`--remote_default_exec_properties=<a 'name=value' assignment>` multiple uses are accumulated
:   Set the default exec properties to be used as the remote execution platform if an execution platform does not already set exec\_properties.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--remote_default_platform_properties=<a string>` default: ""
:   Set the default platform properties to be set for the remote execution API, if the execution platform does not already set remote\_execution\_properties. This value will also be used if the host platform is selected as the execution platform for remote execution.

`--remote_downloader_header=<a 'name=value' assignment>` multiple uses are accumulated
:   Specify a header that will be included in remote downloader requests: --remote\_downloader\_header=Name=Value. Multiple headers can be passed by specifying the flag multiple times. Multiple values for the same name will be converted to a comma-separated list.

`--remote_exec_header=<a 'name=value' assignment>` multiple uses are accumulated
:   Specify a header that will be included in execution requests: --remote\_exec\_header=Name=Value. Multiple headers can be passed by specifying the flag multiple times. Multiple values for the same name will be converted to a comma-separated list.

`--remote_execution_priority=<an integer>` default: "0"
:   The relative priority of actions to be executed remotely. The semantics of the particular priority values are server-dependent.

`--remote_executor=<a string>` default: see description
:   HOST or HOST:PORT of a remote execution endpoint. The supported schemas are grpc, grpcs (grpc with TLS enabled) and unix (local UNIX sockets). If no schema is provided Bazel will default to grpcs. Specify grpc:// or unix: schema to disable TLS.

`--remote_grpc_log=<a path>` default: see description
:   If specified, a path to a file to log gRPC call related details. This log consists of a sequence of serialized com.google.devtools.build.lib.remote.logging.RemoteExecutionLog.LogEntry protobufs with each message prefixed by a varint denoting the size of the following serialized protobuf message, as performed by the method LogEntry.writeDelimitedTo(OutputStream).

`--remote_header=<a 'name=value' assignment>` multiple uses are accumulated
:   Specify a header that will be included in requests: --remote\_header=Name=Value. Multiple headers can be passed by specifying the flag multiple times. Multiple values for the same name will be converted to a comma-separated list.

`--remote_instance_name=<a string>` default: ""
:   Value to pass as instance\_name in the remote execution API.

`--[no]remote_local_fallback` default: "false"
:   Whether to fall back to standalone local execution strategy if remote execution fails.

`--remote_local_fallback_strategy=<a string>` default: "local"
:   No-op, deprecated. See https://github.com/bazelbuild/bazel/issues/7480 for details.

`--remote_max_connections=<an integer>` default: "100"
:   Limit the max number of concurrent connections to remote cache/executor. By default the value is 100. Setting this to 0 means no limitation.
    For HTTP remote cache, one TCP connection could handle one request at one time, so Bazel could make up to --remote\_max\_connections concurrent requests.
    For gRPC remote cache/executor, one gRPC channel could usually handle 100+ concurrent requests, so Bazel could make around `--remote\_max\_connections \* 100` concurrent requests.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--remote_proxy=<a string>` default: see description
:   Connect to the remote cache through a proxy. Currently this flag can only be used to configure a Unix domain socket (unix:/path/to/socket).

`--remote_result_cache_priority=<an integer>` default: "0"
:   The relative priority of remote actions to be stored in remote cache. The semantics of the particular priority values are server-dependent.

`--remote_retries=<an integer>` default: "5"
:   The maximum number of attempts to retry a transient error. If set to 0, retries are disabled.

`--remote_retry_max_delay=<An immutable length of time.>` default: "5s"
:   The maximum backoff delay between remote retry attempts. Following units can be used: Days (d), hours (h), minutes (m), seconds (s), and milliseconds (ms). If the unit is omitted, the value is interpreted as seconds.

`--remote_timeout=<An immutable length of time.>` default: "60s"
:   The maximum amount of time to wait for remote execution and cache calls. For the REST cache, this is both the connect and the read timeout. Following units can be used: Days (d), hours (h), minutes (m), seconds (s), and milliseconds (ms). If the unit is omitted, the value is interpreted as seconds.

`--[no]remote_upload_local_results` default: "true"
:   Whether to upload locally executed action results to the remote cache if the remote cache supports it and the user is authorized to do so.

`--[no]remote_verify_downloads` default: "true"
:   If set to true, Bazel will compute the hash sum of all remote downloads and discard the remotely cached values if they don't match the expected value.

Miscellaneous options, not otherwise categorized.:

`--credential_helper=<Path to a credential helper. It may be absolute, relative to the PATH environment variable, or %workspace%-relative. The path be optionally prefixed by a scope followed by an '='. The scope is a domain name, optionally with a single leading '*' wildcard component. A helper applies to URIs matching its scope, with more specific scopes preferred. If a helper has no scope, it applies to every URI.>` multiple uses are accumulated
:   Configures a credential helper to use for retrieving authorization credentials for repository fetching, remote caching and execution, and the build event service.
    Credentials supplied by a helper take precedence over credentials supplied by --google\_default\_credentials, --google\_credentials, a .netrc file, or the auth parameter to repository\_ctx.download and repository\_ctx.download\_and\_extract.
    May be specified multiple times to set up multiple helpers.
    See https://github.com/bazelbuild/proposals/blob/main/designs/2022-06-07-bazel-credential-helpers.md for details.

`--credential_helper_cache_duration=<An immutable length of time.>` default: "30m"
:   The duration for which credentials supplied by a credential helper are cached.
    Invoking with a different value will adjust the lifetime of preexisting entries; pass zero to clear the cache. A clean command always clears the cache, regardless of this flag.

`--credential_helper_timeout=<An immutable length of time.>` default: "10s"
:   Configures the timeout for a credential helper.
    Credential helpers failing to respond within this timeout will fail the invocation.

`--deleted_packages=<comma-separated list of package names>` default: ""
:   A comma-separated list of names of packages which the build system will consider non-existent, even if they are visible somewhere on the package path.
    Use this option when deleting a subpackage 'x/y' of an existing package 'x'. For example, after deleting x/y/BUILD in your client, the build system may complain if it encounters a label '//x:y/z' if that is still provided by another package\_path entry. Specifying --deleted\_packages x/y avoids this problem.

`--disk_cache=<a path>` default: see description
:   A path to a directory where Bazel can read and write actions and action outputs. If the directory does not exist, it will be created.

`--google_auth_scopes=<comma-separated list of options>` default: "https://www.googleapis.com/auth/cloud-platform"
:   A comma-separated list of Google Cloud authentication scopes.

`--google_credentials=<a string>` default: see description
:   Specifies the file to get authentication credentials from. See https://cloud.google.com/docs/authentication for details.

`--[no]google_default_credentials` default: "false"
:   Whether to use 'Google Application Default Credentials' for authentication. See https://cloud.google.com/docs/authentication for details. Disabled by default.

`--grpc_keepalive_time=<An immutable length of time.>` default: see description
:   Configures keep-alive pings for outgoing gRPC connections. If this is set, then Bazel sends pings after this much time of no read operations on the connection, but only if there is at least one pending gRPC call. Times are treated as second granularity; it is an error to set a value less than one second. By default, keep-alive pings are disabled. You should coordinate with the service owner before enabling this setting. For example to set a value of 30 seconds to this flag, it should be done as this --grpc\_keepalive\_time=30s

`--grpc_keepalive_timeout=<An immutable length of time.>` default: "20s"
:   Configures a keep-alive timeout for outgoing gRPC connections. If keep-alive pings are enabled with --grpc\_keepalive\_time, then Bazel times out a connection if it does not receive a ping reply after this much time. Times are treated as second granularity; it is an error to set a value less than one second. If keep-alive pings are disabled, then this setting is ignored.

`--override_repository=<an equals-separated mapping of repository name to path>` multiple uses are accumulated
:   Override a repository with a local path in the form of <repository name>=<path>. If the given path is an absolute path, it will be used as it is. If the given path is a relative path, it is relative to the current working directory. If the given path starts with '%workspace%, it is relative to the workspace root, which is the output of `bazel info workspace`

`--package_path=<colon-separated list of options>` default: "%workspace%"
:   A colon-separated list of where to look for packages. Elements beginning with '%workspace%' are relative to the enclosing workspace. If omitted or empty, the default is the output of 'bazel info default-package-path'.

`--[no]show_loading_progress` default: "true"
:   If enabled, causes Bazel to print "Loading package:" messages.

`--tls_certificate=<a string>` default: see description
:   Specify a path to a TLS certificate that is trusted to sign server certificates.

`--tls_client_certificate=<a string>` default: see description
:   Specify the TLS client certificate to use; you also need to provide a client key to enable client authentication.

`--tls_client_key=<a string>` default: see description
:   Specify the TLS client key to use; you also need to provide a client certificate to enable client authentication.
