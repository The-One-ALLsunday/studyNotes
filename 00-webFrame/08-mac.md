# MAC

## MAC开启ssh服务

- 启动服务
  - `sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist`
- 停止服务
  - `sudo launchctl unload -w /System/Library/LaunchDaemons/ssh.plist`
- 查看是否启动成功
  - `sudo launchctl list | grep ssh`
  - `0 com.openssh.sshd`  有此提示，则表示开启成功

## MAC 下载brew

该脚本用了中科大镜像加速访问，仅修改仓库地址部分，不会产生安全隐患。 关于中科大所提供的 Homebrew 镜像服务 

[简书相关文章](https://www.jianshu.com/p/e0471aa6672d)

- 终端执行 `/usr/bin/ruby -e "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install)"`

