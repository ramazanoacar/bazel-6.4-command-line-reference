## Build Options

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

`--[no]check_up_to_date` default: "false"
:   Don't perform the build, just check if it is up-to-date. If all targets are up-to-date, the build completes successfully. If any step needs to be executed an error is reported and the build fails.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--dynamic_local_execution_delay=<an integer>` default: "1000"
:   How many milliseconds should local execution be delayed, if remote execution was faster during a build at least once?
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--dynamic_local_strategy=<a '[name=]value1[,..,valueN]' assignment>` multiple uses are accumulated
:   The local strategies, in order, to use for the given mnemonic. Passing 'local' as the mnemonic sets the default for unspecified mnemonics. Takes [mnemonic=]local\_strategy[,local\_strategy,...]
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--dynamic_remote_strategy=<a '[name=]value1[,..,valueN]' assignment>` multiple uses are accumulated
:   The remote strategies to use for the given mnemonic. Passing 'remote' as the mnemonic sets the default for unspecified mnemonics. Takes [mnemonic=]remote\_strategy[,remote\_strategy,...]
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--experimental_docker_image=<a string>` default: ""
:   Specify a Docker image name (e.g. "ubuntu:latest") that should be used to execute a sandboxed action when using the docker strategy and the action itself doesn't already have a container-image attribute in its remote\_execution\_properties in the platform description. The value of this flag is passed verbatim to 'docker run', so it supports the same syntax and mechanisms as Docker itself.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_docker_use_customized_images` default: "true"
:   If enabled, injects the uid and gid of the current user into the Docker image before using it. This is required if your build / tests depend on the user having a name and home directory inside the container. This is on by default, but you can disable it in case the automatic image customization feature doesn't work in your case or you know that you don't need it.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_dynamic_exclude_tools` default: "true"
:   When set, targets that are build "for tool" are not subject to dynamic execution. Such targets are extremely unlikely to be built incrementally and thus not worth spending local cycles on.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--experimental_dynamic_local_load_factor=<a double>` default: "0"
:   Controls how much load from dynamic execution to put on the local machine. This flag adjusts how many actions in dynamic execution we will schedule concurrently. It is based on the number of CPUs Blaze thinks is available, which can be controlled with the --local\_cpu\_resources flag.
    If this flag is 0, all actions are scheduled locally immediately. If > 0, the amount of actions scheduled locally is limited by the number of CPUs available. If < 1, the load factor is used to reduce the number of locally scheduled actions when the number of actions waiting to schedule is high. This lessens the load on the local machine in the clean build case, where the local machine does not contribute much.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--experimental_dynamic_slow_remote_time=<An immutable length of time.>` default: "0"
:   If >0, the time a dynamically run action must run remote-only before we prioritize its local execution to avoid remote timeouts. This may hide some problems on the remote execution system. Do not turn this on without monitoring of remote execution issues.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]experimental_enable_docker_sandbox` default: "false"
:   Enable Docker-based sandboxing. This option has no effect if Docker is not installed.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--experimental_persistent_javac`
:   Enable the experimental persistent Java compiler.
      
    Expands to:  
      `--strategy=Javac=worker`  
      `--strategy=JavaIjar=local`  
      `--strategy=JavaDeployJar=local`  
      `--strategy=JavaSourceJar=local`  
      `--strategy=Turbine=local`  
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--experimental_sandbox_async_tree_delete_idle_threads=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` default: "0"
:   If 0, delete sandbox trees as soon as an action completes (causing completion of the action to be delayed). If greater than zero, execute the deletion of such threes on an asynchronous thread pool that has size 1 when the build is running and grows to the size specified by this flag when the server is idle.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--experimental_sandboxfs_path=<a string>` default: "sandboxfs"
:   Path to the sandboxfs binary to use when --experimental\_use\_sandboxfs is true. If a bare name, use the first binary of that name found in the PATH.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_split_xml_generation` default: "true"
:   If this flag is set, and a test action does not generate a test.xml file, then Bazel uses a separate action to generate a dummy test.xml file containing the test log. Otherwise, Bazel generates a test.xml as part of the test action.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--experimental_total_worker_memory_limit_mb=<an integer, or "HOST_RAM", optionally followed by [-|*]<float>.>` default: "0"
:   If this limit is greater than zero idle workers might be killed if the total memory usage of all workers exceed the limit.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]experimental_use_hermetic_linux_sandbox` default: "false"
:   If set to true, do not mount root, only mount whats provided with sandbox\_add\_mount\_pair. Input files will be hardlinked to the sandbox instead of symlinked to from the sandbox. If action input files are located on a filesystem different from the sandbox, then the input files will be copied instead.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_use_sandboxfs` default: "false"
:   Use sandboxfs to create the actions' execroot directories instead of building a symlink tree. If "yes", the binary provided by --experimental\_sandboxfs\_path must be valid and correspond to a supported version of sandboxfs. If "auto", the binary may be missing or not compatible.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_use_windows_sandbox` default: "false"
:   Use Windows sandbox to run actions. If "yes", the binary provided by --experimental\_windows\_sandbox\_path must be valid and correspond to a supported version of sandboxfs. If "auto", the binary may be missing or not compatible.

`--experimental_windows_sandbox_path=<a string>` default: "BazelSandbox.exe"
:   Path to the Windows sandbox binary to use when --experimental\_use\_windows\_sandbox is true. If a bare name, use the first binary of that name found in the PATH.

