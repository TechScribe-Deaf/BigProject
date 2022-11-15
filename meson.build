project('BigProject', 'c')

cppcheck_program = find_program('cppcheck')
valgrind_program = find_program('valgrind')
kcachegrind_program = find_program('kcachegrind')

# BigProject Dependencies
bigproject_deps = []
# BigProject Source Files
bigproject_src = [ 'src/main.c' ]
# BigProject Include Directories
bigproject_include = [ 'include/' ]

# Run cppcheck and print errors to terminal
run_target('cppcheck',
           command: [cppcheck_program, '--project=compile_commands.json', '--suppress=missingInclude', '--std=c11',
           '--max-ctu-depth=8', '--report-progress'])

bigproject_executable = executable('BigProject', sources: bigproject_src, dependencies: bigproject_deps, include_directories: bigproject_include)

# Run valgrind which defaults to memory leak check
run_target('valgrind',
            command: [valgrind_program, bigproject_executable])

# Generates callgraph file and then view it via kcachegrind program
run_target('callgraph',
            command: [valgrind_program, '--tool=callgrind', '--dump-instr=yes', '--collect-jumps=yes', '--callgrind-out-file=callgraph.out', bigproject_executable, '&&', kcachegrind_program, 'callgraph.out'])
            

