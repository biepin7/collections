1. 修改软件源

    ```
    vi /etc/apt/sources.list
    ```
    
2. 更新

    ```
    apt update && apt full-upgrade && apt autoremove -y
    ```

3. 语言安装支持 && 虚拟机显卡驱动

    ```
    apt install language-selector-gnome language-pack-kde-zh-hans language-pack-gnome-zh-hans open-vmtools -y
    ```

    