`--[no]experimental_worker_as_resource` default: "false"
:   If enabled, workers are acquired as resources from ResourceManager.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]experimental_worker_cancellation` default: "false"
:   If enabled, Bazel may send cancellation requests to workers that support them.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_worker_multiplex` default: "true"
:   If enabled, workers that support the experimental multiplexing feature will use that feature.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]experimental_worker_multiplex_sandboxing` default: "false"
:   If enabled, multiplex workers will be sandboxed, using a separate sandbox directory per work request. Only workers that have the 'supports-multiplex-sandboxing' execution requirement will be sandboxed.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_worker_strict_flagfiles` default: "false"
:   If enabled, actions arguments for workers that do not follow the worker specification will cause an error. Worker arguments must have exactly one @flagfile argument as the last of its list of arguments.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--genrule_strategy=<comma-separated list of options>` default: ""
:   Specify how to execute genrules. This flag will be phased out. Instead, use --spawn\_strategy=<value> to control all actions or --strategy=Genrule=<value> to control genrules only.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--high_priority_workers=<a string>` multiple uses are accumulated
:   Mnemonics of workers to run with high priority. When high priority workers are running all other workers are throttled.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]incompatible_remote_dangling_symlinks` default: "true"
:   If set to true and --incompatible\_remote\_symlinks is also true, symlinks in action outputs are allowed to dangle.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_remote_symlinks` default: "true"
:   If set to true, Bazel will represent symlinks in action outputs in the remote caching/execution protocol as such. Otherwise, symlinks will be followed and represented as files or directories. See #6631 for details.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_sandbox_hermetic_tmp` default: "false"
:   If set to true, each Linux sandbox will have its own dedicated empty directory mounted as /tmp rather thansharing /tmp with the host filesystem. Use --sandbox\_add\_mount\_pair=/tmp to keep seeing the host's /tmp in all sandboxes.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]internal_spawn_scheduler` default: "false"
:   Placeholder option so that we can tell in Blaze whether the spawn scheduler was enabled.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--jobs=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` [`-j`] default: "auto"
:   The number of concurrent jobs to run. Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". Values must be between 1 and 5000. Values above 2500 may cause memory issues. "auto" calculates a reasonable default based on host resources.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--[no]keep_going` [`-k`] default: "false"
:   Continue as much as possible after an error. While the target that failed and those that depend on it cannot be analyzed, other prerequisites of these targets can be.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--loading_phase_threads=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` default: "auto"
:   Number of parallel threads to use for the loading/analysis phase.Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". "auto" sets a reasonable default based on host resources. Must be at least 1.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--[no]reuse_sandbox_directories` default: "false"
:   If set to true, directories used by sandboxed non-worker execution may be reused to avoid unnecessary setup costs.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--sandbox_base=<a string>` default: ""
:   Lets the sandbox create its sandbox directories underneath this path. Specify a path on tmpfs (like /run/shm) to possibly improve performance a lot when your build / tests have many input files. Note: You need enough RAM and free space on the tmpfs to hold output and intermediate files generated by running actions.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--[no]sandbox_explicit_pseudoterminal` default: "false"
:   Explicitly enable the creation of pseudoterminals for sandboxed actions. Some linux distributions require setting the group id of the process to 'tty' inside the sandbox in order for pseudoterminals to function. If this is causing issues, this flag can be disabled to enable other groups to be used.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--sandbox_tmpfs_path=<an absolute path>` multiple uses are accumulated
:   For sandboxed actions, mount an empty, writable directory at this absolute path (if supported by the sandboxing implementation, ignored otherwise).
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--spawn_strategy=<comma-separated list of options>` default: ""
:   Specify how spawn actions are executed by default. Accepts a comma-separated list of strategies from highest to lowest priority. For each action Bazel picks the strategy with the highest priority that can execute the action. The default value is "remote,worker,sandboxed,local". See https://blog.bazel.build/2019/06/19/list-strategy.html for details.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--strategy=<a '[name=]value1[,..,valueN]' assignment>` multiple uses are accumulated
:   Specify how to distribute compilation of other spawn actions. Accepts a comma-separated list of strategies from highest to lowest priority. For each action Bazel picks the strategy with the highest priority that can execute the action. The default value is "remote,worker,sandboxed,local". This flag overrides the values set by --spawn\_strategy (and --genrule\_strategy if used with mnemonic Genrule). See https://blog.bazel.build/2019/06/19/list-strategy.html for details.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--strategy_regexp=<a '<RegexFilter>=value[,value]' assignment>` multiple uses are accumulated
:   Override which spawn strategy should be used to execute spawn actions that have descriptions matching a certain regex\_filter. See --per\_file\_copt for details onregex\_filter matching. The first regex\_filter that matches the description is used. This option overrides other flags for specifying strategy. Example: --strategy\_regexp=//foo.\*\.cc,-//foo/bar=local means to run actions using local strategy if their descriptions match //foo.\*.cc but not //foo/bar. Example: --strategy\_regexp='Compiling.\*/bar=local --strategy\_regexp=Compiling=sandboxed will run 'Compiling //foo/bar/baz' with the 'local' strategy, but reversing the order would run it with 'sandboxed'.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--worker_extra_flag=<a 'name=value' assignment>` multiple uses are accumulated
:   Extra command-flags that will be passed to worker processes in addition to --persistent\_worker, keyed by mnemonic (e.g. --worker\_extra\_flag=Javac=--debug.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--worker_max_instances=<[name=]value, where value is an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` multiple uses are accumulated
:   How many instances of a worker process (like the persistent Java compiler) may be launched if you use the 'worker' strategy. May be specified as [name=value] to give a different value per worker mnemonic. Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". 'auto' calculates a reasonable default based on machine capacity. "=value" sets a default for unspecified mnemonics.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--worker_max_multiplex_instances=<[name=]value, where value is an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` multiple uses are accumulated
:   How many WorkRequests a multiplex worker process may receive in parallel if you use the 'worker' strategy with --experimental\_worker\_multiplex. May be specified as [name=value] to give a different value per worker mnemonic. Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". 'auto' calculates a reasonable default based on machine capacity. "=value" sets a default for unspecified mnemonics.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]worker_quit_after_build` default: "false"
:   If enabled, all workers quit after a build is done.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]worker_sandboxing` default: "false"
:   If enabled, workers will be executed in a sandboxed environment.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]worker_verbose` default: "false"
:   If enabled, prints verbose messages when workers are started, shutdown, ...

Options that configure the toolchain used for action execution:

