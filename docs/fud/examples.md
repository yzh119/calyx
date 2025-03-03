# Examples

These commands will assume you're in the root directory of the Calyx
repository.

**Compiling Calyx.**
Fud wraps the Calyx compiler and provides a set of default compiler options
to compile Calyx programs to Verilog.

```bash
# Compile Calyx source in the test simple.expect
# to Verilog. We must explicitly specify the input
# file type because it can not be guessed from
# the file extension.
fud exec examples/futil/simple.expect --from futil --to verilog
```

Fud can explain its execution plan when running a complex sequence of
steps using the `--dry-run` option.
```bash
# Dry run of compiling the Dahlia dot product file
# to Calyx. As expected, this will *only* print
# the stages that will be run.
fud exec examples/dahlia/dot-product.fuse --to futil --dry-run
```

**Simulating Calyx.**
Fud can compile a Calyx program to Verilog and simulate it using Verilator.


```bash
# Compile and simulate a vectorized add implementation
# in Calyx using the data provided,
# then dump the vcd into a new file for debugging.
# === Calyx:   examples/futil/vectorized-add.futil
# === data:    examples/dahlia/vectorized-add.fuse.data
# === output:  v-add.vcd
fud exec \
  examples/futil/vectorized-add.futil \
  -o v-add.vcd \
  -s verilog.data examples/dahlia/vectorized-add.fuse.data
```

**Simulating Dahlia.**
The following command prints out the final state of all memories by specifying
`--to dat`.

```bash
# Compile a Dahlia dot product implementation and
# simulate in verilog using the data provided.
# === Dahlia: examples/dahlia/dot-product.fuse
# === data:   examples/dahlia/dot-product.fuse.data
#     (`.data` is used as an extension alias for `.json`)
fud exec \
  examples/dahlia/dot-product.fuse \
  --to dat \
  -s verilog.data examples/dahlia/dot-product.fuse.data
```

