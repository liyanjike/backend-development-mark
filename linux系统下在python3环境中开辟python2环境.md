# linux系统下在python3环境中开辟python2环境

## 一、拉取镜像包 
1.尝试清华镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

conda config --set show_channel_urls yes
conda create -n 环境名称 python=2.7 numpy scipy pandas sqlalchemy

or
2.尝试中科大镜像
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/

conda config --set show_channel_urls yes
conda create -n yanli python=2.7 numpy scipy pandas sqlalchemy

## 二、进入python2环境
source activate + 环境名称 进入了python2的环境
此外，缺少包时在终端中可使用pip工具 pip install + 包名
pip --version可查看python版本