`--[no]incompatible_disable_runtimes_filegroups` default: "false"
:   Deprecated no-op.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`deprecated`](#metadata_tag_DEPRECATED), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_dont_emit_static_libgcc` default: "true"
:   Deprecated no-op.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`deprecated`](#metadata_tag_DEPRECATED), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_linkopts_in_user_link_flags` default: "true"
:   Deprecated no-op.
      
    Tags:
    [`action_command_lines`](#effect_tag_ACTION_COMMAND_LINES), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`deprecated`](#metadata_tag_DEPRECATED), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

Options that control the output of the command:

`--[no]build` default: "true"
:   Execute the build; this is the usual behaviour. Specifying --nobuild causes the build to stop before executing the build actions, returning zero iff the package loading and analysis phases completed successfully; this mode is useful for testing those phases.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_run_validations` default: "true"
:   Use --run\_validations instead.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_use_validation_aspect` default: "false"
:   Whether to run validation actions using aspect (for parallelism with tests).
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--output_groups=<comma-separated list of options>` multiple uses are accumulated
:   A list of comma-separated output group names, each of which optionally prefixed by a + or a -. A group prefixed by + is added to the default set of output groups, while a group prefixed by - is removed from the default set. If at least one group is not prefixed, the default set of output groups is omitted. For example, --output\_groups=+foo,+bar builds the union of the default set, foo, and bar, while --output\_groups=foo,bar overrides the default set such that only foo and bar are built.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]run_validations` default: "true"
:   Whether to run validation actions as part of the build. See https://bazel.build/rules/rules#validation\_actions
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

Options that let the user configure the intended output, affecting its value, as opposed to its existence:

`--aspects=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of aspects to be applied to top-level targets. In the list, if aspect some\_aspect specifies required aspect providers via required\_aspect\_providers, some\_aspect will run after every aspect that was mentioned before it in the aspects list whose advertised providers satisfy some\_aspect required aspect providers. Moreover, some\_aspect will run after all its required aspects specified by requires attribute. some\_aspect will then have access to the values of those aspects' providers. <bzl-file-label>%<aspect\_name>, for example '//tools:my\_def.bzl%my\_aspect', where 'my\_aspect' is a top-level value from a file tools/my\_def.bzl

`--bep_maximum_open_remote_upload_files=<an integer>` default: "-1"
:   Maximum number of open files allowed during BEP artifact upload.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_convenience_symlinks` default: "normal"
:   This flag controls how the convenience symlinks (the symlinks that appear in the workspace after the build) will be managed. Possible values:
    normal (default): Each kind of convenience symlink will be created or deleted, as determined by the build.
    clean: All symlinks will be unconditionally deleted.
    ignore: Symlinks will be left alone.
    log\_only: Generate log messages as if 'normal' were passed, but don't actually perform any filesystem operations (useful for tools).
    Note that only symlinks whose names are generated by the current value of --symlink\_prefix can be affected; if the prefix changes, any pre-existing symlinks will be left alone.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_convenience_symlinks_bep_event` default: "false"
:   This flag controls whether or not we will post the build eventConvenienceSymlinksIdentified to the BuildEventProtocol. If the value is true, the BuildEventProtocol will have an entry for convenienceSymlinksIdentified, listing all of the convenience symlinks created in your workspace. If false, then the convenienceSymlinksIdentified entry in the BuildEventProtocol will be empty.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_multi_cpu=<comma-separated list of options>` multiple uses are accumulated
:   Deprecated. No-op.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

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

`--symlink_prefix=<a string>` default: see description
:   The prefix that is prepended to any of the convenience symlinks that are created after a build. If omitted, the default value is the name of the build tool followed by a hyphen. If '/' is passed, then no symlinks are created and no warning is emitted. Warning: the special functionality for '/' will be deprecated soon; use --experimental\_convenience\_symlinks=ignore instead.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

Options that affect how strictly Bazel enforces valid build inputs (rule definitions, flag combinations, etc.):

`--[no]experimental_docker_privileged` default: "false"
:   If enabled, Bazel will pass the --privileged flag to 'docker run' when running actions. This might be required by your build, but it might also result in reduced hermeticity.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--experimental_repository_hash_file=<a string>` default: ""
:   If non-empty, specifies a file containing a resolved value, against which the repository directory hashes should be verified
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_sandboxfs_map_symlink_targets` default: "false"
:   If true, maps the targets of symbolic links specified as action inputs into the sandbox. This feature exists purely to workaround buggy rules that do not do this on their own and should be removed once all such rules are fixed.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--experimental_verify_repository_rules=<a string>` multiple uses are accumulated
:   If list of repository rules for which the hash of the output directory should be verified, provided a file is specified by --experimental\_repository\_hash\_file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]incompatible_legacy_local_fallback` default: "true"
:   If set to true, enables the legacy implicit fallback from sandboxed to local strategy. This flag will eventually default to false and then become a no-op. Use --strategy, --spawn\_strategy, or --dynamic\_local\_strategy to configure fallbacks instead.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--sandbox_add_mount_pair=<a single path or a 'source:target' pair>` multiple uses are accumulated
:   Add additional path pair to mount in sandbox.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--sandbox_block_path=<a string>` multiple uses are accumulated
:   For sandboxed actions, disallow access to this path.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]sandbox_default_allow_network` default: "true"
:   Allow network access by default for actions; this may not work with all sandboxing implementations.

`--[no]sandbox_fake_hostname` default: "false"
:   Change the current hostname to 'localhost' for sandboxed actions.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]sandbox_fake_username` default: "false"
:   Change the current username to 'nobody' for sandboxed actions.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--sandbox_writable_path=<a string>` multiple uses are accumulated
:   For sandboxed actions, make an existing directory writable in the sandbox (if supported by the sandboxing implementation, ignored otherwise).
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

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

Options that govern the behavior of the test environment or test runner:

`--[no]check_tests_up_to_date` default: "false"
:   Don't run tests, just check if they are up-to-date. If all tests results are up-to-date, the testing completes successfully. If any test needs to be built or executed, an error is reported and the testing fails. This option implies --check\_up\_to\_date behavior.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--flaky_test_attempts=<a positive integer, the string "default", or test_regex@attempts. This flag may be passed more than once>` multiple uses are accumulated
:   Each test will be retried up to the specified number of times in case of any test failure. Tests that required more than one attempt to pass are marked as 'FLAKY' in the test summary. Normally the value specified is just an integer or the string 'default'. If an integer, then all tests will be run up to N times. If 'default', then only a single test attempt will be made for regular tests and three for tests marked explicitly as flaky by their rule (flaky=1 attribute). Alternate syntax: regex\_filter@flaky\_test\_attempts. Where flaky\_test\_attempts is as above and regex\_filter stands for a list of include and exclude regular expression patterns (Also see --runs\_per\_test). Example: --flaky\_test\_attempts=//foo/.\*,-//foo/bar/.\*@3 deflakes all tests in //foo/ except those under foo/bar three times. This option can be passed multiple times. The most recently passed argument that matches takes precedence. If nothing matches, behavior is as if 'default' above.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--local_test_jobs=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` default: "auto"
:   The max number of local test jobs to run concurrently. Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". 0 means local resources will limit the number of local test jobs to run concurrently instead. Setting this greater than the value for --jobs is ineffectual.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]test_keep_going` default: "true"
:   When disabled, any non-passing test will cause the entire build to stop. By default all tests are run, even if some do not pass.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--test_strategy=<a string>` default: ""
:   Specifies which strategy to use when running tests.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--test_tmpdir=<a path>` default: see description
:   Specifies the base temporary directory for 'bazel test' to use.

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

`--[no]announce` default: "false"
:   Deprecated. No-op.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]debug_spawn_scheduler` default: "false"

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

`--[no]experimental_collect_local_sandbox_action_metrics` default: "true"
:   When enabled, execution statistics (such as user and system time) are recorded for locally executed actions which use sandboxing
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_docker_verbose` default: "false"
:   If enabled, Bazel will print more verbose messages about the Docker sandbox strategy.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_materialize_param_files_directly` default: "false"
:   If materializing param files, do so with direct writes to disk.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_record_metrics_for_all_mnemonics` default: "false"
:   By default the number of action types is limited to the 20 mnemonics with the largest number of executed actions. Setting this option will write statistics for all mnemonics.

`--experimental_repository_resolved_file=<a string>` default: ""
:   If non-empty, write a Starlark value with the resolved information of all Starlark repository rules that were executed.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_stream_log_file_uploads` default: "false"
:   Stream log file uploads directly to the remote storage rather than writing them to disk.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--explain=<a path>` default: see description
:   Causes the build system to explain each executed step of the build. The explanation is written to the specified log file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]legacy_important_outputs` default: "true"
:   Use this to suppress generation of the legacy important\_outputs field in the TargetComplete event. important\_outputs are required for Bazel to ResultStore integration.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]materialize_param_files` default: "false"
:   Writes intermediate parameter files to output tree even when using remote action execution. Useful when debugging actions. This is implied by --subcommands and --verbose\_failures.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--max_config_changes_to_show=<an integer>` default: "3"
:   When discarding the analysis cache due to a change in the build options, displays up to the given number of changed option names. If the number given is -1, all changed options will be displayed.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--max_test_output_bytes=<an integer>` default: "-1"
:   Specifies maximum per-test-log size that can be emitted when --test\_output is 'errors' or 'all'. Useful for avoiding overwhelming the output with excessively noisy test output. The test header is included in the log size. Negative values imply no limit. Output is all or nothing.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER), [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`execution`](#effect_tag_EXECUTION)

`--output_filter=<a valid Java regular expression>` default: see description
:   Only shows warnings for rules with a name matching the provided regular expression.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--progress_report_interval=<an integer in 0-3600 range>` default: "0"
:   The number of seconds to between reports on still running jobs. The default value 0 means the first report will be printed after 10 seconds, then 30 seconds and after that progress is reported once every minute. When --curses is enabled, progress is reported every second.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--remote_print_execution_messages=<failure, success or all>` default: "failure"
:   Choose when to print remote execution messages. Valid values are `failure`, to print only on failures, `success` to print only on successes and `all` to print always.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]sandbox_debug` default: "false"
:   Enables debugging features for the sandboxing feature. This includes two things: first, the sandbox root contents are left untouched after a build (and if sandboxfs is in use, the file system is left mounted); and second, prints extra debugging information on execution. This can help developers of Bazel or Starlark rules with debugging failures due to missing input files, etc.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--show_result=<an integer>` default: "1"
:   Show the results of the build. For each target, state whether or not it was brought up-to-date, and if so, a list of output files that were built. The printed files are convenient strings for copy+pasting to the shell, to execute them.
    This option requires an integer argument, which is the threshold number of targets above which result information is not printed. Thus zero causes suppression of the message and MAX\_INT causes printing of the result to occur always. The default is one.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]subcommands` [`-s`] default: "false"
:   Display the subcommands executed during a build. Related flags: --execution\_log\_json\_file, --execution\_log\_binary\_file (for logging subcommands to a file in a tool-friendly format).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--test_output=<summary, errors, all or streamed>` default: "summary"
:   Specifies desired output mode. Valid values are 'summary' to output only test status summary, 'errors' to also print test logs for failed tests, 'all' to print logs for all tests and 'streamed' to output logs for all tests in real time (this will force tests to be executed locally one at a time regardless of --test\_strategy value).
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER), [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`execution`](#effect_tag_EXECUTION)

`--test_summary=<short, terse, detailed, none or testcase>` default: "short"
:   Specifies the desired format of the test summary. Valid values are 'short' to print information only about tests executed, 'terse', to print information only about unsuccessful tests that were run, 'detailed' to print detailed information about failed test cases, 'testcase' to print summary in test case resolution, do not print detailed information about failed test cases and 'none' to omit the summary.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]verbose_explanations` default: "false"
:   Increases the verbosity of the explanations issued if --explain is enabled. Has no effect if --explain is not enabled.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]verbose_failures` default: "false"
:   If a command fails, print out the full command line.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

