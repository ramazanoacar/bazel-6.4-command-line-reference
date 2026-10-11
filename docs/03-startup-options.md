## Startup Options

Options that appear before the command and are parsed by the client:

`--[no]autodetect_server_javabase` default: "true"
:   When --noautodetect\_server\_javabase is passed, Bazel does not fall back to the local JDK for running the bazel server and instead exits.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]batch` default: "false"
:   If set, Bazel will be run as just a client process without a server, instead of in the standard client/server mode. This is deprecated and will be removed, please prefer shutting down the server explicitly if you wish to avoid lingering servers.
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION), [`deprecated`](#metadata_tag_DEPRECATED)

`--[no]batch_cpu_scheduling` default: "false"
:   Only on Linux; use 'batch' CPU scheduling for Blaze. This policy is useful for workloads that are non-interactive, but do not want to lower their nice value. See 'man 2 sched\_setscheduler'. If false, then Bazel does not perform a system call.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--bazelrc=<path>` default: see description
:   The location of the user .bazelrc file containing default values of Bazel options. /dev/null indicates that all further `--bazelrc`s will be ignored, which is useful to disable the search for a user rc file, e.g. in release builds.
    This option can also be specified multiple times.
    E.g. with `--bazelrc=x.rc --bazelrc=y.rc --bazelrc=/dev/null --bazelrc=z.rc`,
    1) x.rc and y.rc are read.
    2) z.rc is ignored due to the prior /dev/null.
    If unspecified, Bazel uses the first .bazelrc file it finds in the following two locations: the workspace directory, then the user's home directory.
    Note: command line options will always supersede any option in bazelrc.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]block_for_lock` default: "true"
:   When --noblock\_for\_lock is passed, Bazel does not wait for a running command to complete, but instead exits immediately.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--[no]client_debug` default: "false"
:   If true, log debug information from the client to stderr. Changing this option will not cause the server to restart.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`bazel_monitoring`](#effect_tag_BAZEL_MONITORING)

`--connect_timeout_secs=<an integer>` default: "30"
:   The amount of time the client waits for each attempt to connect to the server
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--[no]expand_configs_in_place` default: "true"
:   Changed the expansion of --config flags to be done in-place, as opposed to in a fixed point expansion between normal rc options and command-line specified options.
      
    Tags:
    [`no_op`](#effect_tag_NO_OP), [`deprecated`](#metadata_tag_DEPRECATED)

`--failure_detail_out=<path>` default: see description
:   If set, specifies a location to write a failure\_detail protobuf message if the server experiences a failure and cannot report it via gRPC, as normal. Otherwise, the location will be ${OUTPUT\_BASE}/failure\_detail.rawproto.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]home_rc` default: "true"
:   Whether or not to look for the home bazelrc file at $HOME/.bazelrc
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]idle_server_tasks` default: "true"
:   Run System.gc() when the server is idle
      
    Tags:
    [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE), [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--[no]ignore_all_rc_files` default: "false"
:   Disables all rc files, regardless of the values of other rc-modifying flags, even if these flags come later in the list of startup options.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--io_nice_level={-1,0,1,2,3,4,5,6,7}` default: "-1"
:   Only on Linux; set a level from 0-7 for best-effort IO scheduling using the sys\_ioprio\_set system call. 0 is highest priority, 7 is lowest. The anticipatory scheduler may only honor up to priority 4. If set to a negative value, then Bazel does not perform a system call.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--local_startup_timeout_secs=<an integer>` default: "120"
:   The maximum amount of time the client waits to connect to the server
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--macos_qos_class=<a string>` default: "default"
:   Sets the QoS service class of the bazel server when running on macOS. This flag has no effect on all other platforms but is supported to ensure rc files can be shared among them without changes. Possible values are: user-interactive, user-initiated, default, utility, and background.
      
    Tags:
    [`host_machine_resource_optimizations`](#effect_tag_HOST_MACHINE_RESOURCE_OPTIMIZATIONS)

`--max_idle_secs=<integer>` default: "10800"
:   The number of seconds the build server will wait idling before shutting down. Zero means that the server will never shutdown. This is only read on server-startup, changing this option will not cause the server to restart.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--output_base=<path>` default: see description
:   If set, specifies the output location to which all build output will be written. Otherwise, the location will be ${OUTPUT\_ROOT}/\_blaze\_${USER}/${MD5\_OF\_WORKSPACE\_ROOT}. Note: If you specify a different option from one to the next Bazel invocation for this value, you'll likely start up a new, additional Bazel server. Bazel starts exactly one server per specified output base. Typically there is one output base per workspace - however, with this option you may have multiple output bases per workspace and thereby run multiple builds for the same client on the same machine concurrently. See 'bazel help shutdown' on how to shutdown a Bazel server.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--output_user_root=<path>` default: see description
:   The user-specific directory beneath which all build outputs are written; by default, this is a function of $USER, but by specifying a constant, build outputs can be shared between collaborating users.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]preemptible` default: "false"
:   If true, the command can be preempted if another command is started.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT)

`--server_jvm_out=<path>` default: see description
:   The location to write the server's JVM's output. If unset then defaults to a location in output\_base.
      
    Tags:
    [`affects_outputs`](#effect_tag_AFFECTS_OUTPUTS), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]shutdown_on_low_sys_mem` default: "false"
:   If max\_idle\_secs is set and the build server has been idle for a while, shut down the server when the system is low on free RAM. Linux only.
      
    Tags:
    [`eagerness_to_exit`](#effect_tag_EAGERNESS_TO_EXIT), [`loses_incremental_state`](#effect_tag_LOSES_INCREMENTAL_STATE)

`--[no]system_rc` default: "true"
:   Whether or not to look for the system-wide bazelrc.
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

`--[no]unlimit_coredumps` default: "false"
:   Raises the soft coredump limit to the hard limit to make coredumps of the server (including the JVM) and the client possible under common conditions. Stick this flag in your bazelrc once and forget about it so that you get coredumps when you actually encounter a condition that triggers them.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--[no]watchfs` default: "false"
:   If true, bazel tries to use the operating system's file watch service for local changes instead of scanning every file for a change.
      
    Tags:
    [`deprecated`](#metadata_tag_DEPRECATED)

`--[no]windows_enable_symlinks` default: "false"
:   If true, real symbolic links will be created on Windows instead of file copying. Requires Windows developer mode to be enabled and Windows 10 version 1703 or greater.
      
    Tags:
    [`bazel_internal_configuration`](#effect_tag_BAZEL_INTERNAL_CONFIGURATION)

`--[no]workspace_rc` default: "true"
:   Whether or not to look for the workspace bazelrc file at $workspace/.bazelrc
      
    Tags:
    [`changes_inputs`](#effect_tag_CHANGES_INPUTS)

Miscellaneous options, not otherwise categorized.:

`--host_jvm_args=<jvm_arg>` multiple uses are accumulated
:   Flags to pass to the JVM executing Blaze.

`--host_jvm_debug`
:   Convenience option to add some additional JVM startup flags, which cause the JVM to wait during startup until you connect from a JDWP-compliant debugger (like Eclipse) to port 5005.
      
    Expands to:  
      `--host_jvm_args=-Xdebug`  
      `--host_jvm_args=-Xrunjdwp:transport=dt_socket,server=y,address=5005`

`--host_jvm_profile=<profiler_name>` default: ""
:   Convenience option to add some profiler/debugger-specific JVM startup flags. Bazel has a list of known values that it maps to hard-coded JVM startup flags, possibly searching some hardcoded paths for certain files.

`--server_javabase=<jvm path>` default: ""
:   Path to the JVM used to execute Bazel itself.
