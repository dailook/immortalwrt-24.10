<img src="https://avatars.githubusercontent.com/u/53193414?s=200&v=4" alt="logo" width="200" height="200" align="right">

# ImmortalWrt 24.10 MTK Project   本项目fork自 ImmortalWrt源码

为方便mtk uboot刷入而修改

默认登录地址：http://192.168.2.1 或 http://immortalwrt.lan  用户名：root  密码：无

## 发展
要构建您自己的固件，您需要 GNU/Linux、BSD 或 macOS 系统（需要区分大小写的文件系统）。由于 Cygwin 不支持区分大小写的文件系统，因此不支持。

  ### 要求
  要构建此项目，建议使用 Debian 11 或者 ubuntu 18-22.04系统。您需要使用基于 AMD64 架构的 CPU、至少 4GB 内存和 25GB 可用磁盘空间。请确保互联网连接畅通。

  编译 ImmortalWrt 需要以下工具，不同发行版的包名称有所不同。

  - 以下是 Debian/Ubuntu 用户的示例：<br/>
    - 方法 1：
      <details>
        <summary>通过APT设置安装依赖项</summary>

        ```bash
        sudo apt update -y
        sudo apt full-upgrade -y
        sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
          bzip2 ccache clang cmake cpio curl device-tree-compiler ecj fastjar flex gawk gettext gcc-multilib \
          g++-multilib git gnutls-dev gperf haveged help2man intltool lib32gcc-s1 libc6-dev-i386 libelf-dev \
          libglib2.0-dev libgmp3-dev libltdl-dev libmpc-dev libmpfr-dev libncurses-dev libpython3-dev \
          libreadline-dev libssl-dev libtool libyaml-dev libz-dev lld llvm lrzsz mkisofs msmtp nano \
          ninja-build p7zip p7zip-full patch pkgconf python3 python3-pip python3-ply python3-docutils \
          python3-pyelftools qemu-utils re2c rsync scons squashfs-tools subversion swig texinfo uglifyjs \
          upx-ucl unzip vim wget xmlto xxd zlib1g-dev zstd
        ```
      </details>
    - 方法 2：
      ```bash
      sudo bash -c 'bash <(curl -s https://build-scripts.immortalwrt.org/init_build_environment.sh)'
      ```

  笔记：
    以非特权用户（而非 root）身份执行所有操作，无需 sudo。
    使用基于其他架构的 CPU 应该可以编译 ImmortalWrt，但需要更多的黑客攻击 - 根本没有任何保证。
    PATH 或驱动器上的工作文件夹中不能有空格或非 ASCII 字符。
    如果您使用的是适用于 Linux 的 Windows 子系统（或 WSL），则需要从 PATH 中删除 Windows 文件夹，请参阅构建系统设置 WSL文档。
    不建议使用 macOS 作为主机构建操作系统。没有任何保证。您可以从macOS 构建系统设置文档中获取相关提示。
    有关更多详细信息，请参阅构建系统设置文档。

  ### 快速入门
  1. 运行 `git clone -b openwrt-24.10 --single-branch --filter=blob:none https://github.com/dailook/immortalwrt-24.10` 以克隆源代码。
  2. 运行 `cd immortalwrt-24.10` 进入源目录。
  3. 运行 `./scripts/feeds update -a` 以获取 feeds.conf / feeds.conf.default 中定义的所有最新包定义
  4. 运行 `./scripts/feeds install -a` 安装所有获取的软件包的符号链接至 package/feeds/
  5. 运行 `make menuconfig` 以选择工具链、目标系统和固件包的首选配置。
  6. 运行 `make` 并构建您的固件。这将下载所有源代码，构建交叉编译工具链，然后为您的目标系统交叉编译 GNU/Linux 内核和所有选定的应用程序。

  ### 二次编译：
  
  ```bash
  cd immortalwrt  
  git pull
  ./scripts/feeds update -a
  ./scripts/feeds install -a
  make defconfig
  make download -j8
  make V=s -j$(nproc)
  ```
 
  ### 如果需要重新配置：
  
  ```bash
  rm -rf .config
  make menuconfig
  make V=s -j$(nproc)
  ```

编译完成后输出路径：bin/targets