Options specifying or altering a generic input to a Bazel command that does not fall into other categories.:

`--aspects_parameters=<a 'name=value' assignment>` multiple uses are accumulated
:   Specifies the values of the command-line aspects parameters. Each parameter value is specified via <param\_name>=<param\_value>, for example 'my\_param=my\_val' where 'my\_param' is a parameter of some aspect in --aspects list or required by an aspect in the list. This option can be used multiple times. However, it is not allowed to assign values to the same parameter more than once.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--experimental_resolved_file_instead_of_workspace=<a string>` default: ""
:   If non-empty read the specified resolved file instead of the WORKSPACE file
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--target_pattern_file=<a string>` default: ""
:   If set, build will read patterns from the file named here, rather than on the command line. It is an error to specify a file here as well as command-line patterns.
      
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

`--experimental_remote_cache_eviction_retries=<an integer>` default: "0"
:   The maximum number of attempts to retry if the build encountered remote cache eviction error. A non-zero value will implicitly set --incompatible\_remote\_use\_new\_exit\_code\_for\_lost\_inputs to true. A new invocation id will be generated for each attempt. If you generate invocation id and provide it to Bazel with --invocation\_id, you should not use this flag. Instead, set flag --incompatible\_remote\_use\_new\_exit\_code\_for\_lost\_inputs and check for the exit code 39.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

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

`--[no]allow_analysis_cache_discard` default: "true"
:   If discarding the analysis cache due to a change in the build system, setting this option to false will cause bazel to exit, rather than continuing with the build. This option has no effect when 'discard\_analysis\_cache' is also set.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--auto_output_filter=<none, all, packages or subpackages>` default: "none"
:   If --output\_filter is not specified, then the value for this option is used create a filter automatically. Allowed values are 'none' (filter nothing / show everything), 'all' (filter everything / show nothing), 'packages' (include output from rules in packages mentioned on the Blaze command line), and 'subpackages' (like 'packages', but also include subpackages). For the 'packages' and 'subpackages' values //java/foo and //javatests/foo are treated as one package)'.

`--[no]build_manual_tests` default: "false"
:   Forces test targets tagged 'manual' to be built. 'manual' tests are excluded from processing. This option forces them to be built (but not executed).

`--build_tag_filters=<comma-separated list of options>` default: ""
:   Specifies a comma-separated list of tags. Each tag can be optionally preceded with '-' to specify excluded tags. Only those targets will be built that contain at least one included tag and do not contain any excluded tags. This option does not affect the set of tests executed with the 'test' command; those are be governed by the test filtering options, for example '--test\_tag\_filters'

`--[no]build_tests_only` default: "false"
:   If specified, only \*\_test and test\_suite rules will be built and other targets specified on the command line will be ignored. By default everything that was requested will be built.

`--combined_report=<none or lcov>` default: "none"
:   Specifies desired cumulative coverage report type. At this point only LCOV is supported.

`--[no]compile_one_dependency` default: "false"
:   Compile a single dependency of the argument files. This is useful for syntax checking source files in IDEs, for example, by rebuilding a single target that depends on the source file to detect errors as early as possible in the edit/build/test cycle. This argument affects the way all non-flag arguments are interpreted; instead of being targets to build they are source filenames. For each source filename an arbitrary target that depends on it will be built.

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

`--[no]discard_analysis_cache` default: "false"
:   Discard the analysis cache immediately after the analysis phase completes. Reduces memory usage by ~10%, but makes further incremental builds slower.

`--disk_cache=<a path>` default: see description
:   A path to a directory where Bazel can read and write actions and action outputs. If the directory does not exist, it will be created.

`--embed_label=<a one-line string>` default: ""
:   Embed source control revision or release label in binary

`--execution_log_binary_file=<a path>` default: see description
:   Log the executed spawns into this file as delimited Spawn protos, according to src/main/protobuf/spawn.proto. The log is first written unordered and is then, at the end of the invocation, sorted in a stable order (can be CPU and memory intensive). Related flags: --execution\_log\_json\_file (ordered text json format), --experimental\_execution\_log\_file (unordered binary protobuf format), --subcommands (for displaying subcommands in terminal output).

`--execution_log_json_file=<a path>` default: see description
:   Log the executed spawns into this file as json representation of the delimited Spawn protos, according to src/main/protobuf/spawn.proto. The log is first written unordered and is then, at the end of the invocation, sorted in a stable order (can be CPU and memory intensive). Related flags: Related flags: --execution\_log\_binary\_file (ordered binary protobuf format), --experimental\_execution\_log\_file (unordered binary protobuf format), --subcommands (for displaying subcommands in terminal output).

`--[no]execution_log_sort` default: "true"
:   Whether to sort the execution log. Set to false to improve memory performance, at the cost of producing the log in nondeterministic order.

`--[no]expand_test_suites` default: "true"
:   Expand test\_suite targets into their constituent tests before analysis. When this flag is turned on (the default), negative target patterns will apply to the tests belonging to the test suite, otherwise they will not. Turning off this flag is useful when top-level aspects are applied at command line: then they can analyze test\_suite targets.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--experimental_execution_log_file=<a path>` default: see description
:   Log the executed spawns into this file as delimited Spawn protos, according to src/main/protobuf/spawn.proto. This file is written in order of the execution of the Spawns. Related flags: --execution\_log\_binary\_file (ordered binary protobuf format), --execution\_log\_json\_file (ordered text json format), --subcommands (for displaying subcommands in terminal output).

`--[no]experimental_execution_log_spawn_metrics` default: "false"
:   Include spawn metrics in the executed spawns log.

`--experimental_extra_action_filter=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths>` default: ""
:   Deprecated in favor of aspects. Filters set of targets to schedule extra\_actions for.

`--[no]experimental_extra_action_top_level_only` default: "false"
:   Deprecated in favor of aspects. Only schedules extra\_actions for top level targets.

`--[no]experimental_prioritize_local_actions` default: "true"
:   If set, actions that can only run locally are given first chance at acquiring resources, dynamically run workers get second chance, and dynamically-run standalone actions come last.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--experimental_spawn_scheduler`
:   Enable dynamic execution by running actions locally and remotely in parallel. Bazel spawns each action locally and remotely and picks the one that completes first. If an action supports workers, the local action will be run in the persistent worker mode. To enable dynamic execution for an individual action mnemonic, use the `--internal\_spawn\_scheduler` and `--strategy=<mnemonic>=dynamic` flags instead.
      
    Expands to:  
      `--internal_spawn_scheduler`  
      `--spawn_strategy=dynamic`

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

`--[no]ignore_unsupported_sandboxing` default: "false"
:   Do not print a warning when sandboxed execution is not supported on this system.

`--[no]incompatible_dont_use_javasourceinfoprovider` default: "false"
:   No-op
      
    Tags:
    [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--local_cpu_resources=<an integer, or "HOST_CPUS", optionally followed by [-|*]<float>.>` default: "HOST\_CPUS"
