This cargo subcommand will largely automate the process of building a Debian package. In order to get a Rust project build with `cargo deb`, you must add a [packages.metadata.deb] table to your Cargo.toml file. You must also ensure that you have filled out the minimal package information, particularly the `description` value.

### Example [package.metadata.deb]
The required keys are `maintainer`, `depends`, `section`, `priority`, and `assets`.

The `assets` are a list of files that will be installed into the system.
- The first argument of each asset is the location of that asset in the Rust project.
- The second argument is where the file will be copied
- The third argument is the permissions to assign that file via chmod.

```toml
[package.metadata.deb]
maintainer = "Michael Aaron Murphy <mmstickman@gmail.com>"
depends = "libc6"
section = "utility"
priority = "optional"
assets = [
    ["target/release/cargo-deb", "usr/bin", "755"],
    ["LICENSE", "usr/share/licenses/systemd-manager/COPYING", "644"]
    ["README.md", "/usr/share/doc/systemd-manager/README", "644"],
]
```

### Running `cargo deb`
Upon running `cargo deb` from the base directory of your Rust project, a Debian package will be saved in the same
directory.