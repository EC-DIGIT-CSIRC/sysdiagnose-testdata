# sysdiagnose-testdata

Non-sensitive sysdiagnose archives that can be used for unit testing sysdiagnose.

See also <https://github.com/EC-DIGIT-CSIRC/sysdiagnose>

## Fetching the test data

The sysdiagnose archives (`*.tar.gz`) in this repository are stored with
[Git LFS](https://git-lfs.com/). You must have Git LFS installed, otherwise
checkouts only produce small LFS *pointer* files (a few hundred bytes) instead
of the real archives, and the tests will fail.

1. Install Git LFS (once per machine)

    ```bash
    # macOS
    brew install git-lfs

    # Debian/Ubuntu
    sudo apt-get install git-lfs

    # then register the LFS hooks in your global git config
    git lfs install
    ```

2. Clone / update including this submodule

    When working from the parent `sysdiagnose` repository:

    ```bash
    git submodule update --init --recursive
    ```

3. Pull the LFS objects

    If the `.tar.gz` files are only a few hundred bytes, they are still LFS
    pointers and need to be downloaded:

    ```bash
    # from the parent repo
    git submodule foreach git lfs pull

    # or from inside this submodule
    git lfs pull
    ```

4. Verifying

    A correctly fetched archive is tens to hundreds of MB and reports as gzip data:

    ```bash
    file iOS15/*.tar.gz   # -> gzip compressed data, ...
    git lfs ls-files      # files marked with "*" are present on disk
    ```