:   Explicitly set the total number of local CPU cores available to Bazel to spend on build actions executed locally. Takes an integer, or "HOST\_CPUS", optionally followed by [-|\*]<float> (eg. HOST\_CPUS\*.5 to use half the available CPU cores).By default, ("HOST\_CPUS"), Bazel will query system configuration to estimate the number of CPU cores available.

`--local_extra_resources=<a named float, 'name=value'>` multiple uses are accumulated
:   Set the number of extra resources available to Bazel. Takes in a string-float pair. Can be used multiple times to specify multiple types of extra resources. Bazel will limit concurrently running actions based on the available extra resources and the extra resources required. Tests can declare the amount of extra resources they need by using a tag of the "resources:<resoucename>:<amount>" format. Available CPU, RAM and resources cannot be set with this flag.

`--local_ram_resources=<an integer, or "HOST_RAM", optionally followed by [-|*]<float>.>` default: "HOST\_RAM\*.67"
:   Explicitly set the total amount of local host RAM (in MB) available to Bazel to spend on build actions executed locally. Takes an integer, or "HOST\_RAM", optionally followed by [-|\*]<float> (eg. HOST\_RAM\*.5 to use half the available RAM). By default, ("HOST\_RAM\*.67"), Bazel will query system configuration to estimate the amount of RAM available and will use 67% of it.

`--local_termination_grace_seconds=<an integer>` default: "15"
:   Time to wait between terminating a local process due to timeout and forcefully shutting it down.

`--override_repository=<an equals-separated mapping of repository name to path>` multiple uses are accumulated
:   Override a repository with a local path in the form of <repository name>=<path>. If the given path is an absolute path, it will be used as it is. If the given path is a relative path, it is relative to the current working directory. If the given path starts with '%workspace%, it is relative to the workspace root, which is the output of `bazel info workspace`

`--package_path=<colon-separated list of options>` default: "%workspace%"
:   A colon-separated list of where to look for packages. Elements beginning with '%workspace%' are relative to the enclosing workspace. If omitted or empty, the default is the output of 'bazel info default-package-path'.

`--[no]show_loading_progress` default: "true"
:   If enabled, causes Bazel to print "Loading package:" messages.

`--test_lang_filters=<comma-separated list of options>` default: ""
:   Specifies a comma-separated list of test languages. Each language can be optionally preceded with '-' to specify excluded languages. Only those test targets will be found that are written in the specified languages. The name used for each language should be the same as the language prefix in the \*\_test rule, e.g. one of 'cc', 'java', 'py', etc. This option affects --build\_tests\_only behavior and the test command.

`--test_size_filters=<comma-separated list of values: small, medium, large or enormous>` default: ""
:   Specifies a comma-separated list of test sizes. Each size can be optionally preceded with '-' to specify excluded sizes. Only those test targets will be found that contain at least one included size and do not contain any excluded sizes. This option affects --build\_tests\_only behavior and the test command.

`--test_tag_filters=<comma-separated list of options>` default: ""
:   Specifies a comma-separated list of test tags. Each tag can be optionally preceded with '-' to specify excluded tags. Only those test targets will be found that contain at least one included tag and do not contain any excluded tags. This option affects --build\_tests\_only behavior and the test command.

`--test_timeout_filters=<comma-separated list of values: short, moderate, long or eternal>` default: ""
:   Specifies a comma-separated list of test timeouts. Each timeout can be optionally preceded with '-' to specify excluded timeouts. Only those test targets will be found that contain at least one included timeout and do not contain any excluded timeouts. This option affects --build\_tests\_only behavior and the test command.

`--tls_certificate=<a string>` default: see description
:   Specify a path to a TLS certificate that is trusted to sign server certificates.

`--tls_client_certificate=<a string>` default: see description
:   Specify the TLS client certificate to use; you also need to provide a client key to enable client authentication.

`--tls_client_key=<a string>` default: see description
:   Specify the TLS client key to use; you also need to provide a client certificate to enable client authentication.

`--workspace_status_command=<path>` default: ""
:   A command invoked at the beginning of the build to provide status information about the workspace in the form of key/value pairs. See the User's Manual for the full specification. Also see tools/buildstamp/get\_workspace\_status for an example.

Options that control build execution:

`--[no]check_up_to_date` default: "false"
:   Don't perform the build, just check if it is up-to-date. If all targets are up-to-date, the build completes successfully. If any step needs to be executed an error is reported and the build fails.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

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

`--[no]experimental_split_xml_generation` default: "true"
:   If this flag is set, and a test action does not generate a test.xml file, then Bazel uses a separate action to generate a dummy test.xml file containing the test log. Otherwise, Bazel generates a test.xml as part of the test action.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_strict_fileset_output` default: "false"
:   If this option is enabled, filesets will treat all output artifacts as regular files. They will not traverse directories or be sensitive to symlinks.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--genrule_strategy=<comma-separated list of options>` default: ""
:   Specify how to execute genrules. This flag will be phased out. Instead, use --spawn\_strategy=<value> to control all actions or --strategy=Genrule=<value> to control genrules only.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--jobs=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` [`-j`] default: "auto"
:   The number of concurrent jobs to run. Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". Values must be between 1 and 5000. Values above 2500 may cause memory issues. "auto" calculates a reasonable default based on host resources.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`execution`](#effect_tag_EXECUTION)

`--[no]keep_going` [`-k`] default: "false"
:   Continue as much as possible after an error. While the target that failed and those that depend on it cannot be analyzed, other prerequisites of these targets can be.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--loading_phase_threads=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` default: "auto"
:   Number of parallel threads to use for the loading/analysis phase.Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". "auto" sets a reasonable default based on host resources. Must be at least 1.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

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

`--spawn_strategy=<comma-separated list of options>` default: ""
:   Specify how spawn actions are executed by default. Accepts a comma-separated list of strategies from highest to lowest priority. For each action Bazel picks the strategy with the highest priority that can execute the action. The default value is "remote,worker,sandboxed,local". See https://blog.bazel.build/2019/06/19/list-strategy.html for details.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--strategy=<a '[name=]value1[,..,valueN]' assignment>` multiple uses are accumulated
:   Specify how to distribute compilation of other spawn actions. Accepts a comma-separated list of strategies from highest to lowest priority. For each action Bazel picks the strategy with the highest priority that can execute the action. The default value is "remote,worker,sandboxed,local". This flag overrides the values set by --spawn\_strategy (and --genrule\_strategy if used with mnemonic Genrule). See https://blog.bazel.build/2019/06/19/list-strategy.html for details.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--strategy_regexp=<a '<RegexFilter>=value[,value]' assignment>` multiple uses are accumulated
:   Override which spawn strategy should be used to execute spawn actions that have descriptions matching a certain regex\_filter. See --per\_file\_copt for details onregex\_filter matching. The first regex\_filter that matches the description is used. This option overrides other flags for specifying strategy. Example: --strategy\_regexp=//foo.\*\.cc,-//foo/bar=local means to run actions using local strategy if their descriptions match //foo.\*.cc but not //foo/bar. Example: --strategy\_regexp='Compiling.\*/bar=local --strategy\_regexp=Compiling=sandboxed will run 'Compiling //foo/bar/baz' with the 'local' strategy, but reversing the order would run it with 'sandboxed'.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

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

