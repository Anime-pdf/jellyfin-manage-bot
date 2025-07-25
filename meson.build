project('jellyfin-manage-bot', 'cpp',
        version : '1.0.0',
        default_options : ['warning_level=3', 'cpp_std=c++20'])

host_os = host_machine.system()
host_cpu = host_machine.cpu_family()
is_64 = host_cpu == 'x86_64'

dpp = dependency('dpp', required: false)

if not dpp.found()
        dpp_base = 'libs/dpp'
        os_dir = host_os == 'windows' ? 'windows' : 'linux'
        arch_dir = is_64 ? 'lib64' : 'lib32'
        lib_prefix = host_os == 'windows' ? '' : 'lib'
        lib_ext = host_os == 'windows' ? 'lib' : 'so'

        dpp_lib_path = join_paths(meson.source_root(), dpp_base, os_dir, arch_dir, lib_prefix + 'dpp.' + lib_ext)
        dpp_include = include_directories(join_paths(dpp_base, 'include'))

        dpp = declare_dependency(
                include_directories: dpp_include,
                link_args: dpp_lib_path
        )
endif

sources = files('src/main.cpp')

jellyfin_manage_bot = executable(
        'jellyfin_manage_bot',
        sources,
        dependencies: [dpp],
        install : true
)

test('test', jellyfin_manage_bot)