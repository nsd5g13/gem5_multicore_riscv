Original source codes from: https://github.com/GT-CHIPS/gem5_chips

Running OS: Ubuntu 22.04

Tools:
scons v4.0.1,
gcc 11.2.0,
python 2.7,

Notes: 

1. "scons" must be performed with Python 2.7, command:
$python2.7 `which scons' build/RISCV_MESI_Two_Level/gem5.opt

2. Do not treat warnings as errors:
gem5/chips-master/SConstruct:372-375, comment these codes out

3. When _SC_SIGSTKSZ_SOURCE or _GNU_SOURCE are defined, MINSIGSTKSZ and SIGSTKSZ are no longer constant on Linux:
Include the following definition in gem5_chips-master/build/RISCV_MESI_Two_Level/sim/init_signals.cc:
#define SIGSTKSZ 8192

4. Example run commands:
./build/RISCV_MESI_Two_Level/gem5.opt configs/example/se.py \
--cpu-type TimingSimpleCPU \
--num-cpus=64 \
--mesh-rows=64 \
--l1d_size=16kB \
--l1i_size=16kB \
--num-l2caches=64 \
--l2_size=128kB \
--num-dirs=4 \
--mem-size=4096MB \
--ruby \
--network=garnet2.0 \
--topology=CHIPS_Multicore_MemCtrlChiplet4 \
-c tests/test-progs/hello/bin/riscv/linux/hello

5. RISCV gcc cross compiler: https://github.com/riscv-collab/riscv-gnu-toolchain