`--[no]build` default: "true"
:   Execute the build; this is the usual behaviour. Specifying --nobuild causes the build to stop before executing the build actions, returning zero iff the package loading and analysis phases completed successfully; this mode is useful for testing those phases.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

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

`--[no]experimental_run_validations` default: "true"
:   Use --run\_validations instead.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_save_feature_state` default: "false"
:   Save the state of enabled and requested feautres as an output of compilation.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--[no]experimental_use_validation_aspect` default: "false"
:   Whether to run validation actions using aspect (for parallelism with tests).
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

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

`--output_groups=<comma-separated list of options>` multiple uses are accumulated
:   A list of comma-separated output group names, each of which optionally prefixed by a + or a -. A group prefixed by + is added to the default set of output groups, while a group prefixed by - is removed from the default set. If at least one group is not prefixed, the default set of output groups is omitted. For example, --output\_groups=+foo,+bar builds the union of the default set, foo, and bar, while --output\_groups=foo,bar overrides the default set such that only foo and bar are built.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]run_validations` default: "true"
:   Whether to run validation actions as part of the build. See https://bazel.build/rules/rules#validation\_actions
      
    Tags:
    [`execution`](#effect_tag_EXECUTION), [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

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

`--aspects=<comma-separated list of options>` multiple uses are accumulated
:   Comma-separated list of aspects to be applied to top-level targets. In the list, if aspect some\_aspect specifies required aspect providers via required\_aspect\_providers, some\_aspect will run after every aspect that was mentioned before it in the aspects list whose advertised providers satisfy some\_aspect required aspect providers. Moreover, some\_aspect will run after all its required aspects specified by requires attribute. some\_aspect will then have access to the values of those aspects' providers. <bzl-file-label>%<aspect\_name>, for example '//tools:my\_def.bzl%my\_aspect', where 'my\_aspect' is a top-level value from a file tools/my\_def.bzl

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

`--[no]experimental_convenience_symlinks` default: "normal"
:   This flag controls how the convenience symlinks (the symlinks that appear in the workspace after the build) will be managed. Possible values:
    normal (default): Each kind of convenience symlink will be created or deleted, as determined by the build.
    clean: All symlinks will be unconditionally deleted.
    ignore: Symlinks will be left alone.
    log\_only: Generate log messages as if 'normal' were passed, but don't actually perform any filesystem operations (useful for tools).
    Note that only symlinks whose names are generated by the current value of --symlink\_prefix can be affected; if the prefix changes, any pre-existing symlinks will be left alone.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]experimental_convenience_symlinks_bep_event` default: "false"
