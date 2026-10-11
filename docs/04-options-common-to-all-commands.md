## Options Common to all Commands

Options that control build execution:

`--experimental_oom_more_eagerly_threshold=<an integer>` default: "100"
:   If this flag is set to a value less than 100, Bazel will OOM if, after two full GC's, more than this percentage of the (old gen) heap is still occupied.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--experimental_ui_max_stdouterr_bytes=<an integer in (-1)-1073741819 range>` default: "1048576"
:   The maximum size of the stdout / stderr files that will be printed to the console. -1 implies no limit.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

Options that let the user configure the intended output, affecting its value, as opposed to its existence:

`--repo_env=<a 'name=value' assignment with an optional value part>` multiple uses are accumulated
:   Specifies additional environment variables to be available only for repository rules. Note that repository rules see the full environment anyway, but in this way configuration information can be passed to repositories through options without invalidating the action graph.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES)

Options that affect how strictly Bazel enforces valid build inputs (rule definitions, flag combinations, etc.):

`--[no]check_bzl_visibility` default: "true"
:   If disabled, .bzl load visibility errors are demoted to warnings.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

This option affects semantics of the Starlark language or the build API accessible to BUILD files, .bzl files, or WORKSPACE files.:

`--[no]enable_bzlmod` default: "false"
:   If true, enables the Bzlmod dependency management system, taking precedence over WORKSPACE. See https://bazel.build/docs/bzlmod for more information.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_action_resource_set` default: "true"
:   If set to true, ctx.actions.run() and ctx.actions.run\_shell() accept a resource\_set parameter for local execution. Otherwise it will default to 250 MB for memory and 1 cpu.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_allow_tags_propagation` default: "false"
:   If set to true, tags will be propagated from a target to the actions' execution requirements; otherwise tags are not propagated. See https://github.com/bazelbuild/bazel/issues/8830 for details.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_analysis_test_call` default: "true"
:   If set to true, analysis\_test native call is available.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_bzl_visibility` default: "true"
:   If enabled, adds a `visibility()` function that .bzl files may call during top-level evaluation to set their visibility for the purpose of load() statements.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_cc_shared_library` default: "false"
:   If set to true, rule attributes and Starlark API methods needed for the rule cc\_shared\_library will be available
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_disable_external_package` default: "false"
:   If set to true, the auto-generated //external package will not be available anymore. Bazel will still be unable to parse the file 'external/BUILD', but globs reaching into external/ from the unnamed package will work.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_enable_android_migration_apis` default: "false"
:   If set to true, enables the APIs required to support the Android Starlark migration.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--[no]experimental_get_fixed_configured_action_env` default: "false"
:   If enabled, action.env will also return fixed environment variables specified through features configuration.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_google_legacy_api` default: "false"
:   If set to true, exposes a number of experimental pieces of Starlark build API pertaining to Google legacy code.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_isolated_extension_usages` default: "false"
:   If true, enables the <code>isolate</code> parameter in the <a href="https://bazel.build/rules/lib/globals/module#use\_extension"><code>use\_extension</code></a> function.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_lazy_template_expansion` default: "true"
:   If set to true, ctx.actions.expand\_template() accepts a TemplateDict parameter for deferred evaluation of substitution values.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_platforms_api` default: "false"
:   If set to true, enables a number of platform-related Starlark APIs useful for debugging.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_repo_remote_exec` default: "false"
:   If set to true, repository\_rule gains some remote execution capabilities.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_sibling_repository_layout` default: "false"
:   If set to true, non-main repositories are planted as symlinks to the main repository in the execution root. That is, all repositories are direct children of the $output\_base/execution\_root directory. This has the side effect of freeing up $output\_base/execution\_root/\_\_main\_\_/external for the real top-level 'external' directory.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]incompatible_always_check_depset_elements` default: "true"
:   Check the validity of elements added to depsets, in all constructors. Elements must be immutable, but historically the depset(direct=...) constructor forgot to check. Use tuples instead of lists in depset elements. See https://github.com/bazelbuild/bazel/issues/10313 for details.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_depset_for_libraries_to_link_getter` default: "true"
:   When true, Bazel no longer returns a list from linking\_context.libraries\_to\_link but returns a depset instead.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disable_objc_library_transition` default: "false"
:   Disable objc\_library's custom transition and inherit from the top level target instead
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disable_starlark_host_transitions` default: "false"
:   If set to true, rule attributes cannot set 'cfg = "host"'. Rules should set 'cfg = "exec"' instead.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disable_target_provider_fields` default: "false"
:   If set to true, disable the ability to access providers on 'target' objects via field syntax. Use provider-key syntax instead. For example, instead of using `ctx.attr.dep.my\_info` to access `my\_info` from inside a rule implementation function, use `ctx.attr.dep[MyInfo]`. See https://github.com/bazelbuild/bazel/issues/9014 for details.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disallow_empty_glob` default: "false"
:   If set to true, the default value of the `allow\_empty` argument of glob() is False.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disallow_legacy_javainfo` default: "true"
:   Deprecated. No-op.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disallow_struct_provider_syntax` default: "false"
:   If set to true, rule implementation functions may not return a struct. They must instead return a list of provider instances.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_existing_rules_immutable_view` default: "true"
:   If set to true, native.existing\_rule and native.existing\_rules return lightweight immutable view objects instead of mutable dicts.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_fail_on_unknown_attributes` default: "false"
:   If enabled, targets that have unknown attributes set to None fail.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_fix_package_group_reporoot_syntax` default: "true"
:   In package\_group's `packages` attribute, changes the meaning of the value "//..." to refer to all packages in the current repository instead of all packages in any repository. You can use the special value "public" in place of "//..." to obtain the old behavior. This flag requires that --incompatible\_package\_group\_has\_public\_syntax also be enabled.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_java_common_parameters` default: "true"
:   If set to true, the output\_jar, and host\_javabase parameters in pack\_sources and host\_javabase in compile will all be removed.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_merge_fixed_and_default_shell_env` default: "false"
:   If enabled, actions registered with ctx.actions.run and ctx.actions.run\_shell with both 'env' and 'use\_default\_shell\_env = True' specified will use an environment obtained from the default shell environment by overriding with the values passed in to 'env'. If disabled, the value of 'env' is completely ignored in this case.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_new_actions_api` default: "true"
:   If set to true, the API to create actions is only available on `ctx.actions`, not on `ctx`.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_no_attr_license` default: "true"
:   If set to true, disables the function `attr.license`.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_no_implicit_file_export` default: "false"
:   If set, (used) source files are are package private unless exported explicitly. See https://github.com/bazelbuild/proposals/blob/master/designs/2019-10-24-file-visibility.md
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_no_rule_outputs_param` default: "false"
:   If set to true, disables the `outputs` parameter of the `rule()` Starlark function.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_package_group_has_public_syntax` default: "true"
:   In package\_group's `packages` attribute, allows writing "public" or "private" to refer to all packages or no packages respectively.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_require_linker_input_cc_api` default: "true"
:   If set to true, rule create\_linking\_context will require linker\_inputs instead of libraries\_to\_link. The old getters of linking\_context will also be disabled and just linker\_inputs will be available.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_run_shell_command_string` default: "true"
:   If set to true, the command parameter of actions.run\_shell will only accept string
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_stop_exporting_language_modules` default: "false"
:   If enabled, certain language-specific modules (such as `cc\_common`) are unavailable in user .bzl files and may only be called from their respective rules repositories.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_struct_has_no_methods` default: "false"
:   Disables the to\_json and to\_proto methods of struct, which pollute the struct field namespace. Instead, use json.encode or json.encode\_indent for JSON, or proto.encode\_text for textproto.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_top_level_aspects_require_providers` default: "false"
:   If set to true, the top level aspect will honor its required providers and only run on top level targets whose rules' advertised providers satisfy the required providers of the aspect.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_unambiguous_label_stringification` default: "true"
:   When true, Bazel will stringify the label @//foo:bar to @//foo:bar, instead of //foo:bar. This only affects the behavior of str(), the % operator, and so on; the behavior of repr() is unchanged. See https://github.com/bazelbuild/bazel/issues/15916 for more information.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_use_cc_configure_from_rules_cc` default: "false"
:   When true, Bazel will no longer allow using cc\_configure from @bazel\_tools. Please see https://github.com/bazelbuild/bazel/issues/10134 for details and migration instructions.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_visibility_private_attributes_at_definition` default: "false"
:   If set to true, the visibility of private rule attributes is checked with respect to the rule definition, rather than the rule usage.
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--max_computation_steps=<a long integer>` default: "0"
:   The maximum number of Starlark computation steps that may be executed by a BUILD file (zero means no limit).
      
    Tags:
    [`build_file_semantics`](#effect_tag_BUILD_FILE_SEMANTICS)

`--nested_set_depth_limit=<an integer>` default: "3500"
:   The maximum depth of the graph internal to a depset (also known as NestedSet), above which the depset() constructor will fail.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

Options that trigger optimizations of the build time:

`--[no]incompatible_do_not_split_linking_cmdline` default: "true"
:   When true, Bazel no longer modifies command line flags used for linking, and also doesn't selectively decide which flags go to the param file and which don't. See https://github.com/bazelbuild/bazel/issues/7670 for details.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]keep_state_after_build` default: "true"
:   If false, Blaze will discard the inmemory state from this build when the build finishes. Subsequent builds will not have any incrementality with respect to this one.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--skyframe_high_water_mark_threshold=<an integer>` default: "85"
:   Flag for advanced configuration of Bazel's internal Skyframe engine. If Bazel detects its retained heap percentage usage is at least this threshold, it will drop unnecessary temporary Skyframe state. Tweaking this may let you mitigate wall time impact of GC thrashing, when the GC thrashing is (i) caused by the memory usage of this temporary state and (ii) more costly than reconstituting the state when it is needed.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]track_incremental_state` default: "true"
:   If false, Blaze will not persist data that allows for invalidation and re-evaluation on incremental builds in order to save memory on this build. Subsequent builds will not have any incrementality with respect to this one. Usually you will want to specify --batch when setting this to false.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

