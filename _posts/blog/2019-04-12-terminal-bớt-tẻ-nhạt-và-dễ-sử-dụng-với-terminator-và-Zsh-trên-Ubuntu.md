---
layout: post
title:  "Terminal bớt tẻ nhạt và dễ sử dụng với Terminator và Zsh trên Ubuntu"
date:   2019-04-12
excerpt: "Hãy thay đổi cái giao diện đen xì của cái terminal tẻ nhạt và tăng hiệu suất sử dụng nó hơn nữa ^^"
image: "/images/terminal.webp"
categories: "blog"
---

Từ hồi bước vào thế giới của Rails là gần như mình không thể dùng Windows cho việc develop Rails app được nữa. Và điều đầu tiên mọi người gặp phải khi làm việc với Ubuntu đó là khi làm việc với Terminal và các câu lệnh shell. Thật sự ấn tượng ban đầu của mình thì khó hiểu một cách kinh khủng và cảm giác cực kì khó control, làm việc cảm giác chậm hơn nhiều khi phải gõ và xử lý nhiều. Ngoài ra nhìn vào cái màn hình đen xì của cái terminal thấy thật tẻ nhạt. Nhưng khi sử dụng thì càng ngày mình càng thấy rõ được sự hiệu quả của nó và tại sao khi rất nhiều developer chọn sử dụng Ubuntu hay các sản phẩm open source thay vì sử dụng Microsoft

##  **Terminator,  Guake Terminal**

* Với terminal bình thường, khi sử dụng một thời gian chúng ta sẽ thấy có một số nhược điểm, như là: không split được nhiều màn hình, hay không luôn luôn start up hay onscreen, tắt 1 cách nhanh gọn. Thì để giải quyết vấn đề này mình khuyên các bạn nên sử dụng 1 trong 2 trình terminal trên. 

### Hướng dẫn cài đặt Terminator:

```SH
sudo add-apt-repository ppa:gnome-terminator
sudo apt-get update
sudo apt-get install terminator
```
> `Terminator` sẽ được cài đặt mặc định, và sau khi cài đặt cần phải khởi động lại terminal (shortcut: "Ctrl+Alt+T"). 
> Bây giờ chúng ta có thể khởi động `Terminator` và dùng thử, với `terminator` chúng ta có thể split 1 cửa sổ ra thành nhiều `terminal` khác nhau để tiện dụng cho việc sử dụng. Chỉnh được các phím tắt, như mình thường chỉnh Ctrl + C cho Copy, Ctrl + V cho Paste cho giống với iTerm2 trên MacOS.

### Hướng dẫn cài đặt Guake Terminal

> Các bạn vào trong Ubuntu Software Center và search "Guake Terminal" và cài đặt. 
> Chúng ta có thể cài đặt phím tắt để mở/tắt nhanh, phím tắt và rất nhiều thứ khác trong mục Preferences