:   This flag controls whether or not we will post the build eventConvenienceSymlinksIdentified to the BuildEventProtocol. If the value is true, the BuildEventProtocol will have an entry for convenienceSymlinksIdentified, listing all of the convenience symlinks created in your workspace. If false, then the convenienceSymlinksIdentified entry in the BuildEventProtocol will be empty.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--experimental_multi_cpu=<comma-separated list of options>` multiple uses are accumulated
:   Deprecated. No-op.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`experimental`](#metadata_tag_EXPERIMENTAL)

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

`--symlink_prefix=<a string>` default: see description
:   The prefix that is prepended to any of the convenience symlinks that are created after a build. If omitted, the default value is the name of the build tool followed by a hyphen. If '/' is passed, then no symlinks are created and no warning is emitted. Warning: the special functionality for '/' will be deprecated soon; use --experimental\_convenience\_symlinks=ignore instead.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

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

`--[no]incompatible_config_setting_private_default_visibility` default: "false"
:   If incompatible\_enforce\_config\_setting\_visibility=false, this is a noop. Else, if this flag is false, any config\_setting without an explicit visibility attribute is //visibility:public. If this flag is true, config\_setting follows the same visibility logic as all other rules. See https://github.com/bazelbuild/bazel/issues/12933.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_disallow_legacy_py_provider` default: "true"
:   No-op, will be removed soon.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`incompatible_change`](#metadata_tag_INCOMPATIBLE_CHANGE)

`--[no]incompatible_enforce_config_setting_visibility` default: "true"
:   If true, enforce config\_setting visibility restrictions. If false, every config\_setting is visible to every target. See https://github.com/bazelbuild/bazel/issues/12932.
      
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

`--[no]check_tests_up_to_date` default: "false"
:   Don't run tests, just check if they are up-to-date. If all tests results are up-to-date, the testing completes successfully. If any test needs to be built or executed, an error is reported and the testing fails. This option implies --check\_up\_to\_date behavior.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_android_use_parallel_dex2oat` default: "false"
:   Use dex2oat in parallel to possibly speed up android\_test.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS), [`experimental`](#metadata_tag_EXPERIMENTAL)

`--flaky_test_attempts=<a positive integer, the string "default", or test_regex@attempts. This flag may be passed more than once>` multiple uses are accumulated
:   Each test will be retried up to the specified number of times in case of any test failure. Tests that required more than one attempt to pass are marked as 'FLAKY' in the test summary. Normally the value specified is just an integer or the string 'default'. If an integer, then all tests will be run up to N times. If 'default', then only a single test attempt will be made for regular tests and three for tests marked explicitly as flaky by their rule (flaky=1 attribute). Alternate syntax: regex\_filter@flaky\_test\_attempts. Where flaky\_test\_attempts is as above and regex\_filter stands for a list of include and exclude regular expression patterns (Also see --runs\_per\_test). Example: --flaky\_test\_attempts=//foo/.\*,-//foo/bar/.\*@3 deflakes all tests in //foo/ except those under foo/bar three times. This option can be passed multiple times. The most recently passed argument that matches takes precedence. If nothing matches, behavior is as if 'default' above.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

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

`--local_test_jobs=<an integer, or a keyword ("auto", "HOST_CPUS", "HOST_RAM"), optionally followed by an operation ([-|*]<float>) eg. "auto", "HOST_CPUS*.5">` default: "auto"
:   The max number of local test jobs to run concurrently. Takes an integer, or a keyword ("auto", "HOST\_CPUS", "HOST\_RAM"), optionally followed by an operation ([-|\*]<float>) eg. "auto", "HOST\_CPUS\*.5". 0 means local resources will limit the number of local test jobs to run concurrently instead. Setting this greater than the value for --jobs is ineffectual.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--runs_per_test=<a positive integer or test_regex@runs. This flag may be passed more than once>` multiple uses are accumulated
:   Specifies number of times to run each test. If any of those attempts fail for any reason, the whole test is considered failed. Normally the value specified is just an integer. Example: --runs\_per\_test=3 will run all tests 3 times. Alternate syntax: regex\_filter@runs\_per\_test. Where runs\_per\_test stands for an integer value and regex\_filter stands for a list of include and exclude regular expression patterns (Also see --instrumentation\_filter). Example: --runs\_per\_test=//foo/.\*,-//foo/bar/.\*@3 runs all tests in //foo/ except those under foo/bar three times. This option can be passed multiple times. The most recently passed argument that matches takes precedence. If nothing matches, the test is only run once.

`--test_env=<a 'name=value' assignment with an optional value part>` multiple uses are accumulated
:   Specifies additional environment variables to be injected into the test runner environment. Variables can be either specified by name, in which case its value will be read from the Bazel client environment, or by the name=value pair. This option can be used multiple times to specify several variables. Used only by the 'bazel test' command.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER)

`--[no]test_keep_going` default: "true"
:   When disabled, any non-passing test will cause the entire build to stop. By default all tests are run, even if some do not pass.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--test_strategy=<a string>` default: ""
:   Specifies which strategy to use when running tests.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--test_timeout=<a single integer or comma-separated list of 4 integers>` default: "-1"
:   Override the default test timeout values for test timeouts (in secs). If a single positive integer value is specified it will override all categories. If 4 comma-separated integers are specified, they will override the timeouts for short, moderate, long and eternal (in that order). In either form, a value of -1 tells blaze to use its default timeouts for that category.

`--test_tmpdir=<a path>` default: see description
:   Specifies the base temporary directory for 'bazel test' to use.

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

`--[no]announce` default: "false"
:   Deprecated. No-op.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

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

`--[no]experimental_materialize_param_files_directly` default: "false"
:   If materializing param files, do so with direct writes to disk.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--[no]experimental_stream_log_file_uploads` default: "false"
:   Stream log file uploads directly to the remote storage rather than writing them to disk.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--explain=<a path>` default: see description
:   Causes the build system to explain each executed step of the build. The explanation is written to the specified log file.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]legacy_important_outputs` default: "true"
:   Use this to suppress generation of the legacy important\_outputs field in the TargetComplete event. important\_outputs are required for Bazel to ResultStore integration.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]materialize_param_files` default: "false"
:   Writes intermediate parameter files to output tree even when using remote action execution. Useful when debugging actions. This is implied by --subcommands and --verbose\_failures.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

`--max_config_changes_to_show=<an integer>` default: "3"
:   When discarding the analysis cache due to a change in the build options, displays up to the given number of changed option names. If the number given is -1, all changed options will be displayed.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--max_test_output_bytes=<an integer>` default: "-1"
:   Specifies maximum per-test-log size that can be emitted when --test\_output is 'errors' or 'all'. Useful for avoiding overwhelming the output with excessively noisy test output. The test header is included in the log size. Negative values imply no limit. Output is all or nothing.
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER), [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`execution`](#effect_tag_EXECUTION)

`--output_filter=<a valid Java regular expression>` default: see description
:   Only shows warnings for rules with a name matching the provided regular expression.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--progress_report_interval=<an integer in 0-3600 range>` default: "0"
:   The number of seconds to between reports on still running jobs. The default value 0 means the first report will be printed after 10 seconds, then 30 seconds and after that progress is reported once every minute. When --curses is enabled, progress is reported every second.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--show_result=<an integer>` default: "1"
:   Show the results of the build. For each target, state whether or not it was brought up-to-date, and if so, a list of output files that were built. The printed files are convenient strings for copy+pasting to the shell, to execute them.
    This option requires an integer argument, which is the threshold number of targets above which result information is not printed. Thus zero causes suppression of the message and MAX\_INT causes printing of the result to occur always. The default is one.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]subcommands` [`-s`] default: "false"
:   Display the subcommands executed during a build. Related flags: --execution\_log\_json\_file, --execution\_log\_binary\_file (for logging subcommands to a file in a tool-friendly format).
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--test_output=<summary, errors, all or streamed>` default: "summary"
:   Specifies desired output mode. Valid values are 'summary' to output only test status summary, 'errors' to also print test logs for failed tests, 'all' to print logs for all tests and 'streamed' to output logs for all tests in real time (this will force tests to be executed locally one at a time regardless of --test\_strategy value).
      
    Tags:
    [`test_runner`](#effect_tag_TEST_RUNNER), [`terminal_output`](#effect_tag_TERMINAL_OUTPUT), [`execution`](#effect_tag_EXECUTION)

`--test_summary=<short, terse, detailed, none or testcase>` default: "short"
:   Specifies the desired format of the test summary. Valid values are 'short' to print information only about tests executed, 'terse', to print information only about unsuccessful tests that were run, 'detailed' to print detailed information about failed test cases, 'testcase' to print summary in test case resolution, do not print detailed information about failed test cases and 'none' to omit the summary.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--toolchain_resolution_debug=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths>` default: "-.\*"
:   Print debug information during toolchain resolution. The flag takes a regex, which is checked against toolchain types and specific targets to see which to debug. Multiple regexes may be separated by commas, and then each regex is checked separately. Note: The output of this flag is very complex and will likely only be useful to experts in toolchain resolution.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

`--[no]verbose_explanations` default: "false"
:   Increases the verbosity of the explanations issued if --explain is enabled. Has no effect if --explain is not enabled.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS)

`--[no]verbose_failures` default: "false"
:   If a command fails, print out the full command line.
      
    Tags:
    [`terminal_output`](#effect_tag_TERMINAL_OUTPUT)

Options specifying or altering a generic input to a Bazel command that does not fall into other categories.:

`--aspects_parameters=<a 'name=value' assignment>` multiple uses are accumulated
:   Specifies the values of the command-line aspects parameters. Each parameter value is specified via <param\_name>=<param\_value>, for example 'my\_param=my\_val' where 'my\_param' is a parameter of some aspect in --aspects list or required by an aspect in the list. This option can be used multiple times. However, it is not allowed to assign values to the same parameter more than once.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

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

`--target_pattern_file=<a string>` default: ""
:   If set, build will read patterns from the file named here, rather than on the command line. It is an error to specify a file here as well as command-line patterns.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Remote caching and execution options:

`--experimental_remote_cache_eviction_retries=<an integer>` default: "0"
:   The maximum number of attempts to retry if the build encountered remote cache eviction error. A non-zero value will implicitly set --incompatible\_remote\_use\_new\_exit\_code\_for\_lost\_inputs to true. A new invocation id will be generated for each attempt. If you generate invocation id and provide it to Bazel with --invocation\_id, you should not use this flag. Instead, set flag --incompatible\_remote\_use\_new\_exit\_code\_for\_lost\_inputs and check for the exit code 39.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

Miscellaneous options, not otherwise categorized.:

`--[no]allow_analysis_cache_discard` default: "true"
:   If discarding the analysis cache due to a change in the build system, setting this option to false will cause bazel to exit, rather than continuing with the build. This option has no effect when 'discard\_analysis\_cache' is also set.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--[no]build_manual_tests` default: "false"
:   Forces test targets tagged 'manual' to be built. 'manual' tests are excluded from processing. This option forces them to be built (but not executed).

`--build_tag_filters=<comma-separated list of options>` default: ""
:   Specifies a comma-separated list of tags. Each tag can be optionally preceded with '-' to specify excluded tags. Only those targets will be built that contain at least one included tag and do not contain any excluded tags. This option does not affect the set of tests executed with the 'test' command; those are be governed by the test filtering options, for example '--test\_tag\_filters'

`--[no]build_tests_only` default: "false"
:   If specified, only \*\_test and test\_suite rules will be built and other targets specified on the command line will be ignored. By default everything that was requested will be built.

`--[no]cache_test_results` [`-t`] default: "auto"
:   If set to 'auto', Bazel reruns a test if and only if: (1) Bazel detects changes in the test or its dependencies, (2) the test is marked as external, (3) multiple test runs were requested with --runs\_per\_test, or(4) the test previously failed. If set to 'yes', Bazel caches all test results except for tests marked as external. If set to 'no', Bazel does not cache any test results.

`--[no]compile_one_dependency` default: "false"
:   Compile a single dependency of the argument files. This is useful for syntax checking source files in IDEs, for example, by rebuilding a single target that depends on the source file to detect errors as early as possible in the edit/build/test cycle. This argument affects the way all non-flag arguments are interpreted; instead of being targets to build they are source filenames. For each source filename an arbitrary target that depends on it will be built.

`--deleted_packages=<comma-separated list of package names>` default: ""
:   A comma-separated list of names of packages which the build system will consider non-existent, even if they are visible somewhere on the package path.
    Use this option when deleting a subpackage 'x/y' of an existing package 'x'. For example, after deleting x/y/BUILD in your client, the build system may complain if it encounters a label '//x:y/z' if that is still provided by another package\_path entry. Specifying --deleted\_packages x/y avoids this problem.

`--[no]discard_analysis_cache` default: "false"
:   Discard the analysis cache immediately after the analysis phase completes. Reduces memory usage by ~10%, but makes further incremental builds slower.

`--execution_log_binary_file=<a path>` default: see description
:   Log the executed spawns into this file as delimited Spawn protos, according to src/main/protobuf/spawn.proto. The log is first written unordered and is then, at the end of the invocation, sorted in a stable order (can be CPU and memory intensive). Related flags: --execution\_log\_json\_file (ordered text json format), --experimental\_execution\_log\_file (unordered binary protobuf format), --subcommands (for displaying subcommands in terminal output).

`--execution_log_json_file=<a path>` default: see description
:   Log the executed spawns into this file as json representation of the delimited Spawn protos, according to src/main/protobuf/spawn.proto. The log is first written unordered and is then, at the end of the invocation, sorted in a stable order (can be CPU and memory intensive). Related flags: Related flags: --execution\_log\_binary\_file (ordered binary protobuf format), --experimental\_execution\_log\_file (unordered binary protobuf format), --subcommands (for displaying subcommands in terminal output).

`--[no]execution_log_sort` default: "true"
:   Whether to sort the execution log. Set to false to improve memory performance, at the cost of producing the log in nondeterministic order.

`--[no]expand_test_suites` default: "true"
:   Expand test\_suite targets into their constituent tests before analysis. When this flag is turned on (the default), negative target patterns will apply to the tests belonging to the test suite, otherwise they will not. Turning off this flag is useful when top-level aspects are applied at command line: then they can analyze test\_suite targets.
      
    Tags:
    [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--[no]experimental_cancel_concurrent_tests` default: "false"
:   If true, then Blaze will cancel concurrently running tests on the first successful run. This is only useful in combination with --runs\_per\_test\_detects\_flakes.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loading_and_analysis`](#effect_tag_LOADING_AND_ANALYSIS)

`--experimental_execution_log_file=<a path>` default: see description
:   Log the executed spawns into this file as delimited Spawn protos, according to src/main/protobuf/spawn.proto. This file is written in order of the execution of the Spawns. Related flags: --execution\_log\_binary\_file (ordered binary protobuf format), --execution\_log\_json\_file (ordered text json format), --subcommands (for displaying subcommands in terminal output).

`--[no]experimental_execution_log_spawn_metrics` default: "false"
:   Include spawn metrics in the executed spawns log.

`--experimental_extra_action_filter=<a comma-separated list of regex expressions with prefix '-' specifying excluded paths>` default: ""
:   Deprecated in favor of aspects. Filters set of targets to schedule extra\_actions for.

`--[no]experimental_extra_action_top_level_only` default: "false"
:   Deprecated in favor of aspects. Only schedules extra\_actions for top level targets.

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

`--[no]experimental_prioritize_local_actions` default: "true"
:   If set, actions that can only run locally are given first chance at acquiring resources, dynamically run workers get second chance, and dynamically-run standalone actions come last.
      
    Tags:
    [`execution`](#effect_tag_EXECUTION)

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

`--local_cpu_resources=<an integer, or "HOST_CPUS", optionally followed by [-|*]<float>.>` default: "HOST\_CPUS"
:   Explicitly set the total number of local CPU cores available to Bazel to spend on build actions executed locally. Takes an integer, or "HOST\_CPUS", optionally followed by [-|\*]<float> (eg. HOST\_CPUS\*.5 to use half the available CPU cores).By default, ("HOST\_CPUS"), Bazel will query system configuration to estimate the number of CPU cores available.

`--local_extra_resources=<a named float, 'name=value'>` multiple uses are accumulated
:   Set the number of extra resources available to Bazel. Takes in a string-float pair. Can be used multiple times to specify multiple types of extra resources. Bazel will limit concurrently running actions based on the available extra resources and the extra resources required. Tests can declare the amount of extra resources they need by using a tag of the "resources:<resoucename>:<amount>" format. Available CPU, RAM and resources cannot be set with this flag.

`--local_ram_resources=<an integer, or "HOST_RAM", optionally followed by [-|*]<float>.>` default: "HOST\_RAM\*.67"
:   Explicitly set the total amount of local host RAM (in MB) available to Bazel to spend on build actions executed locally. Takes an integer, or "HOST\_RAM", optionally followed by [-|\*]<float> (eg. HOST\_RAM\*.5 to use half the available RAM). By default, ("HOST\_RAM\*.67"), Bazel will query system configuration to estimate the amount of RAM available and will use 67% of it.

`--local_termination_grace_seconds=<an integer>` default: "15"
:   Time to wait between terminating a local process due to timeout and forcefully shutting it down.

`--package_path=<colon-separated list of options>` default: "%workspace%"
:   A colon-separated list of where to look for packages. Elements beginning with '%workspace%' are relative to the enclosing workspace. If omitted or empty, the default is the output of 'bazel info default-package-path'.

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

`--[no]show_loading_progress` default: "true"
:   If enabled, causes Bazel to print "Loading package:" messages.

`--test_arg=<a string>` multiple uses are accumulated
:   Specifies additional options and arguments that should be passed to the test executable. Can be used multiple times to specify several arguments. If multiple tests are executed, each of them will receive identical arguments. Used only by the 'bazel test' command.

`--test_filter=<a string>` default: see description
:   Specifies a filter to forward to the test framework. Used to limit the tests run. Note that this does not affect which targets are built.

`--test_lang_filters=<comma-separated list of options>` default: ""
:   Specifies a comma-separated list of test languages. Each language can be optionally preceded with '-' to specify excluded languages. Only those test targets will be found that are written in the specified languages. The name used for each language should be the same as the language prefix in the \*\_test rule, e.g. one of 'cc', 'java', 'py', etc. This option affects --build\_tests\_only behavior and the test command.

`--test_result_expiration=<an integer>` default: "-1"
:   This option is deprecated and has no effect.

`--[no]test_runner_fail_fast` default: "false"
:   Forwards fail fast option to the test runner. The test runner should stop execution upon first failure.

`--test_sharding_strategy=<explicit or disabled>` default: "explicit"
:   Specify strategy for test sharding: 'explicit' to only use sharding if the 'shard\_count' BUILD attribute is present. 'disabled' to never use test sharding.

`--test_size_filters=<comma-separated list of values: small, medium, large or enormous>` default: ""
:   Specifies a comma-separated list of test sizes. Each size can be optionally preceded with '-' to specify excluded sizes. Only those test targets will be found that contain at least one included size and do not contain any excluded sizes. This option affects --build\_tests\_only behavior and the test command.

`--test_tag_filters=<comma-separated list of options>` default: ""
:   Specifies a comma-separated list of test tags. Each tag can be optionally preceded with '-' to specify excluded tags. Only those test targets will be found that contain at least one included tag and do not contain any excluded tags. This option affects --build\_tests\_only behavior and the test command.

`--test_timeout_filters=<comma-separated list of values: short, moderate, long or eternal>` default: ""
:   Specifies a comma-separated list of test timeouts. Each timeout can be optionally preceded with '-' to specify excluded timeouts. Only those test targets will be found that contain at least one included timeout and do not contain any excluded timeouts. This option affects --build\_tests\_only behavior and the test command.

`--tool_java_language_version=<a string>` default: "8"
:   The Java language version used to execute the tools that are needed during a build

`--tool_java_runtime_version=<a string>` default: "remotejdk\_11"
:   The Java runtime version used to execute tools during the build

`--[no]use_ijars` default: "true"
:   If enabled, this option causes Java compilation to use interface jars. This will result in faster incremental compilation, but error messages can be different.