Options that affect the verbosity, format or location of logging:

`--[no]announce_rc` default: "false"
:   Whether to announce rc options.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]attempt_to_print_relative_paths` default: "false"
:   When printing the location part of messages, attempt to use a path relative to the workspace directory or one of the directories specified by --package\_path.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--bes_backend=<a string>` default: ""
:   Specifies the build event service (BES) backend endpoint in the form [SCHEME://]HOST[:PORT]. The default is to disable BES uploads. Supported schemes are grpc and grpcs (grpc with TLS enabled). If no scheme is provided, Bazel assumes grpcs.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]bes_check_preceding_lifecycle_events` default: "false"
:   Sets the field check\_preceding\_lifecycle\_events\_present on PublishBuildToolEventStreamRequest which tells BES to check whether it previously received InvocationAttemptStarted and BuildEnqueued events matching the current tool event.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--bes_header=<a 'name=value' assignment>` multiple uses are accumulated
:   Specify a header in NAME=VALUE form that will be included in BES requests. Multiple headers can be passed by specifying the flag multiple times. Multiple values for the same name will be converted to a comma-separated list.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--bes_instance_name=<a string>` default: see description
:   Specifies the instance name under which the BES will persist uploaded BEP. Defaults to null.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--bes_keywords=<comma-separated list of options>` multiple uses are accumulated
:   Specifies a list of notification keywords to be added the default set of keywords published to BES ("command\_name=<command\_name> ", "protocol\_name=BEP"). Defaults to none.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]bes_lifecycle_events` default: "true"
:   Specifies whether to publish BES lifecycle events. (defaults to 'true').
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--bes_oom_finish_upload_timeout=<An immutable length of time.>` default: "10m"
:   Specifies how long bazel should wait for the BES/BEP upload to complete while OOMing. This flag ensures termination when the JVM is severely GC thrashing and cannot make progress on any user thread.
      
    Tags:
    [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--bes_outerr_buffer_size=<an integer>` default: "10240"
:   Specifies the maximal size of stdout or stderr to be buffered in BEP, before it is reported as a progress event. Individual writes are still reported in a single event, even if larger than the specified value up to --bes\_outerr\_chunk\_size.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--bes_outerr_chunk_size=<an integer>` default: "1048576"
:   Specifies the maximal size of stdout or stderr to be sent to BEP in a single message.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--bes_proxy=<a string>` default: see description
:   Connect to the Build Event Service through a proxy. Currently this flag can only be used to configure a Unix domain socket (unix:/path/to/socket).

`--bes_results_url=<a string>` default: ""
:   Specifies the base URL where a user can view the information streamed to the BES backend. Bazel will output the URL appended by the invocation id to the terminal.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--bes_timeout=<An immutable length of time.>` default: "0s"
:   Specifies how long bazel should wait for the BES/BEP upload to complete after the build and tests have finished. A valid timeout is a natural number followed by a unit: Days (d), hours (h), minutes (m), seconds (s), and milliseconds (ms). The default value is '0' which means that there is no timeout.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--build_event_binary_file=<a string>` default: ""
:   If non-empty, write a varint delimited binary representation of representation of the build event protocol to that file. This option implies --bes\_upload\_mode=wait\_for\_upload\_complete.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]build_event_binary_file_path_conversion` default: "true"
:   Convert paths in the binary file representation of the build event protocol to more globally valid URIs whenever possible; if disabled, the file:// uri scheme will always be used
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--build_event_json_file=<a string>` default: ""
:   If non-empty, write a JSON serialisation of the build event protocol to that file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]build_event_json_file_path_conversion` default: "true"
:   Convert paths in the json file representation of the build event protocol to more globally valid URIs whenever possible; if disabled, the file:// uri scheme will always be used
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--build_event_max_named_set_of_file_entries=<an integer>` default: "-1"
:   The maximum number of entries for a single named\_set\_of\_files event; values smaller than 2 are ignored and no event splitting is performed. This is intended for limiting the maximum event size in the build event protocol, although it does not directly control event size. The total event size is a function of the structure of the set as well as the file and uri lengths, which may in turn depend on the hash function.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]build_event_publish_all_actions` default: "false"
:   Whether all actions should be published.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--build_event_text_file=<a string>` default: ""
:   If non-empty, write a textual representation of the build event protocol to that file
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]build_event_text_file_path_conversion` default: "true"
:   Convert paths in the text file representation of the build event protocol to more globally valid URIs whenever possible; if disabled, the file:// uri scheme will always be used
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_announce_profile_path` default: "false"
:   If enabled, adds the JSON profile path to the log.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--[no]experimental_bep_target_summary` default: "false"
:   Whether to publish TargetSummary events.

`--[no]experimental_build_event_expand_filesets` default: "false"
:   If true, expand Filesets in the BEP when presenting output files.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_build_event_fully_resolve_fileset_symlinks` default: "false"
:   If true, fully resolve relative Fileset symlinks in the BEP when presenting output files. Requires --experimental\_build\_event\_expand\_filesets.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_build_event_upload_max_retries=<an integer>` default: "4"
:   The maximum number of times Bazel should retry uploading a build event.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--experimental_build_event_upload_retry_minimum_delay=<An immutable length of time.>` default: "1s"
:   Initial, minimum delay for exponential backoff retries when BEP upload fails. (exponent: 1.6)
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--experimental_build_event_upload_strategy=<a string>` default: see description
:   Selects how to upload artifacts referenced in the build event protocol.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_profile_additional_tasks=<phase, action, action_check, action_lock, action_release, action_update, action_complete, bzlmod, info, create_package, remote_execution, local_execution, scanner, local_parse, upload_time, process_time, remote_queue, remote_setup, fetch, vfs_stat, vfs_dir, vfs_readlink, vfs_md5, vfs_xattr, vfs_delete, vfs_open, vfs_read, vfs_write, vfs_glob, vfs_vmfs_stat, vfs_vmfs_dir, vfs_vmfs_read, wait, thread_name, thread_sort_index, skyframe_eval, skyfunction, critical_path, critical_path_component, handle_gc_notification, action_counts, local_cpu_usage, system_cpu_usage, local_memory_usage, system_memory_usage, system_network_up_usage, system_network_down_usage, workers_memory_usage, system_load_average, starlark_parser, starlark_user_fn, starlark_builtin_fn, starlark_user_compiled_fn, starlark_repository_fn, action_fs_staging, remote_cache_check, remote_download, remote_network, filesystem_traversal, worker_execution, worker_setup, worker_borrow, worker_working, worker_copying_outputs, credential_helper or unknown>` multiple uses are accumulated
:   Specifies additional profile tasks to be included in the profile.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--[no]experimental_profile_include_primary_output` default: "false"
:   Includes the extra "out" attribute in action events that contains the exec path to the action's primary output.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--[no]experimental_profile_include_target_label` default: "false"
:   Includes target label in action events' JSON profile data.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--[no]experimental_stream_log_file_uploads` default: "false"
:   Stream log file uploads directly to the remote storage rather than writing them to disk.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_workspace_rules_log_file=<a path>` default: see description
:   Log certain Workspace Rules events into this file as delimited WorkspaceEvent protos.

`--[no]generate_json_trace_profile` default: "auto"
:   If enabled, Bazel profiles the build and writes a JSON-format profile into a file in the output base. View profile by loading into chrome://tracing. By default Bazel writes the profile for all build-like commands and query.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--[no]heap_dump_on_oom` default: "false"
:   Whether to manually output a heap dump if an OOM is thrown (including OOMs due to --experimental\_oom\_more\_eagerly\_threshold). The dump will be written to <output\_base>/<invocation\_id>.heapdump.hprof. This option effectively replaces -XX:+HeapDumpOnOutOfMemoryError, which has no effect because OOMs are caught and redirected to Runtime#halt.
      
    Tags:
    [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--[no]legacy_important_outputs` default: "true"
:   Use this to suppress generation of the legacy important\_outputs field in the TargetComplete event. important\_outputs are required for Bazel to ResultStore integration.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--logging=<0 <= an integer <= 6>` default: "3"
:   The logging level.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--memory_profile=<a path>` default: see description
:   If set, write memory usage data to the specified file at phase ends and stable heap to master log at end of build.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--memory_profile_stable_heap_parameters=<integers, separated by a comma expected in pairs>` default: "1,0"
:   Tune memory profile's computation of stable heap at end of build. Should be and even number of integers separated by commas. In each pair the first integer is the number of GCs to perform. The second integer in each pair is the number of seconds to wait between GCs. Ex: 2,4,4,0 would 2 GCs with a 4sec pause, followed by 4 GCs with zero second pause
      
    Tags:
    [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--profile=<a path>` default: see description
:   If set, profile Bazel and write data to the specified file. Use bazel analyze-profile to analyze the profile.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--[no]slim_profile` default: "true"
:   Slims down the size of the JSON profile by merging events if the profile gets too large.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--starlark_cpu_profile=<a string>` default: ""
:   Writes into the specified file a pprof profile of CPU usage by all Starlark threads.
      
    Tags:
    [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--tool_tag=<a string>` default: ""
:   A tool name to attribute this Bazel invocation to.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--ui_event_filters=<Convert list of comma separated event kind to list of filters>` multiple uses are accumulated
:   Specifies which events to show in the UI. It is possible to add or remove events to the default ones using leading +/-, or override the default set completely with direct assignment. The set of supported event kinds include INFO, DEBUG, ERROR and more.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

Miscellaneous options, not otherwise categorized.:

`--build_metadata=<a 'name=value' assignment>` multiple uses are accumulated
:   Custom key-value string pairs to supply in a build event.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--color=<yes, no or auto>` default: "auto"
:   Use terminal controls to colorize output.

`--config=<a string>` multiple uses are accumulated
:   Selects additional config sections from the rc files; for every <command>, it also pulls in the options from <command>:<config> if such a section exists; if this section doesn't exist in any .rc file, Blaze fails with an error. The config sections and flag combinations they are equivalent to are located in the tools/\*.blazerc config files.

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

`--curses=<yes, no or auto>` default: "auto"
:   Use terminal cursor controls to minimize scrolling output.

`--[no]enable_platform_specific_config` default: "false"
:   If true, Bazel picks up host-OS-specific config lines from bazelrc files. For example, if the host OS is Linux and you run bazel build, Bazel picks up lines starting with build:linux. Supported OS identifiers are linux, macos, windows, freebsd, and openbsd. Enabling this flag is equivalent to using --config=linux on Linux, --config=windows on Windows, etc.

`--[no]experimental_skymeld_ui` default: "false"
:   Displays both analysis and execution phase progress when both are running concurrently.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]experimental_windows_watchfs` default: "false"
:   If true, experimental Windows support for --watchfs is enabled. Otherwise --watchfsis a non-op on Windows. Make sure to also enable --watchfs.

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

`--[no]incompatible_disallow_symlink_file_to_dir` default: "true"
:   If set to true, `ctx.actions.symlink` will disallow symlinking a file into a directory.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remove_rule_name_parameter` default: "true"
:   If set to true, `rule` can't be called with the `name` parameter.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]progress_in_terminal_title` default: "false"
:   Show the command progress in the terminal title. Useful to see what bazel is doing when having multiple terminal tabs.

`--[no]show_progress` default: "true"
:   Display progress messages during a build.

`--show_progress_rate_limit=<a double>` default: "0.2"
:   Minimum number of seconds between progress messages in the output.

`--[no]show_timestamps` default: "false"
:   Include timestamps in messages

`--tls_certificate=<a string>` default: see description
:   Specify a path to a TLS certificate that is trusted to sign server certificates.

`--tls_client_certificate=<a string>` default: see description
:   Specify the TLS client certificate to use; you also need to provide a client key to enable client authentication.

`--tls_client_key=<a string>` default: see description
:   Specify the TLS client key to use; you also need to provide a client certificate to enable client authentication.

`--ui_actions_shown=<an integer>` default: "8"
:   Number of concurrent actions shown in the detailed progress bar; each action is shown on a separate line. The progress bar always shows at least one one, all numbers less than 1 are mapped to 1.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]watchfs` default: "false"
:   On Linux/macOS: If true, bazel tries to use the operating system's file watch service for local changes instead of scanning every file for a change. On Windows: this flag currently is a non-op but can be enabled in conjunction with --experimental\_windows\_watchfs. On any OS: The behavior is undefined if your workspace is on a network file system, and files are edited on a remote machine.