## ZSH và Oh-my-zsh
* `Zsh` là một trình shell rất mạnh mẽ có thể tương tác như là một trình thông dịch và tương thích với Bash. (https://wiki.archlinux.org/index.php/zsh)

* `Oh-my-zsh` là một plugin của `Zsh` dùng để thay đổi giao diện của `terminal` và hỗ trợ các plugin (rails, git, OSX, hub, capistrano, brew, ant, php, python, etc) (http://ohmyz.sh/)

### Hướng dẫn cài đặt ZSH

```SH
sudo apt-get install zsh
```

> Khởi động lại Terminal, có 2 option cho việc chọn Shell config.
> Đừng quên khi cài đặt xong thì migrate các config từ file `.bashrc` to `.zshrc`

### Hướng dẫn cài đặt Oh-my-zsh
* Sau khi cài đặt xong `ZSH` thì tiếp tục cài đặt `Oh-my-zsh`
* Link Github: https://github.com/robbyrussell/oh-my-zsh

```SH
cd
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

* Như vậy là chúng ta đã hoàn thành xong việc cài đặt `Terminator` và `Oh-my-zsh`. Để có thể thay đổi themes và config  https://github.com/robbyrussell/oh-my-zsh/wiki/Themes



### Hướng dẫn cài đặt themes Agnoster
* Mình xin giới thiệu các bạn một themes khá đẹp và mình đang sử dụng đó là themes Agnoster (https://gist.github.com/agnoster/3712874)
* Đây là một themes khá dễ nhìn, màu sắc hài hoà.
* **Bước 1: Cài đặt Powerline Font**

```SH
cd
wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf
wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf
mv PowerlineSymbols.otf ~/.fonts/ #nếu chưa có thư mục .fonts thì tự tạo
mkdir -p .config/fontconfig/conf.d #nếu chưa có thư mục
```

* **Bước 2: Clear fonts cache**
```SH
fc-cache -vf ~/.fonts/
```

* **Bước 3: Di chuyển các file config**
```SH
mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/
```

* **Bước 4: Config ZSH**
>Mở file `.zshrc` bằng text editor

```SH
vim ~/.zshrc
```

>Thay đổi  dòng ZSH_THEME="robbyrussell"] thành [ZSH_THEME="agnoster"] sau đó khởi động lại terminal

* **Bước 5: Đổi màu của terminal thành Solarize**
* Trước hết máy phải cài đặt `dconf`, nếu chưa có thì: 

```SH
sudo apt-get install dconf-cli
```
* Clone repository của `solarized` và install
```SH
git clone git://github.com/sigurdga/gnome-terminal-colors-solarized.git ~/.solarized
cd ~/.solarized
./install.sh
```

* Mình khuyên các bạn nên chọn Option 1 (Dark themes) vì nó khá đẹp và dễ nhìn
* Để active đc Dark themes thì phải chuột ở `terminal`
*
```SH
Preferences>Profiles>Colors>Foreground and Background>Built-in schemes: Solarized dark 
Preferences>Profiles>Colors>Palette>Built-in schemes: Solarized
```

* **Bước 6: Đổi màu directory thành `Solarize`**

```
cd
wget https://raw.githubusercontent.com/seebi/dircolors-solarized/master/dircolors.ansi-dark
mv dircolors.ansi-dark .solarized
```


>Mở file `.zshrc` và thêm vào

```
eval `dircolors ~/.solarized/dircolors.ansi-dark`
```
>Khởi động là `terminal` và bạn đã có một terminal hoàn hảo hơn rất nhiều 

### Cài đặt một số plugin (optional)

* `Zsh` có hỗ trợ rất nhiều các plugin cho developer, mình xin hỗ trợ 2 plugin nổi bật và hiện tại mình đang dùng, bạn nào có plugin nào hay thì có thể comment thêm ở dưới
* `zsh-autosuggestions` (sẽ hiện mờ suggesstion cho người dùng https://github.com/zsh-users/zsh-autosuggestions#oh-my-zsh)
* `zsh-syntax-highlighting` (với các keyword sẽ được highlight để developer dễ nhìn hơn khi gõ shell https://github.com/zsh-users/zsh-syntax-highlighting)
* Có 2 cách cài đặt với `Zsh` và với `Oh-my-zsh` (chung với tất cả các plugin - Ngoài ra trong repo github cũng có hướng dẫn rất cụ thể của từng plugin)
*  **Với ZSH:**
  
```SH
1. Clone repository về máy
2. Mở file .zshrc và thêm 1 dòng   
3. source + đường dẫn đến file .zsh của plugin (VD: source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh)
```   
* **Với Oh-my-zsh**
```SH
1.  Clone repository vào thư mục $ZSH_CUSTOM/plugins  ( mặc định: ~/.oh-my-zsh/custom/plugins)
2.  Thêm plugin vào list plugin (VD: plugins=(zsh-autosuggestions))
3.  Bắt đầu phiên làm việc mới với Terminal
```

### Đối với Ruby developer (optional)
* **Plugin**
* Nếu bạn là Ruby developer bạn có thể thay thế 1 số plugins vào file `.zshrc`
```SH
plugins=(git rails rails3 ruby capistrano bundler heroku rake rvm autojump command-not-found python pip github gnu-utils history-substring-search zsh-syntax-highlighting)
```
* Đối với các bạn sử dụng `RVM`: 
```SH
RPROMPT="\$(~/.rvm/bin/rvm-prompt s i v g)%{$fg[yellow]%}[%*]"
```

* Đối với các bạn sử dụng `Rbenv`
```SH
RPROMPT='%{$fg[yellow]%}$(rbenv version-name)%{$reset_color%}%'
```


**That's it!**


